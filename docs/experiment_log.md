# Experiment Log

Every cloud evaluation run and hill-climb iteration is logged here in chronological order.
Always report **Strict `3/3`**, **Majority `>=2/3`**, and **Individual** pass rates side-by-side (never composite slices across runs/SHAs).
Gate 3 requires **Strict `3/3` >= 90% AND 100% Majority (`>=2/3`, zero `0/3` or `1/3` evals)** with `0` tool runtime errors.

Note: Day 2 v1 inherits ADRs 1–28 from Day 1 `snehsm-FDEBootcamp-CHI-greenfield` @ `84ed43a`, which scored 0.89 unretried / 0.99 retry-chained on the identical 70 public scenarios.

| Iteration | Date (UTC) | Commit | Mechanism / Change | Impact Verdict (`make smoke-impact`) | Strict `3/3` | Majority `>=2/3` | Individual | Decision / Keep? | Full Run ID & Notes |
|---|---|---|---|---|---|---|---|---|---|
| 1 (v1 baseline) | 2026-11-03 16:16 | `4032e92` | Baseline migration import (1 Root Router + 4 Domain Specialists + 22 Tools) | PASS | -- | -- | -- | Deployed to app `0cf41d68-5bd0-4fda-b62f-d500cbdca886` | Academy Run 1 in-flight (`b400c58e4cbe47e38d03ce8858b317a2`) |
| 2 (Candidate Round 2) | 2026-11-03 16:30 | `HEAD` | ADR-33 (`tv_streaming` guide & TV platform disambiguation) + ADR-34 (`lookup_account` BAN/account_number kwargs) + ADR-35 (tier-symmetry plan aliases) + migration dossier | PASS | TBD | TBD | TBD | Candidate Round 2 for verification | Isolated candidate app on `fix/mig-round2` |

