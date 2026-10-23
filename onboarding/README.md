# Onboarding

This folder helps you learn the OmegaHive code and then decide, component by component, whether to keep it, harden it, or swap in your own module. Each fact lives in one place. These pages link down to the schematics and the code; they do not repeat them.

## How links work here
- **Inside this folder (`onboarding/`):** normal relative links.
- **Everything else:** always a full link, `https://github.com/PhysixSNET/<repo>/blob/main/<path>` for a file or `https://github.com/PhysixSNET/<repo>/tree/main/<path>` for a folder. This covers the schematics (`omegahive-schematics`), the code (`omegahive`), the app repos and this repo's own root files.
- **Code citations:** a full link to the file on `main`, with `#L<line>` or `#L<start>-L<end>` for lines, for example `https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L20-L22`. Line numbers were read at `omegahive` commit `34b0fb3`. Lines drift; if a line has moved, search the file for the named symbol.

## Files

| File | What it is for |
|---|---|
| [`tracks/`](tracks/) | Learning tracks by role. Start here if you are new. |
| [`PROGRAM.md`](PROGRAM.md) | A suggested four-week rollout for a whole team: all hands, role tracks, DECIDE, review and shadow; track prerequisites, owners and sign-off |
| [`GLOSSARY.md`](GLOSSARY.md) | Every term used across the repos, one or two lines each, with a link to where it is explained |
| [`DECIDE.md`](DECIDE.md) | The keep, harden or swap rubric, how to read the evidence, the decision-record template, and how to swap a module safely |

### Primers (zero to useful, one page each)

| Primer | Read it if you need to |
|---|---|
| [`primers/metta-and-atomspace.md`](primers/metta-and-atomspace.md) | read or write MeTTa, or understand where atoms live |
| [`primers/petta-and-swi-prolog.md`](primers/petta-and-swi-prolog.md) | run anything that reasons, or fix "PeTTa failed to start" |
| [`primers/truth-values-nal-pln.md`](primers/truth-values-nal-pln.md) | read `(stv f c)`, NAL or PLN rules, or the commons revision |
| [`primers/attention-ecan.md`](primers/attention-ecan.md) | understand what "attention" means in this build, and what it does not |
| [`primers/mork-and-das.md`](primers/mork-and-das.md) | plan storage or hive-to-hive work |
| [`primers/the-omegaclaw-mind-loop.md`](primers/the-omegaclaw-mind-loop.md) | change or replace how a native mind thinks and acts |
| [`primers/hive-concepts.md`](primers/hive-concepts.md) | get the hive's nouns straight: swarms, rooms, personal minds, the Ask, governance |
| [`primers/the-programs-contract.md`](primers/the-programs-contract.md) | write, check or replace an app |

## Suggested order
1. Your track in `tracks/`.
2. [`primers/hive-concepts.md`](primers/hive-concepts.md), then the primers your track names.
3. [`omegahive-schematics/README.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/README.md) and [`omegahive-schematics/LEGEND.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/LEGEND.md).
4. [`DECIDE.md`](DECIDE.md) when you start judging a component.

Keep [`GLOSSARY.md`](GLOSSARY.md) open beside you.

## Where else to look
- **What works and what is broken:** [`omegahive/STATUS.md`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md) and each app repo's `STATUS.md`.
- **Every feature and its state:** [`omegahive/docs/FEATURES.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/FEATURES.md).
- **Where the coupling is:** [`omegahive/docs/MODULARITY.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/MODULARITY.md).
- **Work that exists but is not switched on:** [`omegahive/docs/EARLIER_EXPERIMENTS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md).
- **Repos and tiers:** the [`README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md) at the root of this repo.
