# SINDIE ion-optics runs

The meeting point between the IBSimu models of the SINDIE source and beamline (in
[PhD-Thesis](https://github.com/joshbird98/PhD-Thesis), `analysis/ion_optics`) and the machine that
runs the large sweeps (ibc-compute02). Sweeps are queued here, the runner on the cluster takes them,
runs them and pushes the numbers back; the thesis figures and analysis read them from here. Set-up
and the sweep-file format: `analysis/ion_optics/cluster/README.md` and `cluster/runner.py` in
PhD-Thesis.

| Folder | What is in it |
| --- | --- |
| `queue/` | sweep files waiting to run (the only folder edited by hand) |
| `running/`, `done/`, `failed/` | sweep files as the runner takes and finishes them |
| `rejected/` | sweep files that failed validation, with the reason |
| `results/<sweep>/` | `sweep.json` (what was run, thesis commit, host), `status.json` (progress), `cases.jsonl` (one line per case: overrides, status, run time, metrics) and `files/<case id>/` (outputs the sweep asked to publish, xz-compressed) |
| `runner/` | `daemon_<host>.json`, written each time the runner starts |
| `selftest/` | the numbers from the set-up self-test |
| `ibsimu/` | the IBSimu source the models are built against |

Reading a sweep:

```python
import json
import pandas as pd

rows = [json.loads(line) for line in open("results/s001_example/cases.jsonl")]
df = pd.json_normalize([r for r in rows if r["status"] == "ok"])   # columns like metrics.cs_spot.r95_mm
```

A case id is the first ten hex digits of the SHA-1 of its overrides (sorted JSON), so the same case
in a later sweep has the same id. A sweep that is stopped and queued again skips the cases it has
already finished.
