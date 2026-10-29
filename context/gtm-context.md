# Shared GTM context (Q4 2026)

Every agent in this repo is seeded with this context directly in its prompt
(agents run with no memory and no local files, so this doc is the
source-of-truth copy — update both when something changes).

## Q4 2026 GTM objectives

1. **Land the Enterprise ARR plan.**
   - **Live unresolved conflict**: Sales' own "Sales - Q4 2026 OKRs - AMER +
     EMEA v5 (Oct 20 target reset)" Google Doc states **$42M**. Marketing,
     Customer Success, Enablement, GTM Ops, and Sales Assistance docs all
     state **$49M**. As of 2026-10-28, nobody had reconciled this.
     Isabelle (Brian's manager, runs the monthly GTM meeting) is the likely
     owner to resolve it.
   - **Unowned sub-goal**: "make GTM pipeline legible: one reporting,
     analytics & attribution layer." Nobody has claimed this.
2. **Be the #1 AI-native revenue org** — pipeline via agents across field
   events, outbound, and PLG.
3. **Best-in-class retention, expansion, and time to value.**

## Named competitors to track

Bolt, Replit, v0, Base44, Figma Make, Cursor, Emergent.

Note: `#gtm-rubberduck` tracks GTM-*tooling* vendor news — that is a
different thing from product-competitor mentions in deal conversations.
Never conflate the two.

## Systems this repo must never duplicate

- **Catalyst** (CS/Sales): Risk Alerts, Expansion Signals, renewal
  forecasting. Writes to HubSpot deal properties such as
  `annual_contract_value` and `renewal_type`.
  - *Open item*: exact internal HubSpot property names Catalyst uses for
    revenue-cycle signal filtering are still unconfirmed — ask Raj Jagirdar
    (2-minute question, weekly GTM Ops meeting).
- **Deal Creation Agent** (RevOps, owned by Raj Jagirdar): automated
  deal-stage moves and deal creation. API at
  `/api/public/catalyst/recommendations`. Retro posts also land in
  `#project-gtm-command-center`.

## Brian's four recurring meetings (for Meeting Prep)

1. Weekly 1:1 with Isabelle (his manager)
2. Weekly Sales Forecast & Pipeline Sync
3. Weekly GTM Ops Team meeting (Raj Jagirdar among others)
4. Monthly GTM-wide meeting, run by Isabelle, first Tuesday of the month
