# Lineage and acknowledgements

OmegaHive stands on other people's work. We thank SingularityNET, TrueAGI and the OpenCog Hyperon community for MeTTa, the AtomSpace, PLN, ECAN, MORK, DAS and the research behind them. We thank the NARS community for Non-Axiomatic Logic and its reference systems. We thank the OmegaClaw authors, whose runtime every native mind still runs on. And we thank the many open-source projects listed below, from SWI-Prolog to the web and channel libraries.

This page is the one place that records where each upstream piece comes from, how we use it, its licence and the papers behind it. Other pages link here rather than repeat it.

## How to read the tables

- **How we use it** is one of: *vendored copy* (a copy of the upstream source lives in our tree), *pinned dependency* (installed at an exact version or commit), *dependency, not pinned* (installed by name only), *loaded at run time* (fetched or imported when a mind or the hive starts) or *design inspiration only* (no upstream code here).
- **V2 map** gives the verdict from the OmegaV2 prior-art map of 2026-07-21: **USE**, **ADAPT** or **REFERENCE**. Those verdicts were made for the V2 body (`omegav2`), not for the current hive.
- **Licence:** a plain licence was read from a `LICENSE`, `NOTICE`, lock file or installed package metadata. *(notes)* means it was recorded from public repository metadata in the team's research notes; check the upstream `LICENSE` before relying on it. *To be confirmed* means we found no record.
- **Links** were checked against files in these repositories, the pinned setup scripts and the team's notes. Anything we could not check says *(link to be confirmed)*.
- **Authors** are public credit only: the organisation, or the author named in the upstream notice or paper.
- Component cards live in [`omegahive-schematics/components/`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/README.md).

## Contents

1. [MeTTa and Hyperon](#metta-and-hyperon)
2. [PeTTa and SWI-Prolog](#petta-and-swi-prolog)
3. [NAL, NARS and ONA](#nal-nars-and-ona)
4. [PLN](#pln)
5. [Attention (ECAN)](#attention-ecan)
6. [Motivation and emotion](#motivation-and-emotion)
7. [MORK and DAS](#mork-and-das)
8. [ASI:Chain](#asi-chain)
9. [The OmegaClaw Core runtime](#omegaclaw-core)
10. [LLM organ](#llm-organ)
11. [Memory (ChromaDB)](#memory-chromadb)
12. [Predictive coding (FabricPC)](#predictive-coding)
13. [MCP and agent interop](#mcp-and-agent-interop)
14. [The web stack](#web-stack)
15. [Channels](#channels)
16. [Documents](#documents)
17. [Tooling](#tooling)
18. [Papers by topic](#papers-by-topic)

<a id="metta-and-hyperon"></a>
## MeTTa and Hyperon

MeTTa is the language minds think in, and the AtomSpace is where their knowledge lives. This build runs MeTTa on PeTTa (next section), not on the Rust reference implementation.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| hyperon-experimental (MeTTa reference implementation) | <https://github.com/trueagi-io/hyperon-experimental> | TrueAGI | Design inspiration only: the language specification, not the runtime. V2 map: REFERENCE | MIT *(notes)* | [`docs/omegaclaw-core.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegaclaw-core.md); card [hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md) | MeTTa specification; Meta-MeTTa |
| MeTTa specification | <https://trueagi-io.github.io/hyperon-experimental/metta/> | TrueAGI | Design inspiration only | To be confirmed | [`docs/omegaevolve/HYPERON_THEORY_REVIEW.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegaevolve/HYPERON_THEORY_REVIEW.md) | |
| MeTTaScript (`@mettascript/core`, `@mettascript/hyperon`) | (link to be confirmed) | To be confirmed | Pinned dependency, 3.4.0: runs NAL, PLN and the commons in the browser | MIT | [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json), [`hive/ui/src/lib/mindSpace/core.ts`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/src/lib/mindSpace/core.ts); cards [ui-shell](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ui-shell.md), [reasoning](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/reasoning.md) | |
| metta-wam (MeTTaLog) | <https://github.com/trueagi-io/metta-wam> | TrueAGI | Design inspiration only: a comparison point. V2 map: REFERENCE | To be confirmed (the notes disagree) | [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md) | |
| metta-morph | <https://github.com/trueagi-io/metta-morph> | TrueAGI | Design inspiration only. V2 map: REFERENCE | To be confirmed | as above | |
| chaining (controlled chainers) | <https://github.com/trueagi-io/chaining> | TrueAGI | Design inspiration only. V2 map: REFERENCE (the stdlib chaining primitives were ADAPT) | GPL-3.0 *(notes)* | as above | |
| hyperon-miner (pattern miner) | <https://github.com/trueagi-io/hyperon-miner> | TrueAGI | Design inspiration only. V2 map: REFERENCE | AGPL-3.0 *(notes)* | as above | Patterns of Cognition |
| MOSES (program learning) | <https://github.com/opencog/moses> | OpenCog | Design inspiration only: evaluated and declined for V2 | To be confirmed | [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md) | |
| Hyperon architecture and PRIMUS | <https://hyperon.dev/primer#architecture> | SingularityNET, TrueAGI | Design inspiration only | n/a | [`docs/theory/hyperon-alignment-and-peer-work.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/hyperon-alignment-and-peer-work.md) | OpenCog Hyperon; Reflective metagraph rewriting; General theory of general intelligence; PRIMUS world modeling |

<a id="petta-and-swi-prolog"></a>
## PeTTa and SWI-Prolog

PeTTa runs MeTTa on SWI-Prolog. Every native mind and the hive's shared spaces run on it. The pins live in two scripts that must change together. Primer: [PeTTa and SWI-Prolog](onboarding/primers/petta-and-swi-prolog.md).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| PeTTa | <https://github.com/trueagi-io/PeTTa> | Patrick Hammer (TrueAGI) | Pinned dependency at `ae66fa8`. Vendored copy with patches in `omegav2/deps/PeTTa`. V2 map: USE | MIT (Copyright 2025 Patrick Hammer) | [`scripts/dev/setup_petta_env.sh`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh), [`deploy/setup_runtime.sh`](https://github.com/PhysixSNET/omegahive/blob/main/deploy/setup_runtime.sh), [`omegav2/deps/PeTTa`](https://github.com/PhysixSNET/omegav2/tree/main/deps/PeTTa), [`omega-tools/foundations/LICENSE.PeTTa`](https://github.com/PhysixSNET/omega-tools/blob/main/foundations/LICENSE.PeTTa); cards [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md), [hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md), [supervisor-and-drivers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/supervisor-and-drivers.md) | PeTTa announcement |
| SWI-Prolog (swipl-devel) | <https://github.com/SWI-Prolog/swipl-devel> | SWI-Prolog project | Pinned dependency: built from tag `V10.1.14` against Python 3.12 | To be confirmed | [`scripts/dev/setup_petta_env.sh`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh), [`deploy/setup_runtime.sh`](https://github.com/PhysixSNET/omegahive/blob/main/deploy/setup_runtime.sh) | |
| janus-swi (Python and Prolog bridge) | <https://github.com/SWI-Prolog/packages-swipy> | Jan Wielemaker (SWI-Prolog) | Pinned dependency, 1.5.3 | BSD-2-Clause | as above | |

The `Dockerfile` clones `patham9/PeTTa` at `main` instead of the pinned `trueagi-io/PeTTa` commit. Treat the setup scripts as the source of truth.

<a id="nal-nars-and-ona"></a>
## NAL, NARS and ONA

Non-Axiomatic Logic gives evidence-based truth values `(stv f c)`. The commons revises disjoint evidence by the NAL revision rule. Where our library differs from the references is recorded in [`docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md). Primer: [truth values, NAL and PLN](onboarding/primers/truth-values-nal-pln.md).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| NAL library (OmegaClaw lineage) | via [OmegaClaw Core](#omegaclaw-core) | Patrick Hammer | Vendored copy: `lib_nal.metta`; also `omegav2/deps/NAL` | MIT (Copyright 2026 Patrick Hammer) | [`lib_nal.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta), [`hive/spaces/lib_hive.metta`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta), [`omegav2/deps/NAL`](https://github.com/PhysixSNET/omegav2/tree/main/deps/NAL); cards [reasoning](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/reasoning.md), [hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md) | NAL Specification; NARS 4.1 |
| PeTTa `lib_nars` | <https://github.com/trueagi-io/PeTTa> | Patrick Hammer | Loaded at run time from the PeTTa library | MIT | [`lib_omegaclaw_core.metta:14`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta#L14) | |
| metta-nars | <https://github.com/patham9/metta-nars> | Patrick Hammer | Design inspiration only. V2 map: ADAPT (weak end) | MIT *(notes)* | [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md) | |
| ONA (OpenNARS for Applications) | <https://github.com/opennars/OpenNARS-for-Applications> | OpenNARS project | Design inspiration only: a reference for the truth functions (`Truth.c`); not installed. V2 map: REFERENCE | MIT *(notes)* | [`docs/reference-lib-ona.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-lib-ona.md), [`docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) | (ONA paper, link to be confirmed) |
| OpenNARS (Java) | <https://github.com/opennars/opennars> | OpenNARS project | Design inspiration only: a reference in the NAL audit | To be confirmed | [`docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) | |
| NACE (Non-Axiomatic Causal Explorer) | <https://github.com/patham9/NACE> | Patrick Hammer | Design inspiration only: evaluated and declined for V2 | MIT *(notes)* | [`docs/EARLIER_EXPERIMENTS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md), [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md) | |

<a id="pln"></a>
## PLN

Probabilistic Logic Networks. `lib_pln.metta` stays as it is in this release by the owner's ruling; any change to its truth semantics goes to the domain author first.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| PLN (MeTTa-native, v0.9) | <https://github.com/trueagi-io/PLN> | TrueAGI | Vendored copy: `lib_pln.metta` is a fork whose truth block equals commit `4405956`; `omegav2/deps/PLN` holds v0.9. V2 map: USE | MIT (Copyright 2025 NARTECH) | [`lib_pln.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_pln.metta), [`docs/reference-lib-pln.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-lib-pln.md), [`omegav2/deps/PLN`](https://github.com/PhysixSNET/omegav2/tree/main/deps/PLN); card [reasoning](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/reasoning.md) | PLN book |
| hyperon-pln (dependent-type PLN) | <https://github.com/trueagi-io/hyperon-pln> | TrueAGI | Design inspiration only: the source of the formulas, cited in `lib_pln.metta`. V2 map: REFERENCE | AGPL-3.0 *(notes)* | [`lib_pln.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_pln.metta) | PLN book |
| OpenCog PLN (classic) | <https://github.com/opencog/pln> | OpenCog | Design inspiration only: a reference in the PLN audit | To be confirmed | [`docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md), [`docs/reference-lib-pln.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-lib-pln.md) | PLN book |

<a id="attention-ecan"></a>
## Attention (ECAN)

Economic attention allocation decides what a mind keeps in focus. This build has its own small "ECAN-lite" organ; no upstream ECAN code is loaded. Primer: [attention and ECAN](onboarding/primers/attention-ecan.md).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| metta-attention (ECAN in MeTTa) | <https://github.com/iCog-Labs-Dev/metta-attention> | iCog Labs | Design inspiration only here; the plan names it as the swap for ECAN-lite. V2 map: ADAPT | None declared *(notes)* | [`lib_omegaclaw_attention.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_attention.metta), [`docs/omegadots/PLAN.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md), [`omegav2/docs/whitepaper/D18_attention_economics.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D18_attention_economics.md); cards [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md), [goals-and-motivations](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/goals-and-motivations.md) | ECAN wiki; Nonlinear-dynamical attention allocation; Patterns of Cognition |
| singnet/attention (C++ ECAN) | <https://github.com/singnet/attention> | SingularityNET | Design inspiration only. V2 map: REFERENCE | To be confirmed | [`omegav2/docs/whitepaper/D18_attention_economics.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D18_attention_economics.md) | |
| CAIRN (ECAN metrics and dashboard) | <https://github.com/trueagi-io/CAIRN> | TrueAGI | Design inspiration only | None declared *(notes)* | [`docs/omegadots/research/community-drift-viz-2026-10.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/research/community-drift-viz-2026-10.md) | |
| DAS attention broker | see [MORK and DAS](#mork-and-das) | SingularityNET | Design inspiration only | To be confirmed | [`docs/omegadots/PLAN.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md) | |

<a id="motivation-and-emotion"></a>
## Motivation and emotion

Motivations and tasks in the hive are host-side records today. The Hyperon motivation line informs the design; no upstream motivation code runs here.

> MetaMo (also written MeTTaMo) is a motivation system. Do not confuse it with **metta-motto**, the LLM organ listed under [LLM organ](#llm-organ).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| MetaMo (also written MeTTaMo, MettaMo) | <https://github.com/iCog-Labs-Dev/MetaMo> | iCog Labs | Design inspiration only: the framing of motivation as a typed, auditable object was accepted for V2; the code was declined. V2 map: REFERENCE | MIT *(notes)* | [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md), [`omega-tools/modules/tools_goal_compass/src/law.metta`](https://github.com/PhysixSNET/omega-tools/blob/main/modules/tools_goal_compass/src/law.metta); card [goals-and-motivations](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/goals-and-motivations.md) | MetaMo; From MetaMo to Open-Ended OpenPsi |
| MetaMo-Python | (link to be confirmed) | To be confirmed | Design inspiration only. V2 map: REFERENCE | MIT *(notes)* | as above | as above |
| MetaMo-Prototype | <https://github.com/singnet/MetaMo-Prototype> | SingularityNET | Design inspiration only | None declared *(notes)* | as above | as above |
| hyperon-openpsi (motivation, emotion as modulators) | <https://github.com/iCog-Labs-Dev/hyperon-openpsi> | iCog Labs | Design inspiration only here. V2 map: ADAPT (motivation and affect) | MIT in its README, no `LICENSE` file *(notes)* | [`docs/theory/hyperon-alignment-and-peer-work.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/hyperon-alignment-and-peer-work.md); card [goals-and-motivations](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/goals-and-motivations.md) | From MetaMo to Open-Ended OpenPsi |
| PeTTa-OpenPSI | (link to be confirmed) | To be confirmed | Design inspiration only. V2 map: REFERENCE | MIT *(notes)* | none | |
| OpenPsi (original, Atomese and Scheme) | <https://github.com/opencog/opencog> (`opencog/openpsi`) | OpenCog | Design inspiration only: superseded by hyperon-openpsi. V2 map: REFERENCE | To be confirmed (the notes record AGPL or Apache) | [`docs/theory/hyperon-alignment-and-peer-work.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/hyperon-alignment-and-peer-work.md) | |

<a id="mork-and-das"></a>
## MORK and DAS

Neither runs in this build. Both are the intended path to scale and to hive-to-hive links. Primer: [MORK and DAS](onboarding/primers/mork-and-das.md).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| MORK (MeTTa Optimal Reduction Kernel) | <https://github.com/trueagi-io/MORK> | TrueAGI | Design inspiration only: evaluated from source, never built here. V2 map: ADAPT (kernel only) | None declared *(notes)* | [`docs/EARLIER_EXPERIMENTS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md), [`omegav2/docs/dossiers/OMEGAV2_D34_PETTA_MORK_ATOMSPACE_AND_JETTA_SUBSTRATES_2026-08-07.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/dossiers/OMEGAV2_D34_PETTA_MORK_ATOMSPACE_AND_JETTA_SUBSTRATES_2026-08-07.md); cards [hive-spaces](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md), [federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md) | Meta-MeTTa |
| PathMap (MORK's trie) | <https://github.com/Adam-Vandervorst/PathMap> | Adam Vandervorst | Design inspiration only | MIT *(notes)* | none | |
| mork_ffi (PeTTa MORK spaces) | <https://github.com/patham9/mork_ffi> | Patrick Hammer | Design inspiration only: PeTTa's optional `build.sh`, not run here | To be confirmed | none | |
| DAS (Distributed AtomSpace) | <https://github.com/singnet/das> | SingularityNET | Design inspiration only: the model for hive-to-hive links. V2 map: ADAPT (local special-space path only) | To be confirmed | [`docs/theory/ledger-provenance-and-das.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md); card [federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md) | |

<a id="asi-chain"></a>
## ASI:Chain

ASI:Chain is a later anchor for signed chain heads, never a source of authority. Nothing in this build talks to it.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| ASI:Chain | <https://github.com/asi-alliance/asi-chain> | ASI Alliance | Design inspiration only | To be confirmed | [`docs/theory/ledger-provenance-and-das.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md), [`omegav2/docs/dossiers/OMEGAV2_D24_ASI_CHAIN_AND_CRYPTOGRAPHIC_SOVEREIGNTY_2026-08-07.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/dossiers/OMEGAV2_D24_ASI_CHAIN_AND_CRYPTOGRAPHIC_SOVEREIGNTY_2026-08-07.md); card [federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md) | ASI:Chain devnet announcement |

<a id="omegaclaw-core"></a>
## The OmegaClaw Core runtime

The program each native mind runs: a MeTTa agent loop with skills, memory and modules. It is vendored here and credited in [`omegahive/NOTICE`](https://github.com/PhysixSNET/omegahive/blob/main/NOTICE). Primer: [the OmegaClaw mind loop](onboarding/primers/the-omegaclaw-mind-loop.md).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| OmegaClaw Core | <https://github.com/asi-alliance/OmegaClaw-Core> (now redirects to `singnet/Omega`) | Patrick Hammer; ASI Alliance | Vendored copy: `src/`, `modules/`, `channels/`, `lib_*.metta`, `run.metta`. Smoke tests still `git-import!` the upstream URL. V2 map: ADAPT | MIT (Copyright 2026 Patrick Hammer) | [`NOTICE`](https://github.com/PhysixSNET/omegahive/blob/main/NOTICE), [`docs/omegaclaw-core.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegaclaw-core.md), [`lib_omegaclaw.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw.metta); cards [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md), [modules](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/modules.md), [channels](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/channels.md) | (OmegaClaw AGI-26 paper, link to be confirmed) |
| OmegaClaw Core fork used by `run.metta` | <https://github.com/physixCN/OmegaClaw-Core> | the owner's organisation | Loaded at run time by the standalone `run.metta` | MIT (the OmegaClaw Core notice) | [`run.metta`](https://github.com/PhysixSNET/omegahive/blob/main/run.metta) | |
| mettaclaw (ancestor of OmegaClaw) | <https://github.com/patham9/mettaclaw> | Patrick Hammer | Design inspiration only; its memory organ was ADAPT in the V2 map | MIT *(notes)* | [`omegav2/NOTICE`](https://github.com/PhysixSNET/omegav2/blob/main/NOTICE) | |
| Iter (the loop behind Iter workers) | <https://github.com/patham9/iter> | Patrick Hammer | Loaded at run time: cloned once into the hive's data folder when an Iter mind first needs it, not pinned | To be confirmed | [`hive/supervisor/workspace.py:31`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L31); card [supervisor-and-drivers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/supervisor-and-drivers.md) | |

<a id="llm-organ"></a>
## LLM organ

The language model is one organ, not the control plane. In the hive every model call goes through the gateway.

> metta-motto is the LLM organ. Do not confuse it with **MetaMo** (MeTTaMo), the motivation system listed under [Motivation and emotion](#motivation-and-emotion).

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| metta-motto (LLM output as inert `ValueAtom`s) | <https://github.com/zarqa-ai/metta-motto> | zarqa-ai | Design inspiration only: V2 took its pattern of returning model output as an inert value atom, not the framework. V2 map: ADAPT | MIT *(notes)* | [`omegav2/docs/whitepaper/D21_related_work.md`](https://github.com/PhysixSNET/omegav2/blob/main/docs/whitepaper/D21_related_work.md) | |
| PeTTa `lib_llm` | <https://github.com/trueagi-io/PeTTa> | Patrick Hammer | Loaded at run time from the PeTTa library | MIT | [`lib_omegaclaw_core.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta), [`lib_llm_ext.py`](https://github.com/PhysixSNET/omegahive/blob/main/lib_llm_ext.py) | |
| OpenAI Python SDK (`openai`) | <https://github.com/openai/openai-python> | OpenAI | Dependency, not pinned: the OpenAI-compatible client a mind uses | Apache-2.0 | [`requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/requirements.txt), [`lib_llm_ext.py`](https://github.com/PhysixSNET/omegahive/blob/main/lib_llm_ext.py); card [llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md) | |

<a id="memory-chromadb"></a>
## Memory (ChromaDB)

Each mind keeps named AtomSpace spaces as `.metta` files, and embeds long-term recall into ChromaDB beside them.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| petta_lib_chromadb | <https://github.com/patham9/petta_lib_chromadb> | Patrick Hammer | Loaded at run time: `git-import!` or a clone of the default branch, not pinned. V2 map: ADAPT | None declared *(notes)* | [`lib_omegaclaw_core.metta:37-38`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta#L37-L38), [`hive/supervisor/workspace.py:30`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L30), [`src/memory.metta`](https://github.com/PhysixSNET/omegahive/blob/main/src/memory.metta); card [mind-memory](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-memory.md) | |
| ChromaDB | <https://github.com/chroma-core/chroma> | Chroma | Dependency, not pinned | Apache-2.0 | [`requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/requirements.txt), [`docs/reference-internals-memory-store.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-internals-memory-store.md) | |
| sentence-transformers | (link to be confirmed) | To be confirmed | Dependency, not pinned: local embeddings | To be confirmed | [`requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/requirements.txt) | |
| e5-large-v2 embedding model (`intfloat/e5-large-v2`) | (link to be confirmed) | To be confirmed | Loaded at run time in the container image | To be confirmed | [`Dockerfile`](https://github.com/PhysixSNET/omegahive/blob/main/Dockerfile) | |
| FAISS | <https://github.com/facebookresearch/faiss> | facebookresearch | Pinned dependency, `v1.8.0`, in the container image only | To be confirmed | [`Dockerfile`](https://github.com/PhysixSNET/omegahive/blob/main/Dockerfile) | |
| faiss_ffi (PeTTa vector spaces) | <https://github.com/patham9/faiss_ffi> | Patrick Hammer | Design inspiration only here. V2 map: ADAPT | None declared *(notes)* | none | |

<a id="predictive-coding"></a>
## Predictive coding (FabricPC)

The optional Assume organ keeps its graph as MeTTa atoms and uses FabricPC as a warm numeric view. It is not enabled for hive minds.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| FabricPC (predictive coding on JAX) | <https://github.com/trueagi-io/FabricPC> | TrueAGI | Loaded at run time: an optional external checkout found through `FABRICPC_REPO` | MIT *(notes)* | [`modules/assume/README.md`](https://github.com/PhysixSNET/omegahive/blob/main/modules/assume/README.md), [`install/installer_common.py:27`](https://github.com/PhysixSNET/omegahive/blob/main/install/installer_common.py#L27), [`docs/EARLIER_EXPERIMENTS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md) | ActPC-Chem; ActPC-Geom; Predictive coding in the visual cortex |

<a id="mcp-and-agent-interop"></a>
## MCP and agent interop

Outside agents join a swarm over the hive's own MCP server. Agentverse gives an optional module a public agent identity.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| Model Context Protocol | (link to be confirmed) | To be confirmed | Design inspiration only: the hive implements the protocol itself (version `2025-06-18`); no MCP library | To be confirmed | [`hive/core/mcp.py`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/mcp.py), [`hive/MCP_S3.md`](https://github.com/PhysixSNET/omegahive/blob/main/hive/MCP_S3.md); card [mcp-interface](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mcp-interface.md) | |
| uAgents (`uagents`, `uagents_core`) | (link to be confirmed) | Fetch.ai, ASI Alliance | Dependency, not pinned: the optional Agentverse module | To be confirmed | [`modules/agentverse/module.toml`](https://github.com/PhysixSNET/omegahive/blob/main/modules/agentverse/module.toml), [`docs/tutorial-06-remote-agentverse-skills.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/tutorial-06-remote-agentverse-skills.md) | |
| Agentverse | <https://agentverse.ai> | Fetch.ai, ASI Alliance | Loaded at run time: agent search, Almanac and mailbox, when the module is on | n/a (a service) | [`modules/agentverse/src/agentverse_bridge.py`](https://github.com/PhysixSNET/omegahive/blob/main/modules/agentverse/src/agentverse_bridge.py) | |

<a id="web-stack"></a>
## The web stack

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| FastAPI | <https://github.com/fastapi/fastapi> | Sebastián Ramírez and contributors | Dependency, minimum version (`>=0.110`) | MIT | [`hive/requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/hive/requirements.txt), [`hive/core/app.py`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/app.py) | |
| Uvicorn | <https://github.com/Kludex/uvicorn> | Tom Christie and contributors | Dependency, minimum version | BSD-3-Clause | [`hive/requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/hive/requirements.txt) | |
| HTTPX | <https://github.com/encode/httpx> | Encode, Tom Christie | Dependency, minimum version | BSD-3-Clause | as above | |
| websockets | <https://github.com/python-websockets/websockets> | Aymeric Augustin and contributors | Dependency, minimum version | BSD-3-Clause | as above | |
| Pillow | <https://github.com/python-pillow/Pillow> | Pillow contributors | Dependency, minimum version | MIT-CMU | as above | |
| React and React DOM | (link to be confirmed) | To be confirmed | Pinned dependency, 19.3.0 (lock file) | MIT | [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json); card [ui-shell](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ui-shell.md) | |
| Three.js | <https://github.com/mrdoob/three.js> | three.js authors | Pinned dependency, 0.186.1, in the hive UI. Vendored copy in Studio (`omegadesign/ui-src/vendor/three`) | MIT | [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json), [`omegadesign/NOTICE`](https://github.com/PhysixSNET/omegadesign/blob/main/NOTICE) | |
| React Three Fiber and postprocessing (`@react-three/*`) | (link to be confirmed) | To be confirmed | Pinned dependency, 9.8.1 and 3.1.3 | MIT | [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json) | |
| Vite, Tailwind CSS, Zustand, CodeMirror, Framer Motion | (links to be confirmed) | their projects | Pinned dependencies (lock file) | MIT | [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json) | |
| mermaid (`@mermaid-js/mermaid-cli` 11.4.2 for render checks) | (link to be confirmed) | Mermaid project | Design and doc tooling only: the schematics diagrams are mermaid and draw on GitHub | To be confirmed | [`omegahive-schematics/README.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/README.md) | |

<a id="channels"></a>
## Channels

Hive minds use only the hive channel. The inherited adapters below are not wired for hive minds by design.

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| Baileys (`@whiskeysockets/baileys`) | (link to be confirmed) | WhiskeySockets | Pinned dependency, 7.0.0-rc11 (lock file), in the closed-tier WhatsApp bridge. An unofficial WhatsApp Web client | MIT | [`channels/whatsapp_bridge/GPL-NOTICE.md`](https://github.com/PhysixSNET/omegahive/blob/main/channels/whatsapp_bridge/GPL-NOTICE.md); card [channels](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/channels.md) | |
| libsignal | (link to be confirmed) | To be confirmed | Pinned dependency, 6.0.0, reached through Baileys; not committed | GPL-3.0 | as above; [`omegav2/runtime/whatsapp/GPL-NOTICE.md`](https://github.com/PhysixSNET/omegav2/blob/main/runtime/whatsapp/GPL-NOTICE.md) | |
| pino, qrcode, qrcode-terminal | (links to be confirmed) | their projects | Pinned dependencies of the bridge | MIT, MIT, not stated | [`channels/whatsapp_bridge/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/channels/whatsapp_bridge/package.json) | |
| sharp prebuilt libvips binaries | (link to be confirmed) | To be confirmed | Optional, through Baileys' image support | LGPL-3.0-or-later | [`channels/whatsapp_bridge/GPL-NOTICE.md`](https://github.com/PhysixSNET/omegahive/blob/main/channels/whatsapp_bridge/GPL-NOTICE.md) | |
| Telegram Bot API, Slack Web API, Mattermost, IRC | <https://api.telegram.org>, <https://slack.com/api/> | the services | Loaded at run time: Telegram, Slack and IRC use the standard library only; Mattermost uses requests and websocket-client | n/a (services) | [`channels/telegram.py`](https://github.com/PhysixSNET/omegahive/blob/main/channels/telegram.py), [`channels/slack.py`](https://github.com/PhysixSNET/omegahive/blob/main/channels/slack.py), [`channels/mattermost.py`](https://github.com/PhysixSNET/omegahive/blob/main/channels/mattermost.py), [`channels/irc.py`](https://github.com/PhysixSNET/omegahive/blob/main/channels/irc.py) | |
| requests, websocket-client | (links to be confirmed for websocket-client) | their projects | Dependencies, not pinned | requests: Apache-2.0; websocket-client: to be confirmed | [`requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/requirements.txt) | |

<a id="documents"></a>
## Documents

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| pypdf | (link to be confirmed) | Mathieu Fenniak and contributors | Vendored copy, 6.19.0: page extraction in Library | BSD-3-Clause | [`omegalibrary/NOTICE`](https://github.com/PhysixSNET/omegalibrary/blob/main/NOTICE), [`omegalibrary/app/tools/extract_pages.py`](https://github.com/PhysixSNET/omegalibrary/blob/main/app/tools/extract_pages.py) | |
| PyMuPDF (`pymupdf`) | (link to be confirmed) | Artifex | Dependency of the closed-tier Atlas app, installed from PyPI, not bundled | AGPL-3.0 or a commercial licence | [`omegaatlas/NOTICE`](https://github.com/PhysixSNET/omegaatlas/blob/main/NOTICE) | |

<a id="tooling"></a>
## Tooling

| Upstream | URL | Authors or organisation | How we use it | Licence | Where used here | Key papers |
|---|---|---|---|---|---|---|
| CodeTour (VS Code extension `vsls-contrib.codetour`) | <https://code.visualstudio.com/> (VS Code; extension link to be confirmed) | vsls-contrib | Design and doc tooling only: the six `.tours` open in it | To be confirmed | [`.tours/README.md`](https://github.com/PhysixSNET/omegahive/blob/main/.tours/README.md), [`docs/CODE_TOURS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/CODE_TOURS.md) | |
| Epistemic Resolve harness | <https://github.com/khellar/epistemic-resolve> | Khellar Crawford, Patrick Hammer | Loaded at run time by `bench-epistemic` when a checkout is present | Apache-2.0 *(as stated in our code)* | [`hive/bench/epistemic.py`](https://github.com/PhysixSNET/omegahive/blob/main/hive/bench/epistemic.py) | (Epistemic Resolve, AGI-26, link to be confirmed) |
| Benchmarks listed by OmegaBench: MMLU-Pro, HLE, Terminal-Bench, ARC-AGI-2 and 3, SWE-bench Verified, GAIA, OSWorld-V2, tau2-bench | links in the catalogue | their authors | Design inspiration only: references, not installed datasets or results | per benchmark | [`omegabench/catalog.py`](https://github.com/PhysixSNET/omegahive/blob/main/omegabench/catalog.py) | HLE; GAIA |
| pytest, Vitest, Playwright (`playwright-core`) | (links to be confirmed) | their projects | Test dependencies | To be confirmed | [`hive/requirements.txt`](https://github.com/PhysixSNET/omegahive/blob/main/hive/requirements.txt), [`hive/ui/package.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/package.json) | |

<a id="papers-by-topic"></a>
## Papers by topic

Titles, authors and links are as recorded in the repositories' docs and the team's notes. Where a field is missing we say so rather than guess.

### MeTTa, Hyperon and PRIMUS
- Ben Goertzel et al., *OpenCog Hyperon: A Framework for AGI at the Human Level and Beyond*, 2023. <https://arxiv.org/abs/2310.18318>
- Ben Goertzel et al., *Reflective Metagraph Rewriting as a Foundation for an AGI Language of Thought*, 2021. <https://arxiv.org/abs/2112.08272>
- Lucius Gregory Meredith, Ben Goertzel, Jonathan Warrell and Adam Vandervorst, *Meta-MeTTa: an operational semantics for MeTTa*, 2023. <https://arxiv.org/abs/2305.17218>
- TrueAGI, *MeTTa specification* (living document). <https://trueagi-io.github.io/hyperon-experimental/metta/>
- Ben Goertzel, *The General Theory of General Intelligence*, 2021. <https://arxiv.org/abs/2103.15100>
- Ben Goertzel, *Patterns of Cognition: Cognitive Algorithms as Galois Connections Fulfilled by Chronomorphisms on Probabilistically Typed Metagraphs*, 2021. <https://arxiv.org/abs/2102.10581>
- Ben Goertzel, *World Modeling in Hyperon for PRIMUS*, 2025. <https://singularitynet.io/wp-content/uploads/2025/12/PRIMUS-world-modeling_v2.pdf>
- AGI-25 architecture chapter on PRIMUS (title and authors to be confirmed). <https://link.springer.com/chapter/10.1007/978-3-032-00686-8_18>
- Metagoals paper on goal stability (title and authors to be confirmed), 2024. <https://arxiv.org/abs/2412.16559>
- Ben Goertzel, Hyperon architecture whitepaper, July 2026 (link to be confirmed).

### PeTTa
- PeTTa project announcement, SWI-Prolog Discourse (author and year to be confirmed). <https://swi-prolog.discourse.group/t/metta-language-transpiler-petta/9490>

### NAL, NARS and ONA
- Pei Wang, *Non-Axiomatic Logic (NAL) Specification*. <https://cis.temple.edu/~pwang/Writing/NAL-Specification.pdf>
- Pei Wang, *Non-Axiomatic Logic: A Model of Intelligent Reasoning*, 2013 (link to be confirmed).
- Pei Wang, *Non-Axiomatic Reasoning System (Version 4.1)*. <https://cis.temple.edu/~pwang/Publication/NARS-41.pdf>
- Pei Wang and Seemal Awan, *Reasoning in Non-Axiomatic Logic*. <https://cis.temple.edu/~pwang/Publication/Diagnosis.pdf>
- OpenNARS for Applications paper (title, authors and link to be confirmed).

### PLN
- Ben Goertzel, Matthew Iklé, Izabela Freire Goertzel and Ari Heljakka, *Probabilistic Logic Networks*, Springer, 2008. <https://wiki.opencog.org/w/PLNBook>

### Attention (ECAN)
- OpenCog, *Economic Attention Allocation* (wiki). <https://wiki.opencog.org/w/OpenCogPrime%3AEconomicAttentionAllocation>
- Matthew Iklé and Ben Goertzel, *Nonlinear-Dynamical Attention Allocation via Information Geometry* (year to be confirmed). <https://goertzel.org/ECAN_v3.pdf>
- *Engineering General Intelligence*, vol. 1, cited for ECAN in `docs/omegadots/PLAN.md` (authors, year and link to be confirmed).
- See also *Patterns of Cognition*, above.

### Motivation and emotion
- *MetaMo: A Robust Motivational Framework for Open-Ended AGI*, AGI 2025, Springer, 2026 (authors to be confirmed). <https://doi.org/10.1007/978-3-032-00686-8_34>
- *Embodying Abstract Motivational Principles in Concrete AGI Systems: From MetaMo to Open-Ended OpenPsi*, AGI 2025, Springer, 2026 (authors to be confirmed). <https://doi.org/10.1007/978-3-032-00686-8_35>

### Predictive coding
- Ben Goertzel, *ActPC-Chem*, 2024. <https://arxiv.org/abs/2412.16547>
- Ben Goertzel, *ActPC-Geom: A Very Preliminary Analysis*, 2025. <https://arxiv.org/abs/2501.04832>
- Rajesh P. N. Rao and Dana H. Ballard, *Predictive Coding in the Visual Cortex*, Nature Neuroscience 2, 79–87, 1999. <https://doi.org/10.1038/4580>

### ASI:Chain
- SingularityNET, ASI:Chain devnet and Hyperon announcement (title and date to be confirmed). <https://singularitynet.io/singularitynet-launches-asichain-devnet-and-hyperon-agi-framework/>

### OmegaClaw and evaluation
- OmegaClaw paper, AGI-26 (title, authors and link to be confirmed).
- Khellar Crawford and Patrick Hammer, *Epistemic Resolve*, AGI-26 (full title and link to be confirmed). Harness: <https://github.com/khellar/epistemic-resolve>
- The HLE and GAIA benchmark papers, as catalogued by OmegaBench (titles and authors to be confirmed). <https://arxiv.org/abs/2501.14249>, <https://arxiv.org/abs/2311.12983>
