# Primer: MeTTa and the AtomSpace

## What it is
**MeTTa** is the language of the Hyperon project. A program is a set of **atoms**: symbols, numbers, strings, variables (`$x`) and nested expressions in parentheses. An **AtomSpace** (a "space") is a store of atoms you can add to, remove from and **match** against a pattern. A rule `(= (f $x) body)` defines a function by pattern: calling `(f 3)` rewrites to `body` with `$x` bound to 3. A line starting with `!` is evaluated when the file loads.

## Why it is used here
The design is Hyperon-first: knowledge lives as atoms, and the language model is one organ, not the control plane ([`omegahive/docs/START_HERE.md:40-41`](https://github.com/PhysixSNET/omegahive/blob/main/docs/START_HERE.md#L40-L41)). In this build, atoms live in two places:
- **each mind's own spaces,** inside the mind's PeTTa process;
- **the hive's shared spaces,** one commons and one vocabulary per swarm, inside one PeTTa interpreter in the hive process.

## The minimum you must know
- **Spaces are named handles.** A mind binds seven: `&persistent`, `&agenda`, `&beliefs`, `&world`, `&events`, `&activity` and `&cleanup` ([`omegahive/lib_omegaclaw_core.metta:40-46`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta#L40-L46)).
- **The core verbs** are `add-atom`, `remove-atom`, `match`, `collapse` (gather all results into a list) and `let`/`let*` (bind values).
- **Evaluation is lazy at the point you might not expect.** `add-atom` stores its argument *unevaluated*, so compute first with `let`, then add ([`omegahive/hive/spaces/lib_hive.metta:11-12`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L11-L12)).
- **Results can be many.** A call can return several answers, one per matching rule. `collapse` turns them into one list; `unique-atom` removes duplicates.
- **PeTTa has no persistence of its own.** Mind spaces are saved as `.metta` files; the hive commons is rebuilt at start from an operations log ([`omegahive/hive/spaces/service.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L1-L5)).

## A tiny example
How the commons stores one belief per statement ([`omegahive/hive/spaces/lib_hive.metta:99-103`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L99-L103)):

```metta
(= (hive-integrate! $commons $stmt $tv $stamp)
   (let $cur (collapse (match $commons (Current $stmt $t0 $s0) (Current $stmt $t0 $s0)))
        (if (== $cur ())
            (let $added (add-atom $commons (Current $stmt $tv $stamp))
                 (adopted $tv $stamp))
            ...
```

Read it as: find every `(Current stmt ...)` atom; if there is none, add one and return `(adopted tv stamp)`. The `...` branch revises or chooses (see [truth-values-nal-pln.md](truth-values-nal-pln.md)).

And the test that drives it, which also shows how grants are atoms ([`omegahive/tests/hive_lib_smoke.metta:18-20`](https://github.com/PhysixSNET/omegahive/blob/main/tests/hive_lib_smoke.metta#L18-L20)):

```metta
!(add-atom &hive_acl (Grant omega-a &commons_s $stmt publish))
!(add-atom &hive_acl (Grant omega-x &commons_s (--> sky $what) publish))
```

The second grant lets `omega-x` publish only statements that match `(--> sky $what)`.

## Common pitfalls
- **Raw text never goes into MeTTa.** Agent strings pass through `sexpr.py`, which re-renders them from a small grammar and refuses `!`, `&` handles and comments ([`omegahive/hive/spaces/sexpr.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/sexpr.py#L1-L8)). Do not splice strings yourself.
- **Import paths resolve against the main file,** not the importing file. That is why `lib_hive.metta` imports nothing ([`omegahive/hive/spaces/lib_hive.metta:14-16`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L14-L16)).
- **Load order matters.** PeTTa compiles calls when a file is imported, so a caller loaded before the function it calls compiles that call as an inert literal ([`omegahive/lib_omegaclaw.metta:3-6`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw.metta#L3-L6)).
- **One interpreter thread.** In the hive, every MeTTa call goes through one worker thread; a second thread deadlocks ([`omegahive/hive/spaces/service.py:52-57`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L52-L57)).
- **Long-term recall is not the AtomSpace.** It is ChromaDB beside it, and the hive's default embedder is `mock/hash` ([`omegahive/STATUS.md:52`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L52)).

## Upstream
- **MeTTa and Hyperon:** the Hyperon project by TrueAGI and SingularityNET. The language site is metta-lang.dev.
- **PeTTa,** the MeTTa implementation used here: <https://github.com/trueagi-io/PeTTa>. See [petta-and-swi-prolog.md](petta-and-swi-prolog.md).
- **MeTTaScript,** which runs the same libraries in the browser: named in [`omegahive/hive/ui/src/lib/mindSpace/core.ts`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/src/lib/mindSpace/core.ts).

## Read next
- [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md): both kinds of space, persistence and the toolchain.
- [`omegahive-schematics/04-knowledge/02-beliefs-sharing.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md): publish, query and revise in a commons.
- [`omegahive-schematics/03-minds/03-modules.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md): how a module registers its own space.
