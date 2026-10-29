# Routines guide

All four agents run as Claude Code scheduled routines (claude.ai "routines"),
created directly in the routines UI on 2026-10-29. Each fires a fresh,
no-memory session on its own cron schedule and DMs Brian on Slack.

## Current schedule

| Routine | Agent | Cadence | Trigger ID |
|---|---|---|---|
| `meeting-prep-brian-daily` | [Meeting Prep](../agents/meeting-prep.md) | Weekdays 6:30am PT | `trig_01GHANkZZHPhXjvA91mfuzZn` |
| `gtm-planning-synthesizer-daily-brief` | [Planning Synthesizer](../agents/planning-synthesizer.md) (daily) | Weekdays 7:00am PT | `trig_01P1ki6srtZkyNnugy2PXqt2` |
| `competitive-signal-scanner-daily` | [Competitive Signal Scanner](../agents/competitive-signal-scanner.md) | Weekdays 6:00am PT | `trig_01XxdSQ6yXygKUSRMHYeYdsv` |
| `okr-consistency-watcher-weekly` | [OKR Consistency Watcher](../agents/okr-consistency-watcher.md) | Mondays 7:00am PT | `trig_01PsRW2kURUzJ8RWZka2AaAj` |
| `gtm-planning-synthesizer-weekly-report` | [Planning Synthesizer](../agents/planning-synthesizer.md) (weekly) | Fridays 3:00pm PT | `trig_01QBPA7P7dHsvV8vn37z8WrK` |
| `gtm-planning-synthesizer-monthly-review` | [Planning Synthesizer](../agents/planning-synthesizer.md) (monthly) | 1st of month, 8:00am PT | `trig_0193kyA9YGbGXM4hd7wgSn4z` |

All six were created through the claude.ai routines UI directly, each with a
broad connector set attached (Slack, HubSpot, Notion, Granola, Google
Calendar, and the rest of the account's connectors). An agent session cannot
update or delete a routine it didn't create itself via the API — only the
owning account can edit these, at `claude.ai/code/routines/<trigger_id>`.

## Known open item: Daylight Saving Time

These six were created with plain UTC cron expressions reflecting Pacific
Daylight Time (UTC-7). DST ends 2026-11-01, at which point Pacific time
becomes PST (UTC-8) and every routine above will fire **one hour earlier**
than its intended Pacific time until the cron expressions are updated.

The durable fix is a timezone-aware cron
(`CRON_TZ=America/Los_Angeles <minute> <hour> <dom> <mon> <dow>`), which
handles DST automatically going forward — e.g. the OKR watcher would become
`CRON_TZ=America/Los_Angeles 0 7 * * 1`. This has to be done by the account
owner through the routines UI (an agent session can't update a routine it
didn't create via the API).

## Autonomy tiers

Currently **tier 0: shadow mode** — every agent's only allowed action is
reading data and sending Brian a Slack DM. No writes to HubSpot, Notion, or
anywhere else. No messages to anyone but Brian.

Planned promotion path, after 1-2 weeks of validating the signal taxonomy
against real dismissals and missed signals:

1. **Tier 0 — shadow** (current): log + DM Brian only.
2. **Tier 1 — flagged pings**: same as tier 0, but urgent items (e.g. a
   competitor mention in a $25k+ open deal) get a distinct, higher-visibility
   Slack format.
3. **Tier 2 — autonomous low-risk writes**: e.g. the OKR Consistency Watcher
   creating/updating a tracking doc in Notion, still never messaging anyone
   but Brian.

Do not promote a tier without Brian's explicit sign-off — these agents
default to the least autonomous behavior that still does the job.

## Other open items

- **HubSpot property names**: Catalyst's exact internal HubSpot property
  names for revenue-cycle signal filtering are unconfirmed. Two-minute
  question for Raj Jagirdar at the weekly GTM Ops meeting. See
  [context/gtm-context.md](../context/gtm-context.md).
- **Repo as source of truth**: the routines currently run with their prompts
  inline (set at creation time in the UI). This repo is the documentation /
  review copy. If a prompt changes here, it must also be updated in the
  routine itself — there's no automatic sync.
