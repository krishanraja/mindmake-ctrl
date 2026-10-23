# CTRL North Star

Status: Reference
Owner: Mindmaker
Last verified: 2026-08-20

Definition, view, table, and function names confirmed against `supabase/migrations/20260704120000_north_star_flywheel.sql`. The `north-star-daily-snapshot` cron job was confirmed active at `0 6 * * *` by production readback on 2026-08-20, so the trend line is genuinely being populated.

## Horizon

> By March 2027, 100 leaders turn the flywheel every week. CTRL is what a leader keeps after the room, and they would refuse to give it back.

Set by Krish on 18 October 2026, and not reached yet. Everything below serves it, every session in this repository works toward it, and only Krish changes it.

## The number

**Flywheel leaders this week (at least 5 brain facts and a decision weighed in the last 7 days)**: 1,000 by 29 March 2027, on a front-loaded weekly ladder. Checkpoints: 16 Nov 2026: 9; 14 Dec 2026: 32; 11 Jan 2027: 95; 8 Feb 2027: 242; 29 Mar 2027: 1,000.

```yaml north-star-metric
metric: "Flywheel leaders this week (at least 5 brain facts and a decision weighed in the last 7 days)"
unit: count
direction: up
target: 1000
deadline: 2027-03-29
ladder_shape: front-loaded
source: "Supabase ctrl: north_star_flywheel view"
status: active
ladder:
  - [2026-10-26, 1]
  - [2026-11-02, 3]
  - [2026-11-09, 6]
  - [2026-11-16, 9]
  - [2026-11-23, 12]
  - [2026-11-30, 17]
  - [2026-12-07, 24]
  - [2026-12-14, 32]
  - [2026-12-21, 43]
  - [2026-12-28, 57]
  - [2027-01-04, 74]
  - [2027-01-11, 95]
  - [2027-01-18, 122]
  - [2027-01-25, 154]
  - [2027-02-01, 194]
  - [2027-02-08, 242]
  - [2027-02-15, 301]
  - [2027-02-22, 372]
  - [2027-03-01, 457]
  - [2027-03-08, 559]
  - [2027-03-15, 681]
  - [2027-03-22, 827]
  - [2027-03-29, 1000]
```

Urgency (U1 to U5) is worked out every week from where the number stands against that week's target, by [the harness contract](https://github.com/krishanraja/ai-harness/blob/main/contract/north-star-metric.md). Set by Krish on 23 October 2026.

## The outcome

CTRL exists to give a time-poor founder or small-team CEO a quieter way through AI: notice what matters, weigh a real decision against evidence, and compound useful context without surrendering judgement. See [`docs/current/product.md`](../docs/current/product.md) and [`docs/current/commercial.md`](../docs/current/commercial.md).

## The moat metric (founder-signed 2026-07-04): the flywheel

The one number that proves the product works is the **flywheel**: context in, judgment out, recurring.

> **Flywheel leaders (this week)** = leaders who BOTH (a) hold a real brain (at least 5 current facts in `user_memory`) AND (b) weighed at least one decision in the last 7 days.

Either half alone is not the product working. A rich brain that never drives a decision is a filing cabinet. A decision with no brain behind it is a generic answer. Both together, week over week, is the flywheel turning: the more the leader tells CTRL, the sharper the weigh, so they come back and tell it more.

Two component counts are tracked alongside it so a dip is diagnosable:
- **brain_rich_users**: leaders with a real brain (a context problem if this falls).
- **active_deciders**: leaders who weighed a decision in the last 7 days (an engagement problem if this falls).
- **weekly_active_users**: the denominator the flywheel converts (any decision or memory write in 7 days).

## How it is instrumented

Migration `supabase/migrations/20260704120000_north_star_flywheel.sql`:
- `north_star_flywheel` (view): the current live snapshot, on demand.
- `north_star_daily` (table): a daily snapshot for the trend line (RLS on, service-role only).
- `snapshot_north_star()` (function): upserts today's row, idempotent.
- `north-star-daily-snapshot` (pg_cron, 06:00 UTC daily): populates the trend from day one.

Read it now:

```sql
select * from north_star_flywheel;                 -- current
select * from north_star_daily order by day desc;  -- trend
```

The threshold "at least 5 current facts" lives in `ns_brain_min_facts()`; change it there and both the view and the daily snapshot follow.
