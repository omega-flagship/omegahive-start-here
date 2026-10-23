# Track: Module and model integrator

**For you if** you want to plug your own technology into a mind: a skill, sense, channel or organ as a module, or your own model provider behind the gateway.

**Total time:** about 8.5 hours.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | The difference between a module (an organ for a mind) and an app (a program for the hive). |
| 2 | 60 min | Read the primer [The OmegaClaw mind loop](../primers/the-omegaclaw-mind-loop.md), then [OmegaClaw modules](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md). | The kinds of module and how a mind loads and removes one. |
| 3 | 30 min | Read the module contract [reference-omegaclaw-module-contract.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-omegaclaw-module-contract.md). | The exact interface your module must provide. |
| 4 | 45 min | Read the card [mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md), then walk the tour [04: a mind is born](https://github.com/PhysixSNET/omegahive/blob/main/.tours/04-a-mind-is-born.tour). | When modules are loaded during a mind's start, and where skill calls are dispatched. |
| 5 | 20 min | Read the cards [sandbox](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/sandbox.md) and [policy-and-approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/policy-and-approvals.md). | What your module's skills can reach, and how each skill gets an allow, ask or deny policy. |
| 6 | 75 min | Read the primer [PeTTa and SWI-Prolog](../primers/petta-and-swi-prolog.md), then do the exercise [hello-module](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-module) in the [disposable local hive](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md). | A mind calling your skill and the policy gate in front of it. |
| 7 | 45 min | Read [Models and the gateway](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/05-models-and-gateway.md) and the cards [llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md) and [budgets](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/budgets.md). | Where a provider is added, and how its cost is estimated for the worst-case budget check. |
| 8 | 45 min | Walk the tour [05: a paid model call](https://github.com/PhysixSNET/omegahive/blob/main/.tours/05-a-paid-model-call.tour). | Each step from a mind's request to the provider and back, including refusal in local-only swarms. |
| 9 | 60 min | Do the exercise [hello-model](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-model) in the sandbox. | Your provider answering a mind, with spend recorded against a budget. |
| 10 | 40 min | Read [Channels and external members](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/04-channels-and-external-members.md) and the cards [channels](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/channels.md), [mcp-interface](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mcp-interface.md) and [agent-hub](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/agent-hub.md). | When to join as an external member over MCP instead of writing a native module. |
| 11 | 30 min | Read [MODULARITY.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/MODULARITY.md) and the known issue on modules not fully ported ([STATUS.md:76](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). | Which seams are clean today and which modules are untested against this hive. |

## Checkpoint

**You can now** add a module to a mind, put its skills behind the policy gate, add a model provider behind the gateway with a cost estimate, and choose between a native module and an external member.

**Prove it:** in the sandbox, replace the hello-model provider with a stub of your own model that returns a fixed reply. Point a scratch mind at it, set a small budget, make calls until the budget refuses the next one, and show the refusal happened before the call, not after.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Module seam** ([mind-runtime](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-runtime.md)): is the module contract the right seam for your technology, or do you need to replace the mind runtime itself?
2. **Gateway** ([llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md)): keep the gateway and add your providers, or route model calls through your own platform behind the same interface?
3. **Budgets** ([budgets](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/budgets.md)): does the worst-case budget check fit your pricing model?
4. **Native or external** ([mcp-interface](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mcp-interface.md)): should your agents join as native minds or as external members?
5. **Memory** ([mind-memory](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mind-memory.md)): keep the default embedder, which is `mock/hash` in the hive ([STATUS.md:52](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)), or swap in your own?
