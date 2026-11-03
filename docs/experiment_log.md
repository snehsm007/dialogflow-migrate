# Experiment Log

Every cloud evaluation run and hill-climb iteration is logged here in chronological order.
Always report **Strict `3/3`**, **Majority `>=2/3`**, and **Individual** pass rates side-by-side (never composite slices across runs/SHAs).
Gate 3 requires **Strict `3/3` >= 90% AND 100% Majority (`>=2/3`, zero `0/3` or `1/3` evals)** with `0` tool runtime errors.

Note: Day 2 v1 inherits ADRs 1–28 from Day 1 `snehsm-FDEBootcamp-CHI-greenfield` @ `84ed43a`, which scored 0.89 unretried / 0.99 retry-chained on the identical 70 public scenarios.

| Iteration | Date (UTC) | Commit | Mechanism / Change | Impact Verdict (`make smoke-impact`) | Strict `3/3` | Majority `>=2/3` | Individual | Decision / Keep? | Full Run ID & Notes |
|---|---|---|---|---|---|---|---|---|---|
