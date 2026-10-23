# Track: Security and privacy

**For you if** you own the threat model and the controls: sign-in, who can see what, approvals, capability tokens, sandboxing, spend limits and app isolation.

**Total time:** about 8 hours.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | Who the actors are: people, personal minds, task minds, external members and apps. |
| 2 | 60 min | Read the [threat model](https://github.com/PhysixSNET/omegahive-schematics/blob/main/09-security-and-launch/01-threat-model.md) in 09-security-and-launch. | The trust boundaries and which control covers each one. |
| 3 | 30 min | Read the card [people-and-auth](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/people-and-auth.md). | How sign-in, roles and token revocation on sign-out work ([STATUS.md:26](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 4 | 60 min | Read [Visibility, privacy and consent](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/03-visibility-and-privacy.md) and the card [visibility](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/visibility.md), then walk the tour [06: who can see what](https://github.com/PhysixSNET/omegahive/blob/main/.tours/06-who-can-see-what.tour). | Where a visibility tier is checked in code, and what happens when the check is missing. |
| 5 | 45 min | Read [Permissions, policy and approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md) and the cards [policy-and-approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/policy-and-approvals.md) and [capability-tokens-and-delegation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/capability-tokens-and-delegation.md). | How an approval is bound to the exact request. Approvals have one signer and two risk levels today ([STATUS.md:56](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 6 | 45 min | Read [Isolation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/04-isolation.md) and the cards [sandbox](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/sandbox.md) and [supervisor-and-drivers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/supervisor-and-drivers.md). | The mind sandbox is opt-in, and the Docker driver uses host networking without hardening flags ([STATUS.md:54-55](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 7 | 45 min | Read [Budgets and spend](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md) and the cards [llm-gateway-and-providers](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md) and [budgets](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/budgets.md), then walk the tour [05: a paid model call](https://github.com/PhysixSNET/omegahive/blob/main/.tours/05-a-paid-model-call.tour). | That every paid call from the hive's model and embedding clients goes through the gateway, how local-only swarms refuse outside model calls, and why a module's own connections are outside both (K27). |
| 8 | 30 min | Read the cards [app-pins](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-pins.md), [app-frame](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-frame.md) and [code-proxy](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/code-proxy.md). | How a pinned app release is checked, and what an app in the frame can reach. |
| 9 | 30 min | Read the cards [channels](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/channels.md), [mcp-interface](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/mcp-interface.md) and [federation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/federation.md). | Every path by which data leaves or enters the hive. |
| 10 | 15 min | Read the `omegahive` [SECURITY.md](https://github.com/PhysixSNET/omegahive/blob/main/SECURITY.md). | How vulnerabilities are reported and handled. |
| 11 | 60 min | Do the [disposable-hive exercise](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md) with [hello-app](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-app). | Try to make the app read another person's data or act without a grant, through the app contract only. Record what stops it. The local hive is not a security sandbox, so do anything that tries to escape the process or the OS in a disposable VM or container. |
| 12 | 30 min | Read the security part of [10-testing](https://github.com/PhysixSNET/omegahive-schematics/tree/main/10-testing). | Which tests guard each control, and which controls have no test. |

## Checkpoint

**You can now** name each trust boundary in the hive, the control that guards it, the code that enforces it and the test that proves it.

**Prove it:** pick one control (for example the visibility check on a commons query). In the sandbox with invented data, write a test that fails if the check is removed, remove the check on a scratch branch, and confirm the test fails. Then add one row to the threat model table for a gap you found, marked as a proposal.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Sign-in** ([people-and-auth](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/people-and-auth.md)): keep the built-in sign-in, or swap in your organisation's identity provider?
2. **Approvals** ([policy-and-approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/policy-and-approvals.md)): are one signer and two risk levels enough for launch, or do you need multi-signer approvals first?
3. **Tokens** ([capability-tokens-and-delegation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/capability-tokens-and-delegation.md)): keep HMAC capability tokens, or swap for your own token scheme?
4. **Sandbox** ([sandbox](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/sandbox.md)): should the mind sandbox be on by default everywhere, and should the Docker driver be hardened before launch?
5. **Visibility** ([visibility](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/visibility.md)): do the visibility tiers match your privacy policy, or do you need a different model?
6. **Outbound paths:** which channels, MCP members and federation links should be off for launch?
