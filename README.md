# Chief of Staff (CoS)

A set of scheduled, read-only agents that cover GTM planning gaps for Brian Le
(Strategy & Planning Lead, Lovable) that aren't already owned by an existing
system. They run as Claude Code scheduled routines in **shadow mode**: they
read, synthesize, and DM Brian on Slack. They never write anywhere, never
message anyone but Brian, and never duplicate a signal another system already
owns.

## Why these four and not more

Lovable already runs two mature, owned systems in the GTM org:

- **Catalyst** — CS/Sales product. Risk Alerts, Expansion Signals, renewal
  forecasting. Writes to HubSpot deal properties (e.g. `annual_contract_value`,
  `renewal_type`).
- **Deal Creation Agent** — RevOps. Automated deal-stage moves and deal
  creation. API at `/api/public/catalyst/recommendations`. Owned by Raj
  Jagirdar.

An earlier draft of this system proposed eight agents. After recon into what
already exists, four survived as genuine gaps — the planning layer *above*
Catalyst and the Deal Creation Agent, not a duplicate of either:

| Agent | Gap it fills |
|---|---|
| [OKR Consistency Watcher](agents/okr-consistency-watcher.md) | Nobody was tracking cross-team numeric/definitional conflicts in Q4 OKR docs |
| [Competitive Signal Scanner](agents/competitive-signal-scanner.md) | Nobody was surfacing real competitor mentions from live deal conversations to Brian specifically |
| [Planning Synthesizer](agents/planning-synthesizer.md) | Nobody was synthesizing daily/weekly/monthly at the planning level, above Catalyst and the Deal Creation Agent |
| [Meeting Prep](agents/meeting-prep.md) | Nobody was preparing Brian for his four recurring meetings using Granola + calendar context |

See [context/gtm-context.md](context/gtm-context.md) for the shared Q4 2026
facts every agent is seeded with, and [routines/README.md](routines/README.md)
for exactly how and when each one runs.

## Operating principles (all four agents)

1. **Guardrail first.** Every agent checks its required connectors before
   doing anything else. If they're missing, it says so in one plain sentence
   and stops — it never fabricates a meeting, a document, a number, or a
   quote to fill the gap.
2. **Never re-derive a signal another system already owns.** If Catalyst or
   the Deal Creation Agent already surfaced something to its own owner, these
   agents only escalate it if it has a *planning-level* implication (a Q4 OKR
   impact, a cross-functional gap, or a pattern across several accounts).
3. **Shadow mode.** Current tier: log + Slack DM to Brian only. No writes, no
   autonomous actions, no messages to anyone else. See
   [routines/README.md](routines/README.md#autonomy-tiers) for the promotion
   plan.
4. **No memory across runs.** Each scheduled run is a fresh session with no
   local files — every agent definition is written to be fully
   self-contained.

## Status

Live and running since 2026-10-29. See
[routines/README.md](routines/README.md) for current schedule, trigger IDs,
and open items (HubSpot property names, DST).
