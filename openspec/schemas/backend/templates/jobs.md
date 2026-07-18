---
schema-version: 1.2.1
document-version: 0
---

# Background jobs

<!-- CONDITIONAL - only when the system has time-triggered or background work
     outside its request/event surface (scheduled jobs, batch pipelines, workers).
     Run identity/restart vocabulary: Spring Batch domain language + Jakarta Batch;
     overlap policy: Kubernetes CronJob concurrencyPolicy terms.
     Defaults stated once; jobs record deviations from conventions.md and defaults only.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal; repeat the job block per job.
     Delete guidance comments when done. -->

## Defaults

<!-- Stated once for all jobs. -->
| Rule | Value |
|------|-------|
| Schedule timezone | `<IANA tz, e.g. UTC>` |
| Late start | `<run late / skip after <deadline>>` |
| Overlap | `<Allow / Forbid (skip) / Replace>` |
| Retry/backoff | `<per conventions.md or job-level policy>` |

## Jobs

### `<job name>`

- **Purpose**: <one line - implements requirements operation `<name>`>
- **Trigger**: `<cron expression (POSIX five-field) / interval / manual / on-event: channel>`
- **Run identity**: <the identifying parameters (e.g. business date) that make two runs the same logical run - defines what a rerun means>
- **Restart & rerun**: `<restartable from checkpoint / restarts from start>`; rerun of a completed run: `<no-op / idempotent recompute>`
- **Input scope**: `<full scan / incremental since <watermark>>`
- **Effects**: <what it writes; events published (events.md channel by name) and the write-vs-publish relation - see sequences: `<flow>`>
- **Failure**: <behavior on partial failure and the state a failed run leaves; retry deviations from defaults>
- **Backfill**: `<how past periods are re-run / not supported>`
