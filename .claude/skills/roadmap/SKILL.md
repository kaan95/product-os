---
name: roadmap
description: >
  Build a portable, text-based product roadmap as a Notion page. Use this skill whenever the user wants
  to create, refine, or restructure a roadmap — outcome-oriented when possible, but flexible across
  framings (OKR, Now/Next/Later, Theme-based). Trigger phrases: "build me a roadmap", "quarterly
  planning", "Q2/Q3/Q4 roadmap", "Now Next Later", "turn these initiatives into a roadmap", "outcome
  roadmap", "we have OKRs but the roadmap is just a feature list", "help me frame our roadmap around
  outcomes", "roadmap for next quarter", "roadmap planning". Also trigger when the user pastes a list
  of features, initiatives, or goals and mentions planning, next quarter, strategy, or priorities.
  Handles ANY input format: Notion notes, messy bullets, markdown, free-form thoughts, or structured
  OKR drafts. Output is a Notion child page under the user's Roadmap root page.
---

# Roadmap Skill

Assemble a clear, scannable roadmap for a product or team and write it to Notion. The skill is opinionated about **outcomes over outputs** but flexible about framing — pick OKR, Now/Next/Later, or Theme-based depending on what fits the input.

A polished, fictional reference roadmap lives next to this file at `EXAMPLE.md`. Read it once before producing your first roadmap so the tone and shape are calibrated.

---

## Step 1 — Gather inputs (in this order)

Don't ask the user for anything you can pull from existing sources first.

1. **Horizon.** Quarter (`Q[N] [YYYY]`), half (`H[N] [YYYY]`), or rolling Now/Next/Later. Confirm with the user if not stated.
2. **Existing initiatives.** Query the Notion **Product Initiatives** database to surface what's already tracked:
   ```
   mcp__claude_ai_Notion__notion-query-data-sources
   data_source_url: collection://32f5e8ca-ce39-80d7-ad58-000b9fa65b14
   ```
   Filter by status / quarter if those properties exist; otherwise return all and let the user mark which belong on this roadmap.
3. **Existing outcomes.** Look in `.claude/product/outcomes/` for a file matching the horizon (e.g., `q2-2026-v*.md`). If present, reuse the Objectives/KRs verbatim — don't re-derive.
4. **Strategy context.** Read the most recent file in `.claude/product/strategy/`. Use its diagnosis and guiding policy as orientation when picking what makes the roadmap.
5. **Free-form input.** Anything the user pasted or described that isn't already captured above.

If outcomes don't exist yet, **redirect to the `product-outcomes` skill before continuing.** A roadmap without outcomes is a feature list. If the input is mostly stakeholder feature requests, **redirect to `discovery-opportunities`** first to find the underlying problems.

---

## Step 2 — Pick a framing

| Signal in input | Use |
|---|---|
| Clear quarterly outcomes/OKRs already drafted | **OKR** |
| Multi-quarter horizon, or "we don't know exactly when" | **Now / Next / Later** |
| Team organizes around themes/bets, outcomes attached underneath | **Theme-based** |
| Unclear | Ask the user, one line per option |

Don't force OKRs on input that doesn't have them. A Now/Next/Later list of three outcome-anchored items is more honest than seven invented KRs.

---

## Step 3 — Coach (only if needed)

If the input is mostly outputs ("redesign onboarding", "ship push notifications", "migrate infra"), reframe before structuring. Use this table:

| Output (avoid as KR / roadmap item) | Outcome (what it should say) |
|---|---|
| "Launch redesigned onboarding" | "% of new users completing onboarding rises from 45% → 70%" |
| "Ship push notifications" | "Weekly active users grow 15% as users return to finish tasks" |
| "Migrate to new infra" | "P95 API latency drops below 200ms" *or* mark as Committed Work |
| "Build admin dashboard" | "Support tickets about account settings drop 40%" |

Show your reframing reasoning to the user and let them correct. Don't block on perfect outcomes — a near-miss the user can react to beats a long questionnaire.

---

## Step 4 — Structure (framing-dependent)

### OKR framing

```
Objective (qualitative direction)
├── KR 1 (measurable, baseline → target, time-bound)
│   ├── Initiative A — Bet
│   └── Initiative B — Committed
└── KR 2
    └── Initiative C — Bet
```

A good Objective is qualitative, memorable, broad enough for multiple approaches. A good KR is a measurable change in behaviour or performance — not "Complete X" / "Launch Y" / "Ship Z". 2–4 Objectives per quarter, max.

### Now / Next / Later framing

Three sections. Each item names the outcome it serves and a confidence level (`H` / `M` / `L`):

- **Now** — committed, in flight, high confidence
- **Next** — likely next horizon, medium confidence
- **Later** — directionally important, low confidence on timing

### Theme-based framing

Themes (3–5) at the top level. Under each theme: the outcome the theme is moving, then the initiatives. Useful when several outcomes share a domain or audience.

### All three framings include

- **Committed Work (Non-outcome)** — security, compliance, contracts, critical tech debt. Be honest: "this is happening because we have to."
- **What we're NOT doing** — short list of items considered and deprioritized, with a one-line rationale each. Prevents scope creep; surfaces tradeoffs.
- **Open Questions / Risks** — assumptions that need validating, dependencies, unknowns.

---

## Step 5 — Write to Notion

Create a **child page** under the user's Roadmap root: `https://www.notion.so/Roadmap-3515e8cace398021b28ce58408cd4c14` (parent page id `3515e8ca-ce39-8021-b28c-e58408cd4c14`).

**Title format:**
- Quarterly: `Q2 2026 Roadmap`
- Half-year: `H2 2026 Roadmap`
- Rolling: `Now / Next / Later — 2026-04`
- Theme-based variant: append ` (Themes)`

**Before writing, check for an existing page with the same title.** Use `mcp__claude_ai_Notion__notion-fetch` on the parent page or query its descendants. If one exists, **never overwrite silently** — ask the user whether to:
- update the existing page via `notion-update-page` (`command: "update_content"`), or
- create a versioned sibling: `Q2 2026 Roadmap (v2)`.

**Create the page** with `mcp__claude_ai_Notion__notion-create-pages`. Use Notion blocks (headings, tables, callouts, toggles) to render the structure from Step 4. For each initiative on the roadmap, link to its Product Initiatives DB page if found in Step 1.

**End the page with a Sources section:**
- Outcomes file: `.claude/product/outcomes/q2-2026-v1.md` (if used)
- Strategy file: `.claude/product/strategy/<latest>.md` (if used)
- Date generated, framing chosen

This trace lets a future reader (or you, in a later session) understand what fed the roadmap.

---

## Step 6 — Tone, calibration, edge cases

- **Concrete, not corporate.** "DAU 12K → 18K" beats "grow engagement."
- **Honest about TBD.** "Retention improves (TBD baseline — first-week action)" beats invented numbers.
- **Match the user's level of detail.** A sketch should not produce a 10-page plan.
- **Preserve outcome thinking the user has already done.** Build on it, don't replace it.
- **Too many objectives?** More than 3–4 per quarter usually means trying to do everything. Flag it; suggest clustering or splitting into a primary focus and a secondary track.
- **Stakeholder feature dumps?** Translate to outcomes via `discovery-opportunities`; the features become initiatives under the relevant outcome.
- **No baseline metrics?** Mark `TBD` and include a first-week action to establish one.
- **Work that ties to no outcome?** It belongs in Committed Work — or it shouldn't be on the roadmap. Ask: "If this gets delayed a month, would anyone notice or care?"

If you made significant interpretation calls (inferred an outcome from a feature list, reframed a KR), briefly explain your reasoning so the user knows what to review.

---

## See also

- **`product-outcomes`** — define or refine the outcomes the roadmap is anchored on
- **`discovery-opportunities`** — extract underlying problems behind feature requests
- **`strategy`** — the diagnosis and guiding policy this roadmap operationalizes
- **`prd`** — detail any one initiative on the roadmap
- **`sprint-planner`** — break a sprint out of this roadmap
- **`context-update`** — keep individual initiative pages in Notion fresh (mirror its fetch-then-write Notion pattern)

---

## Reference: `EXAMPLE.md`

A fully populated, fictional B2B-scheduling-tool roadmap in OKR framing. Read it for tone and calibration before producing your first roadmap.
