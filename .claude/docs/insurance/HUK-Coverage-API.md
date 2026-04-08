# HUK Coverage API (Deckungsprüfung Service)

## Overview

Integration of HUK-COBURG's Deckungsprüfung (coverage verification) API into the Legalhero platform. When Legalhero receives a case from a HUK Rechtsschutz client, the platform calls HUK's API with the Versicherungsscheinnummer (policy number) to verify coverage status before processing the mandate.

**Jira:** [OS-2540 – BE: Implement VPN & API for HUK Coverage](https://legal-hero.atlassian.net/browse/OS-2540)  
**Status:** In Progress — Go-live committed for April 15, 2026  
**Last external contact:** Apr 1, 2026 (Kolhaupt replied to Kaan with API use case clarification)

---

## Key Contacts

| Person | Role | Company |
|---|---|---|
| Kaan Özgiray | Product Lead | Legalhero |
| Florian Langenhahn | Backend Engineer | Legalhero |
| Mohammad Amir | Software Architect | Legalhero |
| Lukas Klein | CEO | Legalhero |
| Christian Kolhaupt | Rechtsschutz-Schadenregulierung | HUK-COBURG |
| Kathrin Herbst | Rechtsschutz-Schadenregulierung | HUK-COBURG |
| Stephan Ochs | IT / Informatik-Betrieb | HUK-COBURG |
| Thomas Feickert | IT | HUK-COBURG |
| Dirk Bauer | IT | HUK-COBURG |

---

## What Was Done

### Nov 19, 2025 — Kaan proposes IP whitelist alternative
Kaan emailed HUK, apologizing for delays and proposing to use 3 static NAT IPs (18.156.48.145, 3.67.215.202, 3.69.228.228) for IP whitelisting instead of a VPN — citing lower implementation effort. Estimated go-live within a week if accepted.

### Nov 20, 2025 — HUK insists on VPN
Christian Kolhaupt declined the IP whitelist approach. HUK requires VPN for all partners for standardization. Directed to Stephan Ochs for setup.

### Nov 20–21, 2025 — VPN configuration back-and-forth
- Florian sent initial VPN config documents with PSKs → rejected by Ochs (wrong topology: 1:n VPN not possible, Phase 2 IPs can't match VPN gateway IPs)
- Florian submitted corrected config
- **Ochs confirmed: VPNs configured on HUK side** (datasheets: `VPN_LegalHero_V1-1t.pdf` for test, `VPN_LegalHero_V1-1p.pdf` for prod). Downstream firewall approvals ordered.

### Nov 21, 2025 — Credentials & test data exchanged
- Amir confirmed Legalhero has client_id + secret for **test** (from Phillip), requested credentials for **production**
- Thomas Feickert (HUK) provided test data:
  - Valid Versicherungsscheinnummer: `403020973H01`
  - Invalid: change any digit

### Nov 24, 2025 — HUK downstream firewalls approved
Stephan Ochs confirmed firewall approvals done. Testing could begin.

### Dec 8, 2025 — Internal catch-up
Florian forwarded the thread to Kaan to brief him on status.

### Dec 9–10, 2025 — VPN tunnel debugging
- Florian updated infra: single NAT instance, single Phase 2 IP `172.31.7.72`
- Ochs confirmed tunnel visible (`193.201.181.9 ↔ 172.31.7.72`) but **Rx/Tx = 0/0** — no traffic flowing from Legalhero side

### Dec 11, 2025 — VPN confirmed working (test)
Florian: *"Wir konnten gestern erfolgreich den API Server erreichen. Heisst also das VPN steht."* — VPN tunnel up, API server reachable. Team planned to integrate API calls into the application.

Stephan Ochs replied with updated datasheets for test and production, then went on vacation.

### Dec 15, 2025 — Jira ticket on Production (Ready for Review)
OS-2540 "BE – Implement VPN & API for HUK Coverage" marked as deployed to production and ready for review.

### Mar 31, 2026 — Kaan takes ownership, commits to April 15 go-live
After Lukas forwarded the escalation, Kaan replied directly to Kolhaupt (CC: Lukas, Kolhaupt, Kathrin Herbst):
- Apologized for the prolonged delay
- **Committed to go-live by April 15, 2026**
- Asked a clarifying question about the API's intent: per the interface spec (v1.0.0), only the Versicherungsscheinnummer is sent — no case details, service type, or legal area
- Shared the known response structures:
  - **Positive:** `{ "gdvKey": "02", "versichert": "JA", "langText": "Arbeits-Rechtsschutz" }`
  - **Negative:** `{ "vnrsnr": "403091410V01", "ergebnisListe": [], "fehlermeldung": "Die eingegebene Vertragsnummer / Schadennummer ist ungültig! (2)" }`
- Noted that the response confirms general insurance status and Rechtsschutz type — but **not whether the specific case or service type is covered**
- Asked: Is there a second step where case-specific data (service type, legal area) is submitted for a concrete coverage decision?

### Apr 1, 2026 — Kolhaupt clarifies API use cases and scope
Kolhaupt replied confirming the integration and clarifying the intended use:

**Use case 1 — Validate the Versicherungsscheinnummer / Schadennummer**
Catches typos from manual input (e.g., phone-based transfers in Owi proceedings).

**Use case 2 — Coverage confirmation for non-pre-screened mandates**
Cases that are not routed through HUK's internal case managers — specifically:
- Self-acquired cases (*selbst akquirierte Sachverhalte*)
- Follow-up mandates (*Folgemandate*)

Example: In traffic law, HUK may only send one mandate (Owi or accident), but during legal review both cases apply and both mandates should be accepted. Today this requires a manual second-case request. The API eliminates this.

**Coverage logic confirmed:**
- If the service returns **yes** for gdvKey **07, 09, or 11** → this counts as a **Deckungsprüfungszusage** for the agreed Pauschale
- **Court representation** (außergerichtliche cases outside Owi/criminal) → **remains manual for now**
- Future scope expansion (e.g., covering court representation) can be discussed once the service is live

---

## Current Status (as of Apr 7, 2026)

**Infrastructure status (as of HUK's Mar 31 assessment):**
- Test VPN tunnel: exists, connects occasionally, but no API traffic has ever flowed
- Production VPN tunnel: does not exist

**Communication status:**
- Kaan has re-engaged Kolhaupt (Mar 31), committed to April 15 go-live
- Kolhaupt responded positively on Apr 1 with API use case clarification
- Relationship recovered — HUK is now cooperative

**Implementation status:**
- **The application-level endpoint that calls the HUK API has not been built.** The Dec 15 Jira deployment appears to have covered VPN infrastructure only — not the actual business logic that triggers a coverage check when a new case is created.
- There is no integration today where creating a HUK Rechtsschutz case triggers an automatic Deckungsprüfung API call.

---

## API Behavior (Clarified Apr 1, 2026)

**Request:** Only the Versicherungsscheinnummer is sent — no case details, service type, or legal area.

**Response (positive):**
```json
{ "gdvKey": "07", "versichert": "JA", "langText": "Verkehrs-Rechtsschutz" }
```

**Response (negative / invalid):**
```json
{ "vnrsnr": "403091410V01", "ergebnisListe": [], "fehlermeldung": "Die eingegebene Vertragsnummer / Schadennummer ist ungültig! (2)" }
```

**Coverage logic:**
- gdvKey **07** (Verkehrs), **09** (Straf/Owi), or **11** (?) returning `versichert: JA` → counts as **Deckungsprüfungszusage** for the agreed Pauschale
- gdvKey **02** (Arbeits-RS) and other keys → may need separate handling
- Gerichtliche Vertretung (outside Owi/criminal) → **still manual** for now

**This API does not** confirm coverage for a specific case or service type — it confirms the insurance contract exists and what Rechtsschutz category it covers.

---

## Open Questions

- Does Legalhero have the **production** client_id and secret? (Amir requested these in Nov 2025 — confirm with Amir)
- What criteria define a "HUK Rechtsschutz case" in our system — which intake fields / partner indicators trigger a coverage check?
- Which gdvKeys map to which of our 4 service types (Telefonische Erstberatung, Dokumentenprüfung, Außergerichtliche Vertretung, Gerichtliche Vertretung)?
- What should happen in the intake flow if the API returns negative or an error — block the case, flag for manual review, or proceed?
- Is the production VPN truly unconfigured, or just not tested yet?

---

## Next Steps (deadline: April 15, 2026)

### Infrastructure
- [ ] **Confirm production VPN:** Re-engage Stephan Ochs (HUK IT) to configure/verify the production VPN tunnel
- [ ] **Confirm production credentials:** Verify with Amir whether production client_id + secret were ever received; request from HUK if not
- [ ] **E2E test on test environment:** Run a real API call through the VPN tunnel with test Versicherungsscheinnummer `403020973H01` — confirm traffic flows end-to-end

### Implementation (core work)
- [ ] **Build the Deckungsprüfung endpoint:** Implement the backend logic that calls the HUK Coverage API whenever a new case is created that matches HUK Rechtsschutz criteria (by Florian/Amir)
- [ ] **Define trigger criteria:** Agree on which cases should trigger a coverage check (partner = HUK Rechtsschutz, which service types, etc.)
- [ ] **Handle API response in intake flow:** Map gdvKey 07/09/11 to coverage confirmation; define behavior for negative / error responses
- [ ] **E2E test on production:** Execute a real coverage check against the production API with a valid Versicherungsscheinnummer

### Communication
- [ ] **Keep Kolhaupt updated** on progress — he's cooperative now, don't let another silence build up
