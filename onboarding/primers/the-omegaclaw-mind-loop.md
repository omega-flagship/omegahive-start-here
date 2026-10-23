# Primer: the OmegaClaw mind loop

## What it is
**OmegaClaw** is the agent runtime that native minds run on. It is written in MeTTa on PeTTa. The core is inherited from the public OmegaClaw Core by its upstream author and credited in [`omegahive/NOTICE`](https://github.com/PhysixSNET/omegahive/blob/main/NOTICE). A native mind is one PeTTa process that runs one loop forever: **receive, think, gate, act, save, sleep**.

## Why it is used here
Every native mind on the hive (kind `omega`, including each person's personal mind) is this loop. The hive starts it, feeds it messages, gates its commands and pays for its model calls. If you change how a mind thinks, you change this loop or plug into one of its hooks.

## The minimum you must know
- **Entry and load order.** The mind's `run.metta` imports `lib_omegaclaw` and calls `(omegaclaw)` ([`omegahive/hive/supervisor/workspace.py:24-28`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L24-L28)). `lib_omegaclaw` loads the core substrate, then the modules, then attention, then the loop, in that order ([`omegahive/lib_omegaclaw.metta:8-11`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw.metta#L8-L11)).
- **One iteration** ([`omegahive/src/loop.metta:139-190`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L139-L190)):
  1. **Receive** a message from the channel. A new message gives the mind up to 12 model turns ([`omegahive/src/loop.metta:21, 150-155`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L21)).
  2. **Build the context:** prompt, the skills it may use, promoted memory hints, recall, history, last results, time and the output format ([`omegahive/src/loop.metta:87-104`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L87-L104)).
  3. **Call the model** for up to five command lines ([`omegahive/src/loop.metta:99, 165-167`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L99)). On a hive, the call goes through the hive's gateway.
  4. **Gate** each command: on a hive, the policy gate decides first ([`omegahive/src/loop.metta:111-117`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L111-L117)).
  5. **Act:** run each allowed command as a MeTTa call and collect the results ([`omegahive/src/loop.metta:119-132`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L119-L132)).
  6. **Hooks, then save:** run `response` hooks, bound and save the memory spaces, sleep, then recurse ([`omegahive/src/loop.metta:180, 185-190`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L180)).
- **With no new message,** the mind wakes on its own every `wakeupInterval` (900 s) for a few turns ([`omegahive/src/loop.metta:29, 183-184`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L29)).
- **A chosen wait rests the mind.** Live since the handover, and arriving with the omegahive pull request `port/idle-minds`: a reply that is nothing but `wait` ends the remaining turns, so the mind makes no model call until new input or its wake; `wait 900` asks for 900 seconds; a provider error retries after 60 s. Before, `wait` was a no-op and one message could cost 12 calls, all waits. See [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md).
- **Skills are MeTTa functions** declared in catalogue, signature and affordance files. Reasoning skills are callable but never called automatically in this build ([`omegahive/STATUS.md:49`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L49)).
- **Two hook phases** are the seams for new organs: `cycle` (start of every iteration) and `response` (after each model turn) ([`omegahive/src/loop.metta:142, 180`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L142)). Hooks and boot organs run only if trusted ([`omegahive/src/loop.metta:65-70`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L65-L70)).

## A tiny example
The gate, the line between what the model says and what the mind does ([`omegahive/src/loop.metta:111-117`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L111-L117)):

```metta
; Before a command runs, a hive decides whether it may (policy rules and human
; approvals; see hive/core/policy.py): True, or the text recorded instead of a
; result.  Off the hive every command is allowed.
(= (command-gate $cmd)
   (if (== (commchannel) hive)
       (py-call (hive_commons.authorize (repr $cmd)))
       True))
```

`authorize` fails closed: if the hive cannot be reached, the command does not run. A short local list of skills (for example `send`, `remember`, `query`, `hive-publish`) skips the call and is allowed without asking the hive ([`omegahive/modules/hive/src/hive_commons.py:932-962`](https://github.com/PhysixSNET/omegahive/blob/main/modules/hive/src/hive_commons.py#L932-L962)). Check that list when you review the gate.

## Common pitfalls
- **Load order is semantics.** Load the loop before a module's functions and its calls compile as inert literals ([`omegahive/lib_omegaclaw.metta:3-6`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw.metta#L3-L6)).
- **The model's defaults are in the loop file** ([`omegahive/src/loop.metta:24-25`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L24-L25)). On a hive the provider is the hive gateway instead, set by the supervisor ([`omegahive/hive/supervisor/workspace.py:241-246`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L241-L246)). Check which one a mind actually used.
- **Off the hive, nothing is gated.** A mind run on its own allows every command ([`omegahive/src/loop.metta:113-117`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L113-L117)).
- **Malformed model output does nothing.** A response that does not parse is recorded as an error and no command runs ([`omegahive/src/loop.metta:170-172`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L170-L172)).
- **Memory is bounded by size, not judgement** today ([`omegahive/src/loop.metta:30-39`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L30-L39)). See [attention-ecan.md](attention-ecan.md).
- **Two OmegaClaw Core URLs.** The repo's own `run.metta` imports `physixCN/OmegaClaw-Core` ([`omegahive/run.metta:2`](https://github.com/PhysixSNET/omegahive/blob/main/run.metta#L2)). The file the hive writes for each mind names `asi-alliance/OmegaClaw-Core` ([`omegahive/hive/supervisor/workspace.py:25`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L25)). The workspace links the shared checkout, so the import resolves locally ([`omegahive/hive/supervisor/workspace.py:5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L5)). Know which checkout your mind loads.
- **Iter minds are a different runtime** (Python, Docker only). This page is about `omega` minds.

## Upstream
- **OmegaClaw Core** by its upstream author: the public OmegaClaw-Core repository, credited in [`omegahive/NOTICE`](https://github.com/PhysixSNET/omegahive/blob/main/NOTICE).
- **PeTTa:** <https://github.com/trueagi-io/PeTTa>
- **ChromaDB library for PeTTa,** used for recall: <https://github.com/patham9/petta_lib_chromadb>

## Read next
- [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md): the loop, the three connections to the hive, and the lifecycle.
- [`omegahive-schematics/03-minds/03-modules.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md): modules, skills, hooks and organs.
- [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md): what the gate decides.
- [`omegahive/docs/reference-internals-loop.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-internals-loop.md): the inherited loop reference (legacy; check against the code).
