# Primer: the programs contract

## What it is
An **app** (the contract calls it a **program**) is a Python module that tells the hive what a piece of work *means*. It returns that meaning as a **work graph**: plain JSON items, links and groups. The **host** (the hive server and UI) draws it, checks permissions and runs actions. The contract is the boundary between the two ([`omegahive/hive/PROGRAMS.md:1-12`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L1-L12)).

## Why it is used here
It is how every app plugs in: Tools, Planner, Library, Studio and the closed apps. It is plain JSON and does not depend on MeTTa, a truth calculus or any earlier Omega design ([`omegahive/hive/PROGRAMS.md:11-12`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L11-L12)). So you can swap an app for your own without touching the hive, as long as you speak the contract.

## The minimum you must know
- **Three functions** ([`omegahive/hive/PROGRAMS.md:51-55`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L51-L55)):
  - `describe()`: once at load. Declares the app's kinds, relations and actions.
  - `view(ctx, focus, stage)`: each time a person looks. Returns a full work-graph snapshot. `stage` is `unfold`, `map`, `compare` or `detail`.
  - `act(ctx, action, items, params)`: when a person picks an action. The host checks permission first.
- **Files:** a folder with `plugin.json` (id, contract version, module, capabilities) and the module.
- **Version:** v0.1 is frozen; changes come as v0.2 and later ([`omegahive/hive/PROGRAMS.md:8-10`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L8-L10)). The hive also accepts some additive 0.2 fields on `act` ([`omegahive/docs/COMPATIBILITY.md:10`](https://github.com/PhysixSNET/omegahive/blob/main/docs/COMPATIBILITY.md#L10)).
- **Validation, by server and checker alike:** ids unique and stable, links and groups point inside the graph, kinds and relations come from `describe()`, at most 400 items and 1200 links. A bigger view is refused, never cut short ([`omegahive/hive/PROGRAMS.md:115-121`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L115-L121)).
- **Uncertainty is labelled with its method** (`nal`, `pln`, `qualitative` or another). The host never converts one into another. Missing means unassessed, not zero ([`omegahive/hive/PROGRAMS.md:123-131`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L123-L131)).
- **The checker needs no hive:** `python -m hive.programs_check <dir>` loads the app, views every stage, checks ids are stable, and exits 0 when compatible ([`omegahive/hive/programs_check.py:1-20`](https://github.com/PhysixSNET/omegahive/blob/main/hive/programs_check.py#L1-L20)).
- **Apps run inside the hive process** today. They are imported, not separate services; out-of-process programs are a later version ([`omegahive/hive/PROGRAMS.md:42`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L42)).

## A tiny example
The public fixture app's manifest ([`omegahive/hive/plugins/contract_fixture/plugin.json:1-10`](https://github.com/PhysixSNET/omegahive/blob/main/hive/plugins/contract_fixture/plugin.json#L1-L10)) and the start of its `describe()` ([`omegahive/hive/plugins/contract_fixture/program.py:18-35`](https://github.com/PhysixSNET/omegahive/blob/main/hive/plugins/contract_fixture/program.py#L18-L35)):

```json
{ "id": "contract-fixture", "name": "Contract fixture", "version": "0.1.0", "contract": "0.1",
  "module": "program.py", "capabilities": ["goals:write"], "icon": "flask" }
```

```python
def describe():
    return {
        "contract": CONTRACT,
        "kinds": [
            {"id": "question", "label": "Question", "role": "question"},
            {"id": "evidence", "label": "Evidence", "role": "evidence"},
            ...
        ],
        "relations": [
            {"id": "supports", "label": "supports", "polarity": "support"},
            {"id": "contradicts", "label": "contradicts", "polarity": "oppose"},
            ...
```

(Both shortened: the manifest's `description` and the lines marked `...` are left out.) Copy this folder to start a new app, then run the checker on it.

## Common pitfalls
- **Ids are forever.** An item id must stay stable across revisions and never be reused for something else ([`omegahive/hive/PROGRAMS.md:93`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L93)).
- **References are not access.** The host shows a `url` or `local_ref` and fetches nothing by itself ([`omegahive/hive/PROGRAMS.md:137-139`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L137-L139)).
- **`--allow-mutation` changes data.** Point it only at a disposable fixture, never at real records ([`omegahive/hive/programs_check.py:14-16`](https://github.com/PhysixSNET/omegahive/blob/main/hive/programs_check.py#L14-L16)).
- **A stale pin stops the app loading.** With a release pin set (`HIVE_APP_PINS`), the app loads only from exactly that folder and digest; a refused app's code never runs ([`omegahive/hive/core/programs.py:593-620`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/programs.py#L593-L620)). Update the pin with each release.
- **Deploying an app with its swarm is confusing today.** The pin, the swarm, the app home and the grants are set in separate places with no guided step ([`omegahive/STATUS.md:67`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L67)).
- **Passing the checker is not live readiness.** Backend contract readiness is not live app readiness ([`omegahive/hive/PROGRAMS.md:41`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L41)).

## Upstream
This contract is OmegaHive's own. It has no upstream project.

## Read next
- [`omegahive-schematics/06-apps/01-programs-contract.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/01-programs-contract.md): the three calls, who may act, and versions.
- [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md): discovery, pins, homes, activations and grants.
- [`omegahive-schematics/06-apps/03-connect-a-new-app.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/03-connect-a-new-app.md): a worked example, step by step.
- [`omegahive/hive/PROGRAMS.md`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md): the full contract, including the app frame and the Scientist route.
