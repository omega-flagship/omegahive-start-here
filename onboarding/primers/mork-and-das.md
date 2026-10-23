# Primer: MORK and DAS

## What it is
- **MORK** is a high-performance AtomSpace backend from the Hyperon project, built for very large spaces and fast pattern queries. It uses its own rule language, MM2.
- **DAS** (Distributed AtomSpace) is SingularityNET's project for spreading one AtomSpace over many machines. Its pieces include remote atom databases with local caches (`RemoteAtomDB`), per-pattern access manifests (`AuthorizationManifest`), and an attention broker.

## Why it matters here
**Neither runs in this build.** Both are in the design as the path to scale and to hive-to-hive links. You need this page to plan, not to run anything.
- **MORK has never been built or run.** It was evaluated from source only, and its speed-up figure is upstream's own ([`omegahive/docs/EARLIER_EXPERIMENTS.md:82`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L82)).
- **DAS as a hard dependency is deliberately deferred.** It has no PeTTa bridge yet, and its MeTTa-side writes are unfinished. Inside one mind it would also break the single-writer rule. DAS is the model *between* hives, not inside one ([`omegahive/docs/theory/ledger-provenance-and-das.md:105-107`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L105-L107)).
- **The distributed AtomSpace is "single host by choice" today** ([`omegahive/docs/theory/hyperon-alignment-and-peer-work.md:30`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/hyperon-alignment-and-peer-work.md#L30)).

## The minimum you must know
- **Today:** each hive is self-contained. The shared spaces run in one embedded PeTTa, made durable by an append-only operations log that is replayed at start and is not yet hash-chained ([`omegahive/hive/spaces/service.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L1-L5); [`omegahive/docs/theory/ledger-provenance-and-das.md:92-93`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L92-L93)).
- **The intended storage order** is native PeTTa, then remote peers, then MORK, then an optional DAS adapter ([`omegahive/docs/theory/ledger-provenance-and-das.md:90-91`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L90-L91)).
- **The intended seam** is a `SpaceBackend` adapter with `native`, `remote`, `mork` (named stores `&mork:<swarm>`, MM2 batch revision) and `das` (an adapter to DAS's HTTP API) ([`omegahive/docs/omegadots/PLAN.md:285-291`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md#L285-L291)). **That adapter does not exist in the code yet.** Today `SpaceService` talks to PeTTa directly.
- **The road to hive-to-hive** borrows DAS patterns in six steps: chain the log, give each hive a key, shard by swarm with one writer per commons, federate beliefs with stamps, address everything by digest, and anchor to a chain when one is ready ([`omegahive/docs/theory/ledger-provenance-and-das.md:113-134`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L113-L134)).
- **Built now:** a person's representative joining a hive, and moving a mind between hives (built, not verified live). Belief queries never leave the caller's own swarm ([`omegahive/hive/core/hive.py:1637-1642`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/hive.py#L1637-L1642)).

## A tiny example
There is no MORK or DAS code to show. This is the seam a backend would sit behind: the only place the hive asks the interpreter for beliefs ([`omegahive/hive/core/hive.py:1637-1642`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/hive.py#L1637-L1642)):

```python
def query(self, agent_id, pattern):
    row = self._agent_row(agent_id)
    if not row["swarm_id"]:
        return {"results": []}
    try:
        results = self.spaces.query([row["swarm_id"]], pattern)
```

A storage swap keeps this call and its scope rule (own swarm only) and changes what `self.spaces` is.

## Common pitfalls
- **Do not draw MORK or DAS as built.** In the schematics they are dashed boxes.
- **Do not put DAS inside one mind's body.** The single-writer rule holds there ([`omegahive/docs/theory/ledger-provenance-and-das.md:106-107`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L106-L107)).
- **Keep stamps when you federate.** Cross-hive revision is only honest if bundles carry evidence stamps ([`omegahive/docs/theory/ledger-provenance-and-das.md:126-127`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L126-L127)).
- **One interpreter per process** today. Scaling out means sharding by swarm, not a second thread ([`omegahive/docs/omegadots/PLAN.md:280-282`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md#L280-L282)).
- **FEATURES overstates query scope.** Feature CR3 says a query searches "the swarm commons and the federation" ([`omegahive/docs/FEATURES.md:174`](https://github.com/PhysixSNET/omegahive/blob/main/docs/FEATURES.md#L174)). The code searches only the caller's own swarm (see the example).

## Upstream
- **DAS:** <https://github.com/singnet/das>
- **MORK:** the MORK project of the Hyperon ecosystem (TrueAGI). Repository: <https://github.com/trueagi-io/MORK>.

## Read next
- [`omegahive-schematics/04-knowledge/04-federation.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/04-federation.md): what is built and the intended shard-by-swarm shape.
- [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md), "Intended shape and upgrade path".
- [`omegahive/docs/theory/ledger-provenance-and-das.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md): the full design.
