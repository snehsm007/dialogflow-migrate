# Evaluation Ledger (Single Source of Truth)

> **Governance Rules (Mandatory):**
> 1. **Full Runs Only for Hill-Climbing:** Never hill-climb on failed-case retries (`retry_mode=failed`) or targeted smokes (`smoke-*`). Every candidate Keep/Discard decision is measured strictly by comparing **unretried full evaluation runs** (`100`-call `retry_mode=null` Academy full runs and/or `70x3 = 210` `make bench-full` CES server runs).
> 2. **Mandatory Provenance:** Every evaluation run must record its exact **Run ID**, **Git Branch & Commit SHA** (both deployed code SHA and repo log SHA), and **CES App Resource ID + Version**.
> 3. **Strict Separation:** Full runs (`full-*` / unretried `100`-call Academy runs), targeted server smokes (`smoke-*`), and historical `retry_mode=failed` runs are tracked in separate tables below and are never merged into synthetic composite scores.

---

## Deployed CES Applications Inventory

| Alias | CES Display Name | CES App Resource Name | Deployed Version ID & Tag | Git Branch & Code SHA | Source Fingerprint | Role |
|---|---|---|---|---|---|---|
| **v1 (Prod / Baseline)** | `snehsm-FDEBootcamp-CHI-migration` | `projects/fde-bootcamp/locations/us/apps/0cf41d68-5bd0-4fda-b62f-d500cbdca886` | `versions/c9fad922-3080-4397-b78c-45cc5e71648c` (`git-f5c746a`) | `main` @ code `f5c746a` (push log `4032e92`) | `3027b46559602cfc` | Active Academy submission (`73fbf83dd8b943a9bf2745a165ddaaf9`) & full-run baseline |
| **v2 (Candidate R2)** | `snehsm-FDEBootcamp-CHI-migration-r2` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e` | `versions/a25187cf-e8ac-4bf1-acc9-e53969119bbe` (`git-96edbf4`) | `fix/mig-round2` @ code `96edbf4` (push log `436f785`, tip `07e5d91`) | `b1fb07c78bebf033` | Isolated sandbox candidate (ADR-33 `tv_streaming`, ADR-34 BAN kwargs, ADR-35 `MOB-STARTER` alias) |

---

## 1. Full Evaluation Runs (Active Hill-Climbing Ledger — `0` Retries)

| Iteration | UTC Timestamp | Run ID (Clickable / Resource) | Git Branch & Commit SHA | CES App ID & Version | Suite & Modality | Strict `3/3` | Majority `>=2/3` | Public (`70`) | Secret (`30`) | Official Full Score | Hill-Climb Verdict |
|---|---|---|---|---|---|:-:|:-:|:-:|:-:|:-:|---|
| **v1 Baseline** | `2026-11-03T18:16:44Z` | Academy Run [`b400c58e4cbe47e38d03ce8858b317a2`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/b400c58e4cbe47e38d03ce8858b317a2) (`sub=73fbf83dd8b943a9bf2745a165ddaaf9`, `retry_mode=null`) | `main` — code `f5c746a` (log `3ba37f6`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`c9fad922` / `git-f5c746a`) | `100` live voice sims (`1x`, unretried) | N/A (`1x` suite) | N/A (`1x` suite) | **`63/70` (`90.0%`)** | **`28/30` (`93.3%`)** | **`91/100` (`91.0%`)** | **ACTIVE BASELINE (`KEEP`, `>90%` clean pass)** |
| **v2 Candidate** | *Pending* | *Awaiting full run (`make bench-full` `70x3` or clean `100`-call Academy run)* | `fix/mig-round2` — code `96edbf4` (tip `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`a25187cf` / `git-96edbf4`) | — | — | — | — | — | — | **ISOLATED CANDIDATE (Awaiting full-run evaluation)** |

---

## 2. Targeted CES Server Smoke Runs (`Gate 1` — Diagnostic Only, Never Merged into Full Score)

| Label | UTC Timestamp | CES `evaluationRuns` Resource ID | Git Branch & Commit SHA | CES App ID & Version | Scope & Modality | Strict `3/3` | Majority `>=2/3` | Individual | Tool Errors | Notes |
|---|---|---|---|---|---|:-:|:-:|:-:|:-:|---|
| `smoke-failed7-text-r2` | `2026-11-03T18:39:32Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/5c845c1d-1d51-41d0-bbe5-587df3ce584d` | `fix/mig-round2` — code `96edbf4` (runner `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-96edbf4`) | `7` evals × `3` = `21` (`text`: `VE-16,37,39,50,56,57,66`) | **`5/7` (`71.4%`)** | **`6/7` (`85.7%`)** | `18/21` (`85.7%`) | `0` | `VE-37,39,50,56,57` all `3/3` `P P P`; `VE-66` `2/3`; `VE-16` `1/3` (DTMF) |
| `smoke-failed7-audio-r2` | `2026-11-03T18:39:53Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/3118cb57-389f-429a-bd8b-25f813c0146a` | `fix/mig-round2` — code `96edbf4` (runner `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-96edbf4`) | `7` evals × `3` = `21` (`audio`: `VE-16,37,39,50,56,57,66`) | *In-flight* | *In-flight* | `10/11` so far (`21` total) | — | CES server audio smoke launched prior to full-runs-only policy |

---

## 3. Archived Failed-Only Retries (`retry_mode=failed` — Discontinued; Excluded from Hill-Climbing)

> **Policy Note (2026-11-03T18:57Z):** Partial `retry_mode=failed` runs pre-credit prior passes and re-dial only failed scenarios. They remain recorded on the Academy leaderboard and in `history/academy/run-*.json` for audit provenance, but **we no longer run `retry_mode=failed` and never use retry scores for hill-climbing**.

| Historical Label | UTC Timestamp | Academy Run ID & Parent | Git Branch & Commit SHA | CES App ID & Version | Retried Slice | Public (`70`) | Secret (`30`) | Cumulative Leaderboard Score | Governance Status |
|---|---|---|---|---|---|:-:|:-:|:-:|---|
| `v1 Retry 1` | `2026-11-03T18:44:20Z` | [`e0d94fd317764b4a9c5601acd3821648`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/e0d94fd317764b4a9c5601acd3821648) (`prior=b400c58e...`) | `main` — code `f5c746a` (recorded `de8ff99`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`git-f5c746a`) | `9` failed calls (`91` pre-credited) | `66/70` (`94.3%`) | `29/30` (`96.7%`) | `95/100` (`95.0%`) | **ARCHIVED (Not a full run)** |
| `v1 Retry 2` | `2026-11-03T18:53:45Z` | [`ae76fff99a0341999a244697daaf3c18`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/ae76fff99a0341999a244697daaf3c18) (`prior=e0d94fd3...`) | `main` — code `f5c746a` (tag `academy-best-0.97` @ `de8ff99`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`git-f5c746a`) | `5` failed calls (`95` pre-credited) | `67/70` (`95.7%`) | `30/30` (`100.0%`) | `97/100` (`97.0%`) | **ARCHIVED (Not a full run)** |
