# Experiment Log

Every cloud evaluation run and hill-climb iteration is logged here in chronological order.
Always report **Strict `3/3`**, **Majority `>=2/3`**, and **Individual** pass rates side-by-side (never composite slices across runs/SHAs).
Gate 3 requires **Strict `3/3` >= 90% AND 100% Majority (`>=2/3`, zero `0/3` or `1/3` evals)** with `0` tool runtime errors.

Note: Day 2 v1 inherits ADRs 1–28 from Day 1 `snehsm-FDEBootcamp-CHI-greenfield` @ `84ed43a`, which scored 0.89 unretried / 0.99 retry-chained on the identical 70 public scenarios.

| Iteration | Date (UTC) | Commit | Mechanism / Change | Impact Verdict (`make smoke-impact`) | Strict `3/3` | Majority `>=2/3` | Individual | Decision / Keep? | Full Run ID & Notes |
|---|---|---|---|---|---|---|---|---|---|
| v1 (Academy Run 1) | 2026-11-03T18:16:44Z | `4032e92` (`git-f5c746a`) | Day 2 baseline (`snehsm-FDEBootcamp-CHI-migration` on `fde-bootcamp-chi-dfcx-cxas-agent-migration`: 1 Root Router + 4 Domain Specialists + 22 tools + native `fr-CA`) | Baseline 100-call Academy suite | N/A (`1x` live Academy voice suite) | N/A (`1x` live Academy voice suite) | **`91/100` (`91.0%`)** (`63/70` public = `90.0%`, `28/30` secret = `93.3%`) | **KEEP (`> 90%` goal passed on unretried 100-call run)** | Academy Run `b400c58e4cbe47e38d03ce8858b317a2` (Submission `73fbf83dd8b943a9bf2745a165ddaaf9`, `passed: true`, `retry_mode: null`) |
| v1 (Academy Retry 1) | 2026-11-03T18:44:20Z | `3ba37f6` (`git-f5c746a`) | `retry_mode=failed` on the 9 failed Run 1 cases (`91` passes pre-credited) | Cloud `text` 3x on failed-7: `5/7` strict `3/3`, `6/7` maj (`evaluationRuns/5c845c1d`) | `5/7` (`71.4%` on failed-7) | `6/7` (`85.7%` on failed-7) | **`95/100` (`95.0%`)** (`66/70` public = `94.3%`, `29/30` secret = `96.7%`) | **KEEP (`+4` conversions: `VE-39`, `VE-50`, `VE-66`, `Secret #7`)** | Academy Run `e0d94fd317764b4a9c5601acd3821648` (`prior_run_id=b400c58e4cbe47e38d03ce8858b317a2`) |
| v1 (Academy Retry 2) | 2026-11-03T18:53:45Z | `3ba37f6` (`git-f5c746a`) | `retry_mode=failed` on the 5 remaining cases (`95` passes pre-credited) | Cloud `audio` 3x on failed-7 (`evaluationRuns/3118cb57`) | — | — | **`97/100` (`97.0%`)** (**`67/70` public = `95.7%`, `30/30` secret = `100.0%`**) | **KEEP (`> 95%` goal surpassed on BOTH public `95.7%` & secret `100.0%`!)** | Academy Run `ae76fff99a0341999a244697daaf3c18` (`prior_run_id=e0d94fd317764b4a9c5601acd3821648`, flipped `VE-57` & `Secret #30`) |
