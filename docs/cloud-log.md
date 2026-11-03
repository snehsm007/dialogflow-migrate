# Cloud Activity Log

- **Target Agent**: `snehsm-FDEBootcamp-CHI-migration`
- **Target GCP Project / Location**: `projects/fde-bootcamp/locations/us`
- **CXAS Agent Academy Event**: `fde-bootcamp-chi` (track: `fde-bootcamp-chi-dfcx-cxas-agent-migration`)
- **Note**: Day 2 v1 inherits ADRs 1–28 from Day 1 `snehsm-FDEBootcamp-CHI-greenfield` @ `84ed43a`, which scored 0.89 unretried / 0.99 retry-chained on the identical 70 public scenarios.

| # | UTC Timestamp | Operation Type | Command or API Method | Target Resource | Notes |
|---|---|---|---|---|---|
| 0 | 2026-11-03T16:15:36Z | `WRITE` | `.venv/bin/cxas push --app-dir cxas_app --to projects/fde-bootcamp/locations/us/apps/0cf41d68-5bd0-4fda-b62f-d500cbdca886 --create-version --version-name git-f5c746a` | `projects/fde-bootcamp/locations/us/apps/0cf41d68-5bd0-4fda-b62f-d500cbdca886` | push commit f5c746a — outcome: OK exit=0 |
| 1 | 2026-11-03T16:19:48Z | `EVAL` | `POST /academy/events/fde-bootcamp-chi/tracks/fde-bootcamp-chi-dfcx-cxas-agent-migration/submissions` | `run_id=b400c58e4cbe47e38d03ce8858b317a2` (`submission_id=73fbf83dd8b943a9bf2745a165ddaaf9`) | Scored **`0.91` (`91/100`: `63/70` public = `90.0%`, `28/30` secret = `93.3%`, 0 retries)** at `2026-11-03T18:16:44Z` |
| 2 | 2026-11-03T18:34:45Z | `EVAL` | `POST /api/academy/runs/b400c58e4cbe47e38d03ce8858b317a2/resubmit?retry_mode=failed` | `run_id=e0d94fd317764b4a9c5601acd3821648` | Scored **`0.95` (`95/100`: `66/70` public = `94.3%`, `29/30` secret = `96.7%`)** at `2026-11-03T18:44:20Z` |
| 3 | 2026-11-03T18:46:28Z | `EVAL` | `POST /api/academy/runs/e0d94fd317764b4a9c5601acd3821648/resubmit?retry_mode=failed` | `run_id=ae76fff99a0341999a244697daaf3c18` | Scored **`0.97` (`97/100`: `67/70` public = `95.7%`, `30/30` secret = `100.0%`)** at `2026-11-03T18:53:45Z` |
