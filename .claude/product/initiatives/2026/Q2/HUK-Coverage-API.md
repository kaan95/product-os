# HUK Coverage API (Deckungsprüfung Service)

## Overview

Integration of HUK-COBURG's Deckungsprüfung (coverage verification) API into the Legalhero platform. When Legalhero receives a case from a HUK Rechtsschutz client, the platform calls HUK's API with the Versicherungsscheinnummer (policy number) to verify coverage status before processing the mandate.

**Jira:** [OS-2540 – BE: Implement VPN & API for HUK Coverage](https://legal-hero.atlassian.net/browse/OS-2540)  
**Status:** Blocked / Stalled  
**Last external contact:** Mar 31, 2026 (HUK escalated to Lukas Klein)

---

## Key Contacts

| Person | Role | Company |
|---|---|---|
| Kaan Özgiray | Product Lead | Legalhero |
| Florian Langenhahn | Backend Engineer | Legalhero |
| Mohammad Amir | Software Architect | Legalhero |
| Lukas Klein | CEO | Legalhero |
| Christian Kolhaupt | Rechtsschutz-Schadenregulierung | HUK-COBURG |
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

---

## Current Status (as of Mar 31, 2026)

**HUK's assessment (from Kolhaupt's escalation email to Lukas Klein on Mar 31, 2026):**

> - **Test environment:** VPN tunnel exists, connects occasionally, but **no actual API traffic has ever flowed**
> - **Production environment:** VPN tunnel does **not exist**
> - Last known email contact: Dec 11, 2025 — 3.5 months of silence

Lukas Klein replied to Kolhaupt: *"Ich kümmere mich und komme auf dich zurück."* (I'll handle it and get back to you.)

HUK is frustrated. They have received multiple commitments from different Legalhero stakeholders over months, none of which delivered the integration.

---

## Open Questions

- Did the Dec 15 production deployment actually integrate and test real API calls, or only the VPN infrastructure?
- Does Legalhero have the **production** client_id and secret? (Amir requested these in Nov 2025 — unclear if received)
- Why did traffic never flow in test despite Florian confirming the API was reachable on Dec 11?
- Is the production VPN actually not configured, or just misconfigured?

---

## Next Steps

- [ ] **Lukas → Kaan/Flo/Amir:** Brief the team on HUK's escalation and get an honest internal status
- [ ] **Clarify prod credentials:** Confirm whether the production client_id + secret were ever received from HUK
- [ ] **Fix test environment:** Diagnose why no API traffic has flowed despite the VPN tunnel being up — run a real end-to-end coverage check against test API
- [ ] **Set up production VPN:** Re-engage Stephan Ochs (HUK IT) to configure the production VPN tunnel
- [ ] **Run production E2E test:** Execute a real coverage check against the production API with a valid Versicherungsscheinnummer
- [ ] **Reply to Kolhaupt with a concrete timeline** (Lukas committed to getting back to him)
- [ ] **Define go-live criteria:** Coverage check integrated into intake flow, tested with real HUK cases
