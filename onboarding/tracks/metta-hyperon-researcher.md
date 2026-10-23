# Track: MeTTa and Hyperon researcher

**For you if** you know MeTTa, AtomSpace, NAL, PLN or NARS and want to see how this build uses them: in each mind's own spaces, in a swarm's shared commons, and in the reasoning skills.

**Total time:** about 8.5 hours.

**Before you start:** have a toolchain that runs PeTTa (the `omegahive` [README](https://github.com/PhysixSNET/omegahive/blob/main/README.md) has the exact steps). Without a working PeTTa most hive tests error rather than skip ([STATUS.md:22](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)).

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | Hive, mind, swarm, commons and module, and how they relate. |
| 2 | 40 min | Read the primers [MeTTa and AtomSpace](../primers/metta-and-atomspace.md) and [PeTTa and SWI-Prolog](../primers/petta-and-swi-prolog.md), and skim the [glossary](../GLOSSARY.md). | Terms that mean something narrower here than in Hyperon generally, and how PeTTa runs MeTTa on SWI-Prolog. |
| 3 | 40 min | Read the schematics page [MeTTa and AtomSpace](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md). | Which spaces a mind owns, which the hive owns, and where PeTTa runs. |
| 4 | 30 min | Read the component cards [hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md) and [mind-memory](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-memory.md). | What each must guarantee, and where long-term recall sits beside the AtomSpace. |
| 5 | 45 min | Walk the code tour [02: a belief from mind to commons](https://github.com/PhysixSNET/omegahive/blob/main/.tours/02-a-belief-from-mind-to-commons.tour). | The path a belief takes, and where its evidence stamp and truth value are set. |
| 6 | 45 min | Read the primer [Truth values, NAL and PLN](../primers/truth-values-nal-pln.md), then [Beliefs: publish, query and revise](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md). | Disjoint-evidence revision and the operations log replayed at boot ([STATUS.md:32](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 7 | 60 min | Read the primer [Attention and ECAN](../primers/attention-ecan.md), then [Reasoning: NAL, PLN, NARS and attention](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/03-reasoning.md) and the card [reasoning](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/reasoning.md). | What is a callable skill today and what is held. Automatic reasoning from the mind loop is deliberately not wired in this build ([STATUS.md:49](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 8 | 30 min | Read [reasoning-deviations.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md). | Each place a truth function departs from its reference ([STATUS.md:50](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 9 | 45 min | Read the primer [The OmegaClaw mind loop](../primers/the-omegaclaw-mind-loop.md), then [Mind runtime and lifecycle](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md) and the card [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md). | Where in the mind loop a skill call happens, and so where reasoning could later be wired. |
| 10 | 60 min | Do the exercise [hello-module](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-module) in the [disposable local hive](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md). | How a module registers a skill that a mind can call. |
| 11 | 60 min | Read the primer [MORK and DAS](../primers/mork-and-das.md), then [Federation: hives as nodes](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/04-federation.md) and [Intended governance](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/05-intended-governance.md). | Which parts of the deeper legacy V2 mind design are mapped onto this build, and which are only intended (dashed). |

## Checkpoint

**You can now** explain how a belief is created in one mind, stamped, published to a swarm commons, revised against other evidence and queried back, and say which reasoning pieces are callable and which are held.

**Prove it:** in the sandbox, extend your hello-module so a mind publishes one invented belief with a truth value to a scratch swarm's commons, then publish a second belief with disjoint evidence and query the revised result. Write down the truth value you expected before you query, and compare.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Commons store** ([hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md)): keep one MeTTa space per swarm on PeTTa, or swap in your own AtomSpace backend (for example MORK)? What must the replacement keep stable for the beliefs API?
2. **Revision rule:** is disjoint-evidence revision the rule you want for a shared commons, or do you need a different merge policy?
3. **Reasoning** ([reasoning](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/reasoning.md)): keep the NAL and PLN libraries with their documented deviations, or swap in your reference implementations as a module?
4. **Wiring:** should reasoning stay a skill the mind chooses to call, or be activated from the mind loop? What evidence would you need first?
5. **Attention:** the current classifier is heuristic with ECAN-inspired naming ([STATUS.md:51](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). Keep, or replace with full ECAN?
6. **Long-term recall** ([mind-memory](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-memory.md)): keep the vector store beside the AtomSpace, or move recall into the AtomSpace itself?
