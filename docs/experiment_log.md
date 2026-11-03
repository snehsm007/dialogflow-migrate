# Experiment Log

Every full hill-climb evaluation run is logged here in chronological order. See [`docs/EVAL_LEDGER.md`](EVAL_LEDGER.md) for the complete cross-table ledger (Full Runs, Targeted Smokes, and Archived Retries).

- **Hill-Climb Policy:** Hill-climb strictly on **full evaluation runs only** (`100`-call unretried `retry_mode=null` Academy full runs and/or `70x3 = 210` `make bench-full` CES server runs). Never hill-climb on `retry_mode=failed` partial retries or merge smoke slices onto prior full runs.
- Always report **Strict `3/3`**, **Majority `>=2/3`**, and **Individual** pass rates side-by-side alongside the exact **Run ID**, **Git Branch + Commit SHA**, and **CES App Resource ID + Version**.
- Gate 3 (`70x3` CES full run) requires **Strict `3/3` >= 90% AND 100% Majority (`>=2/3`, zero `0/3` or `1/3` evals)** with `0` tool runtime errors.

Note: Day 2 v1 inherits ADRs 1–28 from Day 1 `snehsm-FDEBootcamp-CHI-greenfield` @ `84ed43a`.

| Iteration | Date (UTC) | Git Branch & Commit SHA | CES App ID & Version | Mechanism / Change | Strict `3/3` | Majority `>=2/3` | Individual / Full Score | Decision / Keep? | Full Run ID & Notes |
|---|---|---|---|---|---|---|---|---|---|
| **v1 (Full Baseline)** | `2026-11-03T18:16:44Z` | `main` @ code `f5c746a` (push `4032e92`, log `3ba37f6`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`c9fad922` / `git-f5c746a`) | Day 2 baseline (`snehsm-FDEBootcamp-CHI-migration`: 1 Root Router + 4 Domain Specialists + 22 tools + native `fr-CA`) | N/A (`1x` live Academy voice suite) | N/A (`1x` live Academy voice suite) | **`91/100` (`91.0%`)** (`63/70` public = `90.0%`, `28/30` secret = `93.3%`) | **KEEP — ACTIVE FULL-RUN BASELINE** | Academy Run `b400c58e4cbe47e38d03ce8858b317a2` (`submission_id=73fbf83dd8b943a9bf2745a165ddaaf9`, `retry_mode: null`, `0` retries). *(Historical `retry_mode=failed` runs `e0d94fd3...` -> `95%` and `ae76fff9...` -> `97%` archived in `docs/EVAL_LEDGER.md` and excluded from hill-climbing.)* |
| **v2 (Candidate R2)** | *Pending full run* | `fix/mig-round2` @ code `96edbf4` (push `436f785`, tip `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`a25187cf` / `git-96edbf4`) | ADR-33 (`tv_streaming` P0 guide & Fibe TV vs Satellite disambiguation), ADR-34 (`lookup_account` BAN kwargs), ADR-35 (`MOB-STARTER` plan alias), `docs/migration_audit.md` | *Smoke only so far (`5/7` `3/3` on `5c845c1d`)* | *Smoke only so far (`6/7` maj on `5c845c1d`)* | *Pending full run* | **PENDING FULL RUN** | Isolated on `8a121e2f-8601-4eac-bb77-ccf4f919374e`; awaiting user go-ahead for full `70x3` CES run or unretried `100`-call Academy full run. |
