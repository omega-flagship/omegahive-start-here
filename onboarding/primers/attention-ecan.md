# Primer: attention and ECAN

## What it is
**ECAN** (Economic Attention Networks) is OpenCog's attention model. Each atom holds attention values: **STI** (short-term importance, what is in focus now) and **LTI** (long-term importance, what is worth keeping). Atoms pay **rent** to stay in focus and earn **wages** when they are useful; importance **spreads** along links. Atoms that fall too low are forgotten.

## Why it is used here
A mind's spaces grow every turn and must stay bounded. The design wants attention to decide what the mind looks at, and what it keeps. **In this build that is mostly intent.** What ships is a heuristic classifier that uses ECAN's names ([`omegahive/STATUS.md:51`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L51)).

## The minimum you must know
- **What is built:** an optional attention organ. It binds an `&attention` space, persists it to `attention.metta`, and registers a hook that runs after each model turn ([`omegahive/lib_omegaclaw_attention.metta:7-17`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_attention.metta#L7-L17)).
- **How it scores:** `attention_ledger.py` matches keyword lists (protected, stale, event, malformed) and length, and returns STI, LTI and a proposed action such as keep, review-retire or review-merge ([`omegahive/src/attention_ledger.py:157-210`](https://github.com/PhysixSNET/omegahive/blob/main/src/attention_ledger.py#L157-L210)).
- **It only proposes.** The pass defaults to `review-only` ([`omegahive/src/attention_ledger.py:362`](https://github.com/PhysixSNET/omegahive/blob/main/src/attention_ledger.py#L362)). "Active" mode records intent only, until changes to the target space are approved separately ([`omegahive/src/attention_ledger.py:357-358`](https://github.com/PhysixSNET/omegahive/blob/main/src/attention_ledger.py#L357-L358)).
- **What actually bounds memory today** is a size limit per space, with protected atoms never dropped and every drop recorded in `memory/evicted.metta` ([`omegahive/src/skills_runtime_spaces.metta:14-16`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_runtime_spaces.metta#L14-L16)). The loop sets those limits and calls them "temporary survival bounds" until attention-driven pruning can replace them ([`omegahive/src/loop.metta:30-39`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L30-L39)).
- **What is not built here:** a real STI/LTI economy, spreading, or attention in the swarm commons.
- **The design rule:** attention decides what is on the table, never the choice. It may rank and propose; it never confers truth, consent or authority ([`omegahive/docs/theory/cognition-attention-importance.md:85-88`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/cognition-attention-importance.md#L85-L88)).

## A tiny example
The organ's hook, kept as a plain atom so the loop calls it live each turn ([`omegahive/lib_omegaclaw_attention.metta:14-17`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_attention.metta#L14-L17)):

```metta
; Keep this as a symbolic runtime-hook atom. Registering through eval would
; evaluate the observer once and store a stale result instead of the live call.
(RuntimeHook response spin-counter (attention-observe-response (get-state &lastResponseMsgNew) (get-state &lastResponseSexpr)))
(TrustedRuntimeHook response spin-counter)
```

The loop runs every trusted `response` hook after each model turn ([`omegahive/src/loop.metta:180`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L180)).

## Common pitfalls
- **Do not read "ECAN" in names as ECAN behaviour.** STI and LTI here are numbers set by keyword matches, not an economy.
- **Raw spreading made things worse.** In the separate V2 body, raw ECAN spreading cut focus precision to 2/3, and a utility gate restored 3/3 on a synthetic test. Treat spreading as a qualified negative until gated ([`omegahive/docs/EARLIER_EXPERIMENTS.md:42, 85`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L42)).
- **The V2 attention bank is a different body.** It had a conserved STI/LTI economy, but it needs an adapter behind `lib_omegaclaw_attention.metta` to come here ([`omegahive/docs/EARLIER_EXPERIMENTS.md:42`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L42)).
- **Keep the seam when you replace it.** Keep the `&attention` registration and persistence; swap what `attention_ledger.py` computes.

## Upstream
- **ECAN:** described in OpenCog's attention allocation work and in *Engineering General Intelligence* (named in [`omegahive/docs/omegadots/PLAN.md:83`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md#L83)).
- **metta-attention,** an ECAN implementation in MeTTa: <https://github.com/iCog-Labs-Dev/metta-attention>. The plan names it as a later replacement ([`omegahive/docs/omegadots/PLAN.md:799`](https://github.com/PhysixSNET/omegahive/blob/main/docs/omegadots/PLAN.md#L799)).
- **DAS Attention Broker,** part of the Distributed AtomSpace project (see [mork-and-das.md](mork-and-das.md)).

## Read next
- [`omegahive-schematics/04-knowledge/03-reasoning.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/03-reasoning.md), diagram 2, "Attention: what exists and what is intended".
- [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md): space limits and eviction.
- [`omegahive-schematics/03-minds/03-modules.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md): runtime hooks and organs.
