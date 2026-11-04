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
| **v3 (Candidate R3)** | `snehsm-FDEBootcamp-CHI-migration-r2` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e` | `versions/02cafd7f-872c-4826-8e25-f27bd2c46e98` (`git-3f8ddb5`) | `fix/mig-round2` @ code `3f8ddb5` (push log `c4441be`) | `38933eeb6d234ba4` | Isolated candidate R3 (ADR-36 unfiled card, ADR-37 prospect port-in & donor SMS, ADR-38 queue routing, ADR-39 mixed ASR recovery) |
| **v4 (Candidate R4)** | `snehsm-FDEBootcamp-CHI-migration-r2` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e` | `versions/ba90c2f2-f7eb-4a35-b29d-b4d0c69b3c25` (`git-31d0b36`) | `fix/mig-round4` @ code `31d0b36` (push log `2d6c47a`) | `b4568a2092841788` | Isolated candidate R4 (ADR-40 default profile, ADR-41 card not on file, ADR-42 line clarify & pre-selected plan, ADR-43 content guardrail, ADR-44 outage SMS consistency, ADR-45 Fibe TV app naming) |

---

## 1. Full Evaluation Runs (Active Hill-Climbing Ledger — `0` Retries)

| Iteration | UTC Timestamp | Run ID (Clickable / Resource) | Git Branch & Commit SHA | CES App ID & Version | Suite & Modality | Strict `3/3` | Majority `>=2/3` | Public (`70`) | Secret (`30`) | Official Full Score | Hill-Climb Verdict |
|---|---|---|---|---|---|:-:|:-:|:-:|:-:|:-:|---|
| **v1 Baseline** | `2026-11-03T18:16:44Z` | Academy Run [`b400c58e4cbe47e38d03ce8858b317a2`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/b400c58e4cbe47e38d03ce8858b317a2) (`sub=73fbf83dd8b943a9bf2745a165ddaaf9`, `retry_mode=null`) | `main` — code `f5c746a` (log `3ba37f6`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`c9fad922` / `git-f5c746a`) | `100` live voice sims (`1x`, unretried) | N/A (`1x` suite) | N/A (`1x` suite) | **`63/70` (`90.0%`)** | **`28/30` (`93.3%`)** | **`91/100` (`91.0%`)** | **ACTIVE BASELINE (`KEEP`, `>90%` clean pass)** |
| **v2 Candidate** | `2026-11-03T18:39:53Z` | *Skipped full run (superseded by v3)* | `fix/mig-round2` — code `96edbf4` (tip `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`a25187cf` / `git-96edbf4`) | — | — | — | — | — | — | **SUPERSEDED BY v3** |
| **v3 Candidate (R3)** | `2026-11-04T00:00:14Z` | Academy Run [`83d89a04be95420ebbf0cb7c2e13b550`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/83d89a04be95420ebbf0cb7c2e13b550) (`sub=73fbf83dd8b943a9bf2745a165ddaaf9`, `retry_mode=null`) | `fix/mig-round2` — code `3f8ddb5` (push `c4441be`, tip `1836f53`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`02cafd7f` / `git-3f8ddb5`) | `100` live voice sims (`1x`, unretried) | N/A (`1x` suite) | N/A (`1x` suite) | **`62/70` (`88.6%`)** | **`28/30` (`93.3%`)** | **`90/100` (`90.0%`)** | **DO NOT PROMOTE (`-1` vs `91/100` v1 baseline; +5 cured / -6 regressed, overlapped Day 1 Run 11)** |
| **v4 Candidate (R4)** | `2026-11-04T05:24:43Z` | Academy Run [`c8a76fcae77541a0bfc1505fe2687d5a`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/c8a76fcae77541a0bfc1505fe2687d5a) (`sub=73fbf83dd8b943a9bf2745a165ddaaf9`, `retry_mode=null`) | `fix/mig-round4` — code `31d0b36` (push `2d6c47a`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`ba90c2f2` / `git-31d0b36`) | `100` live voice sims (`1x`, unretried, solo) | N/A (`1x` suite) | N/A (`1x` suite) | **`64/70` (`91.4%`)** | **`29/30` (`96.7%`)** | **`93/100` (`93.0%`)** | **NEW BEST CLEAN FULL RUN (`+2` vs `91/100` v1 baseline, `+3` vs `90/100` v3; cured 8/9 original v1 failures; awaiting owner GO to merge to `main` & `0cf41d68`)** |

---

## 2. Targeted CES Server Smoke Runs (`Gate 1` — Diagnostic Only, Never Merged into Full Score)

| Label | UTC Timestamp | CES `evaluationRuns` Resource ID | Git Branch & Commit SHA | CES App ID & Version | Scope & Modality | Strict `3/3` | Majority `>=2/3` | Individual | Tool Errors | Notes |
|---|---|---|---|---|---|:-:|:-:|:-:|:-:|---|
| `smoke-failed7-text-r2` | `2026-11-03T18:39:32Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/5c845c1d-1d51-41d0-bbe5-587df3ce584d` | `fix/mig-round2` — code `96edbf4` (runner `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-96edbf4`) | `7` evals × `3` = `21` (`text`: `VE-16,37,39,50,56,57,66`) | **`5/7` (`71.4%`)** | **`6/7` (`85.7%`)** | `18/21` (`85.7%`) | `0` | `VE-37,39,50,56,57` all `3/3` `P P P`; `VE-66` `2/3`; `VE-16` `1/3` (DTMF) |
| `smoke-failed7-audio-r2` | `2026-11-03T18:39:53Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/3118cb57-389f-429a-bd8b-25f813c0146a` | `fix/mig-round2` — code `96edbf4` (runner `07e5d91`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-96edbf4`) | `7` evals × `3` = `21` (`audio`: `VE-16,37,39,50,56,57,66`) | **`5/7` (`71.4%`)** | **`7/7` (`100.0%`)** | `19/21` (`90.5%`) | `0` | `VE-16,37,39,50,56` all `3/3`; `VE-57,66` `2/3`; `100%` majority pass; Gate 1 cleared |
| `smoke-r3-impact18-audio` | `2026-11-03T20:18:31Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/2064091c-54a8-4fe7-813c-3c88ddd5f751` & `6bd65eed-0a42-4e6b-834a-19e9639c5654` | `fix/mig-round2` — code `3f8ddb5` (log `c4441be`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-3f8ddb5` / `02cafd7f`) | `18` evals × `3` = `54` (`audio`: `VE-16,17,18,19,34,35,37,38,39,42,43,46,50,56,57,64,65,66`) | **`15/18` (`83.3%`)** | **`15/18` (`83.3%`)** | `48/54` (`88.9%`) | `0` | 15/18 strict 3/3; all 4 R3 ADR fixes verified 3/3 (VE-37,39,50,56 P P P); VE-57,66 upgraded to 3/3; all 9 regression CUJs 3/3; VE-16,17,43 at 1/3 (0 tool errors) |
| `smoke-r4-impact20-audio` | `2026-11-04T04:23:23Z` | `projects/fde-bootcamp/locations/us/apps/8a121e2f-8601-4eac-bb77-ccf4f919374e/evaluationRuns/180e22cf-2dbb-4942-8060-3af15819cd59` & `5088d2a5-5676-4d55-9068-5da7835b6a91` | `fix/mig-round4` — code `31d0b36` (log `2d6c47a`) | `8a121e2f-8601-4eac-bb77-ccf4f919374e` (`git-31d0b36` / `ba90c2f2`) | `20` evals × `3` = `60` (`audio`: `VE-04,11,16,17,19,37,38,39,43,44,50,51,52,53,56,57,64,65,66,68`) | **`18/20` (`90.0%`)** | **`19/20` (`95.0%`)** | **`57/60` (`95.0%`)** | `0` | 18/20 strict 3/3; VE-04, 17, 43, 53, 57 all 3/3 (ADR-40, 41, 44, 45 validated); VE-66 2/3 (majority pass); VE-16 1/3 (spoken numbers vs DTMF expectation); 0 unexpected tool errors |

---

## 3. Archived Failed-Only Retries (`retry_mode=failed` — Discontinued; Excluded from Hill-Climbing)

> **Policy Note (2026-11-03T18:57Z):** Partial `retry_mode=failed` runs pre-credit prior passes and re-dial only failed scenarios. They remain recorded on the Academy leaderboard and in `history/academy/run-*.json` for audit provenance, but **we no longer run `retry_mode=failed` and never use retry scores for hill-climbing**.

| Historical Label | UTC Timestamp | Academy Run ID & Parent | Git Branch & Commit SHA | CES App ID & Version | Retried Slice | Public (`70`) | Secret (`30`) | Cumulative Leaderboard Score | Governance Status |
|---|---|---|---|---|---|:-:|:-:|:-:|---|
| `v1 Retry 1` | `2026-11-03T18:44:20Z` | [`e0d94fd317764b4a9c5601acd3821648`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/e0d94fd317764b4a9c5601acd3821648) (`prior=b400c58e...`) | `main` — code `f5c746a` (recorded `de8ff99`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`git-f5c746a`) | `9` failed calls (`91` pre-credited) | `66/70` (`94.3%`) | `29/30` (`96.7%`) | `95/100` (`95.0%`) | **ARCHIVED (Not a full run)** |
| `v1 Retry 2` | `2026-11-03T18:53:45Z` | [`ae76fff99a0341999a244697daaf3c18`](https://cxas-labs-api-6mnjcet6bq-uc.a.run.app/academy/runs/ae76fff99a0341999a244697daaf3c18) (`prior=e0d94fd3...`) | `main` — code `f5c746a` (tag `academy-best-0.97` @ `de8ff99`) | `0cf41d68-5bd0-4fda-b62f-d500cbdca886` (`git-f5c746a`) | `5` failed calls (`95` pre-credited) | `67/70` (`95.7%`) | `30/30` (`100.0%`) | `97/100` (`97.0%`) | **ARCHIVED (Not a full run)** |
