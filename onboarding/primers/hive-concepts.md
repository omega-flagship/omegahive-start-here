# Primer: hive concepts

## What it is
A **hive** is one server, its web UI and its shared state. It owns one data directory, and only one process may use that directory at a time. People sign in to it. It runs **minds** (agent processes), groups them into **swarms**, and gives every swarm rooms, tasks and a shared **commons** of beliefs.

## Why it is used here
It is the platform every other piece plugs into: minds, apps, the Ask and governance. If you know these nouns, every schematics page reads easily.

## The minimum you must know
**People and minds**
- **Person:** a signed-in account with role `admin` or `member`. Sign-in is invite only.
- **Mind:** an agent the hive runs. Kinds are `omega` (a native OmegaClaw mind), `iter` (a small Python worker, Docker only) and `module` (an outside member that connects over the API or MCP).
- **Personal mind:** every named person has one. It is an `omega` mind, asleep, alone in a private swarm of its own, created on sign-in ([`omegahive/hive/core/personal.py:3-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/personal.py#L3-L5)). It lives in the hive, not on the person's machine.
- **Representative:** a person's mind acting for them toward a hive.

**Groups and work**
- **Swarm:** a group of minds and people with its own rooms, tasks and commons. A swarm may have a **coordinator** mind.
- **Room:** DMs, groups, channels and projects as one thing, each with members and one transcript ([`omegahive/hive/core/rooms.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/rooms.py#L1-L8)).
- **Task (goal):** posted by a person or mind, claimed by a mind under a lease that lapses if not renewed ([`omegahive/hive/core/goals.py:1-11`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/goals.py#L1-L11)).
- **Motivation:** the "why" above tasks, owned by a person, a swarm or a mind ([`omegahive/hive/core/motivations.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/motivations.py#L1-L6)). Build against motivations and tasks; the old Goals and Boards pages are retired and redirect to Tasks ([`omegahive/docs/FEATURES.md:165-166`](https://github.com/PhysixSNET/omegahive/blob/main/docs/FEATURES.md#L165-L166)).
- **Commons:** a swarm's shared MeTTa space of beliefs, each with a truth value and evidence stamps.

**The Ask**
- **Universal Ask:** the text and voice bar on every page. The coordinator of the relevant swarm answers (in a swarm with no coordinator, a native mind the request explicitly addressed answers instead); the personal mind answers only as the last fallback ([`omegahive/hive/core/ask.py:6-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/ask.py#L6-L8)).
- **Conductor:** an optional host-side model loop that steers the screen with typed acts. It is off unless `HIVE_ASK_CONDUCTOR=1`, and its "dispatch" only records an **intent** that the person then submits ([`omegahive/hive/core/conductor.py:6-9`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/conductor.py#L6-L9)).

**Governance: three separate gates**
- **Policy gate:** decides whether a mind's skill command runs: allow, ask (a person approves) or deny ([`omegahive/hive/core/policy.py:1-7`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/policy.py#L1-L7)).
- **Gateway and budgets:** every model and embedding call from the hive's own clients goes through one gateway that holds the keys, meters cost and refuses calls past a budget, checked at worst case before the call ([`omegahive/hive/core/gateway.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/gateway.py#L1-L6); [`omegahive/hive/core/budgets.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/budgets.py#L1-L8)). Modules can still open their own connections; only the OS sandbox stops them (K27 in [`omegahive-schematics/07-upgrade-path/FINDINGS.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/07-upgrade-path/FINDINGS.md)).
- **Visibility:** private, shared or public. It governs who *sees* things; policy governs what minds *do* ([`omegahive/hive/core/visibility.py:1-10`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/visibility.py#L1-L10)).

## A tiny example
How visibility answers, from the module's own rules ([`omegahive/hive/core/visibility.py:3-10`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/visibility.py#L3-L10)):

```text
- private: the owner (who created it) and the hive's admins (admins keep sight: auditability, no true secrets)
- shared:  additionally the people named in shared_with (principals such as user:u_ab12)
- public:  every signed-in person of this hive
...
A person who may not see something gets 'not found'
(never 'forbidden'), so its existence is not revealed. Visibility governs who sees; policy governs what minds do.
```

## Common pitfalls
- **The supervisor is inside the hive process,** not a separate service. Apps are imported into the hive process too; only the Code service is a separate daemon.
- **The policy gate is not the gateway.** One decides skills; the other decides model calls and money.
- **Belief queries stay in the caller's own swarm** ([`omegahive/hive/core/hive.py:1637-1642`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/hive.py#L1637-L1642)). Memory shares never cross swarms ([`omegahive/hive/core/shares.py:14`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/shares.py#L14)).
- **Rooms deliver deliberately.** A mind's message reaches only the minds it @mentions, and only for a few turns (default 3) before the room waits for a person ([`omegahive/hive/core/rooms.py:10-14`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/rooms.py#L10-L14)). Every delivery can cost a model call.
- **The mind sandbox is opt-in** (`HIVE_MIND_SANDBOX=1`). Deployments set it; development does not ([`omegahive/STATUS.md:54`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L54)).
- **Hive-to-hive is planned, not built.** A representative talking to a hive works. Moving a mind between hives is built but not verified live ([`omegahive/STATUS.md:71`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L71)).
- **Expect integration bugs.** These pieces have lived together for about a week ([`omegahive/STATUS.md:74`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L74)).

## Upstream
The hive is OmegaHive's own. Its native minds run OmegaClaw Core (see [the-omegaclaw-mind-loop.md](the-omegaclaw-mind-loop.md)). Outside members can join over MCP, the Model Context Protocol.

## Read next
- [`omegahive-schematics/LEGEND.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/LEGEND.md): the words used on every page.
- [`omegahive-schematics/01-system/01-system-overview.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/01-system-overview.md) and `02-hive-server-map.md`: the whole platform and its areas.
- [`omegahive-schematics/02-ask-and-ui/01-ask-and-conductor.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/01-ask-and-conductor.md): who answers the Ask.
- [`omegahive-schematics/05-governance/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/05-governance): policy, budgets, visibility and isolation.
- [`../GLOSSARY.md`](../GLOSSARY.md) for every other term.
