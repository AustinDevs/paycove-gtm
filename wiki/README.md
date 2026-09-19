# paycove-gtm

## What this repo is

A single-page, no-build-step **interactive strategy tracker** ("Paycove Strategy Tracker") for the 2025 franchise go-to-market part-time-hire implementation plan. It is a static site (deployable as-is to GitHub Pages) with no framework and no dependencies beyond vanilla HTML/CSS/JS.

This repo is deliberately narrow in scope: it contains only the milestone/checklist tracker tool for the "20 hours/week" implementation plan. It does **not** contain the broader franchise GTM marketing site (`franchise.paycove.io` / `wordpress.paycove.io`), the HubSpot pipeline analysis, the Fastest Labs pilot materials, or any franchise-conference/channel strategy — those live only as business narrative in the Paycove Obsidian notes, not in this codebase.

## Files

- **`index.html`** — the entire application: styling (gradient/card UI) plus a small vanilla-JS renderer. On load it fetches `config.json`, renders one `.month-section` per month entry (flow steps → checklist → KPI grid), then a "Tools & Budget" section from `config.tools` / `config.timeAllocation`.
- **`config.json`** — all content. Structure:
  - `title` / `subtitle` — page header text
  - `months[]` — each has `id`, `number`, `title`, `subtitle`, `flowSteps[]` (time/title/description), `checklist[]` (plain strings), `kpis[]` (number/label). Currently populated for **Month 1** ("Foundation & Setup"), **Month 3** ("Scale & Validate"), and **Month 6** ("Convert & Expand") — Months 2/4/5 are not present.
  - `tools[]` — name/cost/description (LinkedIn Sales Navigator $80/mo, Apollo $100/mo, Loom $24/mo)
  - `timeAllocation[]` — category/hours breakdown of the 20 hrs/week (Prospecting 8, Outreach 6, Demos/Meetings 4, Follow-up/Admin 2)
- **`.github/workflows/`** — a `static.yml` GitHub Actions workflow that deploys the repo to GitHub Pages on push.

## How it works

- Checkbox completion state is stored in **`localStorage`** only (key `checkboxStates`), keyed by `<monthId>-<checklistIndex>`. There is no backend and no shared/multi-user state — progress tracked by one person in one browser only.
- `config.json` is also cached to `localStorage` (`strategyConfig`) as a fallback if the fetch fails (e.g. opened via `file://`).
- To update the plan's content (add a month, change KPIs/checklist items, adjust tools/budget), edit `config.json` directly — no rebuild step required.

## Current state

Last substantive commit: 2025-05-27 (`Update config.json`). The tool has not been touched since; it reflects the original 1/3/6-month plan drafted at GTM-pivot launch and has not been updated to track actual 2025–2026 progress (targets: ~100→200→300 prospects over 6 months, 1 pilot by month 3, 2–3 paying customers / $30–50K ARR by month 6).

## Related context (kept in Obsidian, not here)

The wider franchise GTM initiative — HubSpot pipeline conversion analysis, the Fastest Labs pilot/pricing, the `franchise.paycove.io` → `wordpress.paycove.io` site build-out, franchise-conference channel strategy, and the franchise/multi-entity data-model "moat" — is business strategy, not part of this codebase. See the Paycove Obsidian vault (`Paycove Franchise GTM Strategy.md`) for that narrative.
