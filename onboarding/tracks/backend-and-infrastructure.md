# Track: Backend and infrastructure

**For you if** you run the hive server: its request handling, its state, the supervisor that runs minds, the model gateway, and its deployments.

**Total time:** about 8.5 hours.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | One hive owns one data directory; what lives in it. |
| 2 | 45 min | Read [System overview](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/01-system-overview.md) and [Hive server map](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/02-hive-server-map.md). | The server areas and which `hive/core` modules belong to each. |
| 3 | 45 min | Read [State and storage](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/03-state-and-storage.md) and the cards [sqlite-state](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/sqlite-state.md) and [events](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/events.md). | Which tables exist, who owns each, and how events are delivered. |
| 4 | 60 min | Read [Request lifecycle](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/04-request-lifecycle.md), then walk the tour [01: follow an Ask request](https://github.com/PhysixSNET/omegahive/blob/main/.tours/01-follow-an-ask-request.tour). | Every hop from the browser to a mind and back, and where auth and policy run. |
| 5 | 75 min | Read the primer [The OmegaClaw mind loop](../primers/the-omegaclaw-mind-loop.md), then [Supervisor, drivers and sandbox](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/02-supervisor-drivers-sandbox.md) and the cards [supervisor-and-drivers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/supervisor-and-drivers.md) and [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md), then walk the tour [04: a mind is born](https://github.com/PhysixSNET/omegahive/blob/main/.tours/04-a-mind-is-born.tour). | How a mind process is started, watched and stopped, and how Off, Wake all and Stop all use a durable snapshot. |
| 6 | 40 min | Read [Models and the gateway](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/05-models-and-gateway.md) and the cards [llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md) and [budgets](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/budgets.md). | The path for the hive's configured model and embedding calls, why module egress is outside it (K27), and the worst-case budget check before each paid call. |
| 7 | 60 min | Read the primer [MORK and DAS](../primers/mork-and-das.md), then [Federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/04-federation.md) and the cards [federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md), [mcp-interface](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mcp-interface.md) and [agent-hub](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/agent-hub.md). | What links to other hives and external members today. Full hive-to-hive linking is not built yet ([STATUS.md:71](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 8 | 45 min | Read the deploy [RUNBOOK.md](https://github.com/PhysixSNET/omegahive/blob/main/deploy/RUNBOOK.md) and [hive.env.example](https://github.com/PhysixSNET/omegahive/blob/main/deploy/hive.env.example). | Every setting a deployment needs, and which ones must agree with each other. |
| 9 | 30 min | Read [MODULARITY.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/MODULARITY.md). | Where the coupling is high and what to split first. |
| 10 | 90 min | Read the primer [PeTTa and SWI-Prolog](../primers/petta-and-swi-prolog.md), follow the [disposable local hive setup](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md) and run the hive server suite on a clean clone with a scratch data directory (`python -m pytest -q hive/tests`, [STATUS.md:15](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). | Your count against the recorded one. Run one heavy suite at a time. |
| 11 | 30 min | Read the operations parts of the launch checklist in [09-security-and-launch](https://github.com/PhysixSNET/omegahive-schematics/tree/main/09-security-and-launch). | Backups, restarts, sign-in checks after restart and rollback. |

## Checkpoint

**You can now** start a hive on a scratch data directory, trace one request through the server, name the tables it touches, and explain how minds are supervised and how model calls are metered.

**Prove it:** on a scratch hive with invented data, add one read-only endpoint that returns the count of minds in a swarm. Put the auth and visibility checks in the same place the existing endpoints do, add a test for it, and run only the tests for the area you changed plus a smoke test.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **State** ([sqlite-state](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/sqlite-state.md)): keep SQLite in one data directory per hive, or swap in your own database? What changes for backups and for more than one server?
2. **Events** ([events](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/events.md)): keep the built-in event delivery, or swap for your message bus?
3. **Supervisor** ([supervisor-and-drivers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/supervisor-and-drivers.md)): keep the current drivers, or run minds under your own scheduler or orchestrator?
4. **Gateway** ([llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md)): keep it, or put your own model routing behind the same interface?
5. **Federation** ([federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md)): build hive-to-hive linking on the current design, or on your own network layer?
6. **Deployment:** which settings should be derived from one source so they cannot drift apart?
