# Track: App owner

**For you if** you own one app repo (for example Tools, Planner, Library, Studio, Code, Fusion, Social, Purple, Atlas or Truth) and need to know exactly how it plugs into the hive and what you must keep stable.

**Total time:** about 7.5 hours.

**Note on tiers:** if your app is closed-tier, its internals are described only in your own repo's `docs/schematics/`. The open schematics show it as a named box and its connection to the hive.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | What an app (program) is, and how it differs from a module. |
| 2 | 60 min | Read the primer [The programs contract](../primers/the-programs-contract.md), then [Programs contract: describe, view, act](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/01-programs-contract.md), then the contract itself, [hive/PROGRAMS.md](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md). | The three calls your app must answer and the shapes it must return. |
| 3 | 40 min | Read [App lifecycle](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md) and the card [programs-host](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/programs-host.md). | Discovery, homes, activations and grants, in order. |
| 4 | 30 min | Read the card [app-pins](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-pins.md). | How a digest-pinned release (`HIVE_APP_PINS`) is loaded, and why the hive loads releases, not working folders. |
| 5 | 40 min | Read [Connect a new app: a worked example](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/03-connect-a-new-app.md). | Each step from an empty repo to an app running in a swarm. |
| 6 | 20 min | Read your own app's page in [06-apps/apps](https://github.com/PhysixSNET/omegahive-schematics/tree/main/06-apps/apps). | What the hive expects from your app today, and its listed seams. |
| 7 | 45 min | Walk the tour [03: an app action, click to result](https://github.com/PhysixSNET/omegahive/blob/main/.tours/03-an-app-action-click-to-result.tour). | Where the hive checks the grant and the exact request before your app sees it. |
| 8 | 30 min | Read the cards [app-frame](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-frame.md) and [code-proxy](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/code-proxy.md). | How your view is hosted and what it can call. |
| 9 | 40 min | Read the cards [policy-and-approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/policy-and-approvals.md), [capability-tokens-and-delegation](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/capability-tokens-and-delegation.md) and [visibility](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/visibility.md). | Which of your actions need an approval, and what your app may show to whom. |
| 10 | 90 min | Do the exercise [hello-app](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-app) in the [disposable local hive](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md), and check it with [programs_check.py](https://github.com/PhysixSNET/omegahive/blob/main/hive/programs_check.py). | A passing contract check, a pinned release and one action from the frame. |
| 11 | 20 min | Read the known issue on deploying an app with its swarm ([STATUS.md:67](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)) and the app part of the launch checklist in [09-security-and-launch](https://github.com/PhysixSNET/omegahive-schematics/tree/main/09-security-and-launch). | The settings that must agree (pin, swarm, home, grants) and how you will check they do. |

## Checkpoint

**You can now** explain the programs contract, pin a release of your app, give it a home and grants in a swarm, and trace one action from a click to your app's result.

**Prove it:** in the sandbox, add one new action to hello-app that needs an approval. Pin a new release, give it a grant in a scratch swarm, trigger the action from the frame, approve it once, and show that the same action with different arguments asks again.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Contract** ([programs-host](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/programs-host.md)): does describe, view and act cover what your app needs, or do you need a contract change? Who must agree to it?
2. **Hosting** ([app-frame](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-frame.md)): keep your view inside the hive frame, or run your own front end against the hive API?
3. **Release** ([app-pins](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-pins.md)): keep digest pins, or swap for your own release and signing process?
4. **Your app's own parts:** for each part of your app, keep it, or replace it with an existing team service behind the same contract?
5. **Deploy flow:** what would a one-step "deploy app into swarm" flow need to check before you would trust it?
