# Primer: PeTTa on SWI-Prolog

## What it is
**PeTTa** is a MeTTa implementation that compiles MeTTa to Prolog and runs it on **SWI-Prolog**. **janus** is SWI-Prolog's two-way bridge to Python: Prolog can call Python (`py-call` in MeTTa) and Python can drive Prolog.

## Why it is used here
Every native mind and the hive's shared spaces run on PeTTa. The plan records why: the older Hyperon runtime was too slow for this use, and the ecosystem has moved to PeTTa ([`omegahive/docs/omegadots/PLAN.md:90-93`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md#L90-L93)). It runs two ways:
- **One process per mind.** The supervisor starts `sh <PETTA_PATH>/run.sh <workspace>/run.metta --silent` ([`omegahive/hive/supervisor/workspace.py:109-114`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L109-L114)). Here Prolog calls out to Python helpers.
- **Embedded in the hive.** The hive's Python imports PeTTa's Python package and loads `lib_hive.metta` into it ([`omegahive/hive/spaces/service.py:79-86`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L79-L86)). Here Python calls into Prolog.

## The minimum you must know
**The toolchain is pinned. Use exactly these** ([`omegahive/scripts/dev/setup_petta_env.sh:4-8`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L4-L8)):

| Piece | Pin |
|---|---|
| Python | 3.12 |
| SWI-Prolog | 10.1.14, built from source against that same Python |
| PeTTa | commit `ae66fa8` |
| janus-swi | 1.5.3 |

- **Build it with the script:** `scripts/dev/setup_petta_env.sh`. On a development machine it puts SWI-Prolog in a private prefix (default `swipl-patched` in your home folder), so it never shadows a system `swipl` ([`omegahive/scripts/dev/setup_petta_env.sh:10-13`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L10-L13)). The Linux server install, `deploy/setup_runtime.sh`, installs system-wide instead ([`omegahive/deploy/setup_runtime.sh:3-4`](https://github.com/PhysixSNET/omegahive/blob/main/deploy/setup_runtime.sh#L3-L4)).
- **Then set two things** before any test: the prefix's `bin` first on `PATH`, and `PETTA_PATH` to your PeTTa checkout ([`omegahive/scripts/dev/setup_petta_env.sh:19-21`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L19-L21)).
- **The pins live in two places:** this script and `deploy/setup_runtime.sh`. Change both together ([`omegahive/scripts/dev/setup_petta_env.sh:4`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L4)).

## A tiny example
The hive's embedded interpreter, start to finish ([`omegahive/hive/spaces/service.py:79-86, 99-102`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L79-L86)):

```python
sys.path.insert(0, str(pathlib.Path(self.petta_path) / "python"))
from petta import PeTTa
metta = PeTTa(verbose=False, petta_path=self.petta_path)
metta.load_metta_file(str(LIB_HIVE))
...
def run(self, code, timeout=30):
    future: Future = Future()
    self._jobs.put((code, future))
    return future.result(timeout)
```

Every call is queued to one worker thread, because janus binds the interpreter to the first thread that calls it ([`omegahive/hive/spaces/service.py:52-57`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L52-L57)).

## Common pitfalls
- **A stock SWI-Prolog is not enough.** A packaged (for example Homebrew) `swipl` loads, but its Prolog-to-Python bridge fails with `janus:py_call/4` not found. Then every hive test errors with "PeTTa failed to start" ([`omegahive/scripts/dev/setup_petta_env.sh:11-13`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L11-L13)). Check which `swipl` is first on your `PATH`.
- **Without PeTTa, tests error rather than skip.** A red hive suite on a fresh machine is usually the toolchain, not the code ([`omegahive/STATUS.md:20-22`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L20-L22)).
- **Do not drift the PeTTa pin.** Truth-function results and the browser parity run were measured on `ae66fa8` ([`omegahive/docs/reasoning-deviations.md:13`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L13); [`omegahive/docs/EARLIER_EXPERIMENTS.md:27`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L27)).
- **One thread only** for the embedded interpreter. A second thread deadlocks ([`omegahive/hive/spaces/service.py:55-56`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L55-L56)).
- **A mind's entry file fetches the core by `git-import!`.** The workspace links `repos/OmegaClaw-Core` to the shared checkout so the import finds it there ([`omegahive/hive/supervisor/workspace.py:3-6, 24-28`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L3-L6)).
- **`--silent`** stops PeTTa echoing every compiled clause. The mind's own output still reaches `agent.log` ([`omegahive/hive/supervisor/workspace.py:113`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L113)).

## Upstream
- **PeTTa:** <https://github.com/trueagi-io/PeTTa>
- **SWI-Prolog,** source used here: <https://github.com/SWI-Prolog/swipl-devel> (tag `V10.1.14`)
- **janus-swi:** the SWI-Prolog Python bridge, published as the `janus-swi` Python package.

## Read next
- [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md), diagram 3, "PeTTa on SWI-Prolog, two ways".
- [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md): how the supervisor starts a mind.
- [`omegahive-schematics/03-minds/02-supervisor-drivers-sandbox.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/02-supervisor-drivers-sandbox.md): what that process may reach.
