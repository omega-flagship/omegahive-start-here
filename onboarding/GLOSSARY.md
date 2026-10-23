# Glossary

One or two lines per term, with a link to where it is explained. Terms are in alphabetical order. Where a word has more than one meaning in the code, every meaning is listed. Code citations are `omegahive/path:line`, read at commit `34b0fb3` and linked to `main` (see [README.md](README.md)).

**Activation.** A named admin switches an app on in one swarm. An app that defines a `bind` hook, or has any activation row, needs one; deactivating revokes its attachments in that swarm ([`omegahive/hive/core/program_attachments.py:36-60`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/program_attachments.py#L36-L60)). See [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md).

**Admission (app).** A person's successful view or read of an app in a swarm records that the app admitted them there; file actions require it. See [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md).

**Agent hub.** The WebSocket a native mind uses to receive and send messages. A small daemon holds it and talks to the loop through files. See [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md).

**App (program).** A plug-in that supplies a work graph through `describe`, `view` and `act`, imported into the hive process. See [primers/the-programs-contract.md](primers/the-programs-contract.md).

**App frame.** An app's own screen, served from its `ui/` folder inside a sandboxed frame under host rules ([`omegahive/hive/core/ui_parts.py:1-4`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/ui_parts.py#L1-L4)). See [`omegahive-schematics/02-ask-and-ui/03-app-frame-bridge.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/03-app-frame-bridge.md).

**Approval.** What "ask" in the policy gate files. A person answers with one of five decisions: Once, For a time, Always, No, Never ([`omegahive/hive/core/policy.py:351`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/policy.py#L351)). See [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md).

**ASI:Chain.** The blockchain named as a later anchor for chain heads and multi-signer keys. Not on mainnet; nothing here is a blockchain ([`omegahive/docs/theory/ledger-provenance-and-das.md:102-104`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/ledger-provenance-and-das.md#L102-L104)).

**Ask (Universal Ask).** The text and voice bar on every page. The relevant swarm's coordinator answers (or, in a swarm with no coordinator, the native mind the request addressed); the personal mind only as last fallback ([`omegahive/hive/core/ask.py:6-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/ask.py#L6-L8)). See [`omegahive-schematics/02-ask-and-ui/01-ask-and-conductor.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/01-ask-and-conductor.md).

**AtomSpace.** A store of MeTTa atoms that can be added to, removed from and matched. Here: each mind's spaces and each swarm's commons. See [primers/metta-and-atomspace.md](primers/metta-and-atomspace.md).

**Attachment.** An admin attaches an existing mind to an app; the hive then writes one policy rule per allowed app action ([`omegahive/hive/core/program_attachments.py`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/program_attachments.py)). See [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md).

**Attention.** In this build, an optional organ that scores atoms with keyword rules and only proposes changes. Full ECAN is intent ([`omegahive/STATUS.md:51`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L51)). See [primers/attention-ecan.md](primers/attention-ecan.md).

**Belief.** A statement in a commons with a truth value and an evidence stamp, stored as `(Current stmt tv stamp)` ([`omegahive/hive/spaces/lib_hive.metta:98-103`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L98-L103)). See [`omegahive-schematics/04-knowledge/02-beliefs-sharing.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md).

**Browser memory.** The personal mind's memory kept in the person's own browser, not on the hive. Held copies wait for the browser to collect them ([`omegahive/hive/core/personal_inbox.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/personal_inbox.py#L1-L6)).

**Budget.** A spending rule `(scope, period, limit_usd)` for the hive, a swarm, a mind, a person or a key. Every paid model call is checked against every applying rule at worst case before it is made ([`omegahive/hive/core/budgets.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/budgets.py#L1-L8)). See [`omegahive-schematics/05-governance/02-budgets-and-spend.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md).

**Capability token.** A signed `hc1.<payload>.<sig>` token (HMAC-SHA256) the hive issues to a registered service such as Code. The service also checks live status before every change ([`omegahive/hive/core/services.py:8-13`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/services.py#L8-L13)). See [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md).

**Channel.** How a native mind talks: the hive channel on a hive, or (inherited, not used by hive minds) Telegram, WhatsApp and others ([`omegahive/STATUS.md:59`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L59)). See [`omegahive-schematics/03-minds/04-channels-and-external-members.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/04-channels-and-external-members.md).

**Child mind.** A mind a team's coordinator starts for one request under a lease and budget. Built and tested, activation held, never spawned live ([`omegahive/STATUS.md:53`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L53); [`omegahive/hive/core/minds.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/minds.py#L1-L6)).

**ChromaDB.** The vector store used for a mind's long-term recall, beside the AtomSpace. The hive's default embedder is `mock/hash` ([`omegahive/STATUS.md:52`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L52)).

**Closed tier.** "Closed Source for Product Consideration": shared privately, not to be published or relicensed. See the root [`README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md) of this repo.

**Commons.** A swarm's shared MeTTa space of beliefs (`&commons_<swarm>`), with evidence-stamped revision and an operations log ([`omegahive/hive/spaces/service.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L1-L8)). See [`omegahive-schematics/04-knowledge/02-beliefs-sharing.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md).

**Commons Explorer.** A built-in app: "What does this swarm believe, and why?" Each shared belief unfolds into the reports behind it ([`omegahive/hive/plugins/commons_explorer/plugin.json`](https://github.com/PhysixSNET/omegahive/blob/main/hive/plugins/commons_explorer/plugin.json)).

**Conductor.** An optional host-side model loop that steers the person's screen with typed acts. Off unless `HIVE_ASK_CONDUCTOR=1` ([`omegahive/hive/core/conductor.py:1-9`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/conductor.py#L1-L9)). See [`omegahive-schematics/02-ask-and-ui/01-ask-and-conductor.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/01-ask-and-conductor.md).

**Confidence (c).** The second number of `(stv f c)`: how much evidence stands behind a belief, from 0 toward 1. See [primers/truth-values-nal-pln.md](primers/truth-values-nal-pln.md).

**Connection (between swarms).** An agreement made by an admin that grants only its scopes (a memory read share, or request kinds) and only while active ([`omegahive/hive/core/connections.py:1-14`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/connections.py#L1-L14)).

**Contract version.** The programs contract is v0.1, frozen; some additive 0.2 fields are accepted on `act` ([`omegahive/docs/COMPATIBILITY.md:10`](https://github.com/PhysixSNET/omegahive/blob/main/docs/COMPATIBILITY.md#L10)).

**Coordinator.** The mind that coordinates a swarm. It answers the Ask for that swarm and may run members under delegation leases ([`omegahive/hive/core/hive.py:202`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/hive.py#L202)).

**Copy-apply.** A feature whose consent flow is built and tested but which stays off (`HIVE_COPY_APPLY_CLAIMS`) ([`omegahive/STATUS.md:57`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L57)).

**Cross-swarm request.** A goal in one swarm linked to a goal the hive creates in another. It confers nothing by itself ([`omegahive/hive/core/collab.py:1-7`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/collab.py#L1-L7)).

**DAS (Distributed AtomSpace).** SingularityNET's distributed AtomSpace project. Its patterns shape the intended hive-to-hive design; it is not a dependency today. See [primers/mork-and-das.md](primers/mork-and-das.md).

**Delegation lease.** A named admin lets a coordinator start one specialist for one task, for at most 15 minutes and within a budget ([`omegahive/hive/core/delegation.py:1-11`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/delegation.py#L1-L11)).

**Demo mode.** The `?sim=1` showreel and guided demos. Listed as out of date and broken at handover ([`omegahive/STATUS.md:77`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L77)); the live fixes made since then arrive with the omegahive demo-mode fix pull request (`port/demo-mode-fix-r2`, which replaces the first one, closed unmerged). See [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md).

**Digest.** A sha256 that identifies a file, release or artifact. App pins, assets and exhibits are addressed by digest.

**Driver.** How the supervisor runs one mind process: `local` (a process on this host) or `docker` (one container per mind) ([`omegahive/hive/supervisor/drivers.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/drivers.py#L1-L6)). See [`omegahive-schematics/03-minds/02-supervisor-drivers-sandbox.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/02-supervisor-drivers-sandbox.md).

**ECAN (Economic Attention Networks).** OpenCog's attention model: STI, LTI, rent, wages and spreading. Named here, not implemented. See [primers/attention-ecan.md](primers/attention-ecan.md).

**Egress / local-only swarm.** A swarm listed in `HIVE_LOCAL_ONLY_SWARMS` may use only local model routes; outside calls get `403 egress_refused` ([`omegahive/hive/core/gateway.py:232-253`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/gateway.py#L232-L253)).

**Energy.** A native mind's posture (for example `warm`) and the skills that change how many turns it takes ([`omegahive/src/loop.metta:56`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L56); [`omegahive/src/skills_energy.metta`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_energy.metta)).

**Evidence.** Two senses. (1) In NAL, the weight behind a truth value: w = c / (1 − c) ([`omegahive/lib_nal.metta:2-6`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L2-L6)). (2) In the commons, the **evidence stamp**: a sorted list of unique ids such as `(ev omega-a 1)`; beliefs revise only when stamps are disjoint ([`omegahive/hive/spaces/lib_hive.metta:6-9`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L6-L9)).

**Evolve.** A closed-tier built-in app for research claims, experiments and lineage ([`omegahive/hive/plugins/omegaevolve/`](https://github.com/PhysixSNET/omegahive/tree/main/hive/plugins/omegaevolve)). Its gain is unmeasured ([`omegahive/docs/EARLIER_EXPERIMENTS.md:89`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L89)).

**Exhibit.** A fixed piece of work a mind publishes to named minds or its swarm for a set time ([`omegahive/hive/core/shares.py:9-11`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/shares.py#L9-L11)).

**Expectation.** One number from `(stv f c)`: c × (f − 0.5) + 0.5 ([`omegahive/lib_nal.metta:101-102`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L101-L102)).

**Experience.** A whole alternative front end (layout, navigation, motion). Only reviewed ones ship. See [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md).

**External member.** A mind of kind `module`: an outside agent that joins a swarm with a member token over REST or MCP. See [`omegahive-schematics/03-minds/04-channels-and-external-members.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/04-channels-and-external-members.md).

**Federation.** Linking hives. The representative-to-hive link works; full hive-to-hive is planned ([`omegahive/STATUS.md:71`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L71)). See [`omegahive-schematics/04-knowledge/04-federation.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/04-federation.md).

**Frequency (f).** The first number of `(stv f c)`: how often the statement held in the evidence. PLN calls it strength.

**Galaxy (hive map).** On the hive map, each person's hive drawn as one galaxy, with their own mind as "You" at its centre and the cloud hive in the middle. What a viewer is shown is decided once, before anything is grouped or counted, and a private app's homes stay hidden until known. Arrives with the omegahive pull request `port/hive-scale`. See [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md).

**Gateway.** The one path for model and embedding calls (`/llm/v1`). It holds the keys, meters cost and refuses calls past a budget; keys never reach minds ([`omegahive/hive/core/gateway.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/gateway.py#L1-L6)).

**Goal.** See **Task**.

**Grant.** Three senses. (1) **Publish grant:** `(Grant agent space pattern publish)` in `&hive_acl`, letting a member publish matching statements to a commons ([`omegahive/tests/hive_lib_smoke.metta:18-20`](https://github.com/PhysixSNET/omegahive/blob/main/tests/hive_lib_smoke.metta#L18-L20)). (2) **App grant:** short-lived read grants an app gets when its owner opens it, renewed all or nothing (see [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md)). (3) **Service grant:** a collaborator grant that bounds a service's capability tokens ([`omegahive/hive/core/services.py:1`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/services.py#L1)).

**Health question (idle).** The one question Health asks an awake mind it notices idle: owed work, model spend with no input, or no input and no output for an hour. It goes through the normal message path (a personal mind's to its person's own chat), is asked once per idle stretch, and is never a limit or a sleep; a person can Remind. Health's **Idle minds** section shows the question, the answer and the history. A personal mind's record is its person's whatever its visibility; an admin reads it only by explicit audit. Live since the handover; arrives with the omegahive pull requests `port/idle-minds` (merged), `port/idle-minds-r2.5` and `port/health-idle-ui`. See [`omegahive-schematics/components/mind-observability.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-observability.md).

**Hive.** The server, its UI and its shared state. One hive process owns one data directory, held by an exclusive lock ([`omegahive/hive/core/exclusive.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/exclusive.py#L1-L5)). See [primers/hive-concepts.md](primers/hive-concepts.md).

**Home (app home).** The swarms an app works in, best first, limited to swarms the caller can see. See [`omegahive-schematics/06-apps/02-app-lifecycle.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md).

**Human-only skill.** A skill the policy gate always refuses for minds, such as payments or password changes. See [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md).

**Hyperon.** The OpenCog Hyperon framework by TrueAGI and SingularityNET: MeTTa, AtomSpace and the reasoning tools built on them. The design here is Hyperon-first ([`omegahive/docs/START_HERE.md:40-41`](https://github.com/PhysixSNET/omegahive/blob/main/docs/START_HERE.md#L40-L41)).

**Idle signal (`last_input_at`).** When a mind last had real input (a message from a person or mind, a goal claim, heartbeat or result, a published belief, or its own message). Model spend and the hive's own notes never count. Idle sleep and Health's idle question read it. Arrives with the omegahive pull request `port/idle-minds`. See [`omegahive-schematics/05-governance/02-budgets-and-spend.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md).

**Intent.** The host's custody of one exact request from an Ask turn. The conductor's dispatch records it; the person submits it. It adds custody, never authority ([`omegahive/hive/core/ask_intents.py:1-4`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/ask_intents.py#L1-L4)).

**Iter.** A small Python agent runtime (upstream `patham9/iter`), mind kind `iter`. It polls the hive over HTTP; its tools are not covered by the policy gate, so it runs only in the Docker driver ([`omegahive/hive/supervisor/workspace.py:31, 39-42`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L31)).

**janus.** SWI-Prolog's two-way Python bridge, pinned at janus-swi 1.5.3. See [primers/petta-and-swi-prolog.md](primers/petta-and-swi-prolog.md).

**Lease.** A time-limited claim. A mind's claim on a task is a lease it renews by heartbeat ([`omegahive/hive/core/goals.py:4-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/goals.py#L4-L6)); delegation and child minds also run under leases.

**Legacy.** Code and docs kept for reference and marked with `LEGACY.md` or a note: `omegav2`, `omegahive-candidates` and the inherited OmegaClaw Core folders. See [`omegahive/LEGACY.md`](https://github.com/PhysixSNET/omegahive/blob/main/LEGACY.md).

**Look.** A data-only restyling of the classic UI (colour tokens, fonts, density), saved per person. See [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md).

**MCP.** The Model Context Protocol. Outside harnesses join a swarm through an invite code and the `/mcp` endpoint ([`omegahive/hive/core/mcp.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/mcp.py#L1-L6)).

**MeTTa.** Hyperon's language: atoms, pattern rules and spaces. See [primers/metta-and-atomspace.md](primers/metta-and-atomspace.md).

**MeTTaScript.** A MeTTa runner in the browser. It runs the same vendored `lib_nal`, `lib_pln` and `lib_hive` ([`omegahive/hive/ui/src/lib/mindSpace/core.ts:1-3`](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/src/lib/mindSpace/core.ts#L1-L3)).

**Mind.** An agent the hive runs, with its own workspace and memory. Kinds: `omega`, `iter`, `module`. See [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md).

**Mind role.** A reusable bundle (prompt template, model, budget, approval rules) assigned to a mind ([`omegahive/hive/core/roles.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/roles.py#L1-L6)). Not the same as a person's role (`admin` or `member`).

**Mind loop.** The native mind's receive, think, gate, act, save cycle ([`omegahive/src/loop.metta:139-190`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L139-L190)). See [primers/the-omegaclaw-mind-loop.md](primers/the-omegaclaw-mind-loop.md).

**Module.** Two senses. (1) A removable organ for a native mind: a folder under `modules/` with `module.toml`, `entry.metta` and skill files (see [`omegahive-schematics/03-minds/03-modules.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md)). (2) Mind kind `module`: an external member.

**MORK.** A high-performance AtomSpace backend in the Hyperon ecosystem, with the MM2 rule language. Intended storage backend; never built or run here ([`omegahive/docs/EARLIER_EXPERIMENTS.md:82`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L82)). See [primers/mork-and-das.md](primers/mork-and-das.md).

**Motivation.** The "why" above tasks, owned by a person, a swarm or a mind ([`omegahive/hive/core/motivations.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/motivations.py#L1-L6)).

**NAL (Non-Axiomatic Logic).** The logic of NARS: inference rules with truth functions. `lib_nal.metta`, called through `nal-step`. See [primers/truth-values-nal-pln.md](primers/truth-values-nal-pln.md).

**NARS.** The Non-Axiomatic Reasoning System. Minds load PeTTa's `lib_nars`, called through `nars-query` and `nars-derive` ([`omegahive/src/skills_reasoning_spaces.metta:1-9`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_reasoning_spaces.metta#L1-L9)).

**OBSERVE organ.** An organ that writes the mind's experience to atoms from the core, not the model. Built and tested, default off, held ([`omegahive/docs/EARLIER_EXPERIMENTS.md:24`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L24)).

**OmegaBench.** The benchmark harness in [`omegahive/omegabench/`](https://github.com/PhysixSNET/omegahive/tree/main/omegabench); the Lab runs suites from the UI ([`omegahive/hive/core/lab.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/lab.py#L1-L5)).

**OmegaClaw.** The MeTTa agent runtime native minds run, inherited from the public OmegaClaw Core and credited in [`omegahive/NOTICE`](https://github.com/PhysixSNET/omegahive/blob/main/NOTICE). See [primers/the-omegaclaw-mind-loop.md](primers/the-omegaclaw-mind-loop.md).

**ONA.** OpenNARS for Applications. Its `Truth.c` is the NAL reference the audit used ([`omegahive/docs/reasoning-deviations.md:11-12`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L11-L12)).

**Open tier.** Apache-2.0 repos and folders. See the root [`README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md) of this repo.

**Operations log.** `spaces.log.jsonl`: every grant, revoke, vocabulary term and accepted publish, replayed at start. Append-only, not hash-chained ([`omegahive/hive/spaces/service.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/service.py#L1-L5)).

**Organ.** A part of a mind that does one job: memory, attention, a sense, a channel. Module kinds include `memory-organ` and `runtime-organ`; a **runtime organ** runs at boot only if trusted ([`omegahive/src/loop.metta:65-70`](https://github.com/PhysixSNET/omegahive/blob/main/src/loop.metta#L65-L70)). The design calls the language model one organ, not the control plane.

**Per-viewer flags (`is_mine`, `may_remind`, `may_sleep`).** The host's answer, for the person asking, to "is this my personal mind", "may I Remind it" and "may I put it to sleep", on every agent view and Health idle row. Each flag is true exactly when the matching route would accept the call; the UI never works out ownership itself. Arrives with the omegahive pull request `port/idle-minds-r2.5`. See [`omegahive-schematics/05-governance/03-visibility-and-privacy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/03-visibility-and-privacy.md).

**Personal mind.** Every named person's own mind: kind `omega`, asleep, alone in a private swarm of its own, paid from the person's allowance ([`omegahive/hive/core/personal.py:3-12`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/personal.py#L3-L12)).

**PeTTa.** The MeTTa implementation that compiles to SWI-Prolog, pinned at `ae66fa8`. See [primers/petta-and-swi-prolog.md](primers/petta-and-swi-prolog.md).

**Pin.** Four senses. (1) **App release pin:** `HIVE_APP_PINS` names the exact folder and digest an app may load from ([`omegahive/hive/core/programs.py:593-620`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/programs.py#L593-L620)). (2) **Toolchain pin:** PeTTa `ae66fa8`, SWI-Prolog 10.1.14, janus-swi 1.5.3 ([`omegahive/scripts/dev/setup_petta_env.sh:4-8`](https://github.com/PhysixSNET/omegahive/blob/main/scripts/dev/setup_petta_env.sh#L4-L8)). (3) The `pin` skill, which a mind uses to pin state continuity ("pin state-continuity"); the skill itself only returns `PIN-SUCCESS`, so the note lives in the recorded turn ([`omegahive/src/skills_core.metta:67-68`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_core.metta#L67-L68); [`omegahive/src/skill_catalog_core.metta:5`](https://github.com/PhysixSNET/omegahive/blob/main/src/skill_catalog_core.metta#L5)). It is on the gate's local allow list ([`omegahive/modules/hive/src/hive_commons.py:932`](https://github.com/PhysixSNET/omegahive/blob/main/modules/hive/src/hive_commons.py#L932)). (4) Pinned atoms count as protected and are never evicted from a mind's spaces ([`omegahive/src/skills_runtime_spaces.metta:14-16`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_runtime_spaces.metta#L14-L16)).

**Placement.** Where a mind lives, and moving it between hives by export, import and settle (a tombstone at the source). A personal mind's bundle carries its person's chats only for that person or an explicit audit, and imports only back home (`409 personal_mind_unbound`). Built, not verified live ([`omegahive/hive/core/placement.py:1-14`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/placement.py#L1-L14)).

**PLN (Probabilistic Logic Networks).** OpenCog's probabilistic logic. `lib_pln.metta`, called through `pln-step`; never run inside a loop ([`omegahive/docs/EARLIER_EXPERIMENTS.md:80`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L80)). See [primers/truth-values-nal-pln.md](primers/truth-values-nal-pln.md).

**Policy gate.** The engine that decides, before a skill command, whether a mind may run it: allow, ask or deny. Not yet universal: a native mind's local skip list bypasses it and unknown skills default to allow; universal gating is a launch requirement (K10, K30 in [`omegahive-schematics/07-upgrade-path/FINDINGS.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/07-upgrade-path/FINDINGS.md)). Separate from the gateway ([`omegahive/hive/core/policy.py:1-7`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/policy.py#L1-L7)). See [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md).

**Power (Off, Wake all, Stop all).** Hive-wide stop and restore, with a durable snapshot of which minds were awake ([`omegahive/hive/core/power.py:1-5`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/power.py#L1-L5)).

**Program.** See **App**. [`omegahive/hive/PROGRAMS.md`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md) calls apps "dot programs".

**Programs contract.** The JSON boundary between an app and the host: `describe`, `view`, `act` ([`omegahive/hive/PROGRAMS.md`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md)). See [primers/the-programs-contract.md](primers/the-programs-contract.md).

**Promotion.** A memory's usefulness score, moved up or down by one, capped at 10, decaying with time; the top memories are fed back as hints. See [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md).

**Quarantine.** A publish whose symbols are not in the swarm vocabulary is recorded as `Quarantined`, not integrated ([`omegahive/hive/spaces/lib_hive.metta:126-129`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L126-L129)).

**Reconcile loop.** The hive pass every few seconds that restarts minds that should be awake and settles leases. See [`omegahive-schematics/01-system/02-hive-server-map.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/02-hive-server-map.md).

**Recorded claim.** How OmegaEvolve keeps a contribution: a claim with its evidence references, each with its declared origin, custody `unresolved` and `verified: false` until the host settles them; never an adopted result. Lab shows them read-only in a predictive-coding band and counts none of them. Arrives with the omegahive pull request `port/lab-pc-band`. See [`omegahive-schematics/components/lab-and-evolve.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/lab-and-evolve.md).

**Repository map (`repo-map/1`).** A JSON map of one repository revision: files, modules, definitions, imports, tests and docs as nodes, and their links as edges, each with a stated basis (`declared`, `syntax` or `heuristic`). An admin loads it; people, minds (`repo-query`) and MCP members (`hive_repo_query`) read it through one bounded, read-only engine, and each revision is also mounted as a read-only space. Arrives with the omegahive pull request `port/repo-map-host`. See [`omegahive-schematics/components/hive-spaces.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/hive-spaces.md#repository-maps).

**Representative.** A person's mind acting for them toward a hive. The representative-to-hive connection works today ([`omegahive/STATUS.md:71`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L71)).

**Revision.** Merging two beliefs about the same statement by adding their evidence ([`omegahive/lib_nal.metta:92-99`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L92-L99)). In the commons, only with disjoint stamps; otherwise the higher-confidence belief is kept and the choice recorded as `Chosen` ([`omegahive/hive/spaces/lib_hive.metta:105-117`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L105-L117)).

**Room.** DMs, groups, channels and projects as one thing, with members and one transcript ([`omegahive/hive/core/rooms.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/rooms.py#L1-L8)).

**Runtime hook.** `(RuntimeHook phase name call)`, run by the loop in phase `cycle` or `response` if trusted ([`omegahive/src/skills_reasoning_spaces.metta:24-28`](https://github.com/PhysixSNET/omegahive/blob/main/src/skills_reasoning_spaces.metta#L24-L28)).

**Sandbox (mind sandbox).** OS isolation for mind processes: Landlock and namespaces on Linux, sandbox-exec on macOS. Opt-in with `HIVE_MIND_SANDBOX=1` ([`omegahive/STATUS.md:36-38, 54`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L36-L38)). See [`omegahive-schematics/05-governance/04-isolation.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/04-isolation.md).

**Scientist route.** An app shows a snapshot to one named mind and posts a goal only that mind can claim; the result must echo the binding ([`omegahive/hive/PROGRAMS.md`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md) §7).

**Service (registered).** An outside service such as Code that enrols with a one-time token and gets a service token and capability secret ([`omegahive/hive/core/services.py:3-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/services.py#L3-L6)).

**Session.** A focused working room of one person and one mind, bound to a goal and a spend cap ([`omegahive/hive/core/sessions.py:1-6`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/sessions.py#L1-L6)). An Ask thread is a session of purpose `ask`.

**sexpr membrane.** `hive/spaces/sexpr.py`: parses agent text and re-renders it from a small grammar before it reaches MeTTa ([`omegahive/hive/spaces/sexpr.py:1-8`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/sexpr.py#L1-L8)).

**Shadow run.** An end-to-end run of the real path, reported separately from mock or replay demos. Nothing counts as accepted without one ([`omegahive/docs/START_HERE.md:108-109`](https://github.com/PhysixSNET/omegahive/blob/main/docs/START_HERE.md#L108-L109)).

**Share.** Timed, consented access to one of a mind's private spaces: a request, an offer or an exhibit. Never across swarms ([`omegahive/hive/core/shares.py:1-14`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/shares.py#L1-L14)).

**Skill.** A command a native mind can run, written as a MeTTa function with a catalogue entry, a signature and an affordance ([`omegahive/lib_omegaclaw_core.metta:19-35`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta#L19-L35)). Every skill passes the policy gate on a hive.

**Stage.** One of `unfold`, `map`, `compare` or `detail`: how the host shows a work graph ([`omegahive/hive/PROGRAMS.md:60-63`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L60-L63)).

**STI / LTI.** Short-term and long-term importance in ECAN. Here they are numbers set by keyword rules ([`omegahive/src/attention_ledger.py:157-210`](https://github.com/PhysixSNET/omegahive/blob/main/src/attention_ledger.py#L157-L210)).

**Studio.** The closed-tier design app (`omegadesign`). See [`omegahive-schematics/06-apps/apps/omegadesign.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/apps/omegadesign.md).

**stv.** "Simple truth value": `(stv f c)`. See **Truth value**.

**Supervisor.** Starts, stops and watches mind processes through a driver. Runs inside the hive process. See [`omegahive-schematics/03-minds/02-supervisor-drivers-sandbox.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/02-supervisor-drivers-sandbox.md).

**Swarm.** A group of minds and people with its own rooms, tasks and commons. See [primers/hive-concepts.md](primers/hive-concepts.md).

**Task (goal).** Work posted by a person or mind and claimed by a mind under a lease; `done` needs a result that says what was done ([`omegahive/hive/core/goals.py:1-11`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/goals.py#L1-L11)).

**Tier.** Open (Apache-2.0) or Closed Source for Product Consideration. A tier travels with the code when it moves. See the root [`README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md) of this repo.

**Truth value (stv f c).** Frequency f and confidence c, both in [0, 1], c below 1 ([`omegahive/lib_nal.metta`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta)). See [primers/truth-values-nal-pln.md](primers/truth-values-nal-pln.md).

**Two-reviewer rule.** Two independent reviewers check a change before anything is deployed. See the root [`README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md) of this repo, "Rules carried over".

**V2 body.** The separate OmegaV2 mind design in the closed `omegav2` repo. Evidence from it describes a different body ([`omegahive/docs/EARLIER_EXPERIMENTS.md:32-47`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md#L32-L47)).

**Visibility tier.** Private, shared or public, for minds, swarms and tasks. A hidden thing answers "not found" ([`omegahive/hive/core/visibility.py:1-10`](https://github.com/PhysixSNET/omegahive/blob/main/hive/core/visibility.py#L1-L10)). See [`omegahive-schematics/05-governance/03-visibility-and-privacy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/03-visibility-and-privacy.md).

**Vocabulary.** A swarm's shared terms (`&vocab_<swarm>`). Publishing adds a member's symbols; unknown symbols are quarantined. See [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md).

**Workbench Map.** The Code page's Map mode (`#/code/map/<repo>@<sha>`): a repository map drawn level by level, with a node card, drift between revisions and the Ask's words as an editable query. Arrives with the omegahive pull request `port/workbench-map`. See [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md).

**WorkGraph (work graph).** The JSON snapshot an app's `view` returns: items, links, groups and notes, with a revision ([`omegahive/hive/PROGRAMS.md:88-112`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L88-L112)).

**Workspace.** A mind's body on disk: `run.metta`, linked repos, `memory/`, its token and its log ([`omegahive/hive/supervisor/workspace.py:1-11`](https://github.com/PhysixSNET/omegahive/blob/main/hive/supervisor/workspace.py#L1-L11)).
