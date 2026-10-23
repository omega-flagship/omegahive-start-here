# Track: Product and launch

**For you if** you decide what ships, what is held, and what must be true before a secure, safe, tested launch. This track has no coding; the exercises are reading and deciding.

**Total time:** about 6 hours.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | The product in one picture: people, personal minds, swarms, apps. |
| 2 | 15 min | Read the [start-here README](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md). | The two tiers (open and closed), which repos are current and which are legacy. |
| 3 | 45 min | Read the `omegahive` [STATUS.md](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md) and [FEATURES.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/FEATURES.md). | Each feature's state: works, limited, deliberately off or known broken. |
| 4 | 30 min | Read [System overview](https://github.com/PhysixSNET/omegahive-schematics/blob/main/01-system/01-system-overview.md). | Solid parts are built; dashed parts are intended only. |
| 5 | 45 min | Read [App lifecycle](https://github.com/PhysixSNET/omegahive-schematics/blob/main/06-apps/02-app-lifecycle.md) and skim the app pages in [06-apps/apps](https://github.com/PhysixSNET/omegahive-schematics/tree/main/06-apps/apps). | Which apps ran on the hive from their own repos ([STATUS.md:39](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)), and how hard it is to deploy an app with its swarm ([STATUS.md:67](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 6 | 40 min | Read [Budgets and spend](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md) and [Visibility, privacy and consent](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/03-visibility-and-privacy.md). | What a person is promised about spend and about who sees their data. |
| 7 | 60 min | Read the threat model and launch checklist in [09-security-and-launch](https://github.com/PhysixSNET/omegahive-schematics/tree/main/09-security-and-launch). | Each checklist item, who owns it, and its current state. |
| 8 | 30 min | Read the test map in [10-testing](https://github.com/PhysixSNET/omegahive-schematics/tree/main/10-testing). | Which launch features have tests, and which do not. |
| 9 | 30 min | Read [MODULARITY.md](https://github.com/PhysixSNET/omegahive/blob/main/docs/MODULARITY.md). | Which components are easy to swap and which are coupled. |
| 10 | 30 min | Read [DECIDE.md](../DECIDE.md). | The keep-or-swap rubric and the decision template you will collect from each owner. |

## Checkpoint

**You can now** say what the product does today, what is held or broken, which tier each repo is in, and what must be true before launch.

**Prove it:** draft a launch scope of one page: the features in, the features held (with the STATUS.md line for each), the closed-tier pieces included, and the launch-checklist items still open with an owner role for each. Ask one reviewer and one security owner to check it.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Scope:** which held features stay off for launch: child minds, copy-apply, automatic reasoning ([STATUS.md:49-57](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md))?
2. **Known issues:** which known issues block launch, and which can ship with a note ([STATUS.md:63-78](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md))?
3. **Tiers:** which closed-tier apps are in the launch, and on what terms?
4. **Swap plan:** across all components, which will the team keep and which replace with its own tech? Collect one DECIDE.md record per component.
5. **Demos:** demo mode was out of date and broken at handover ([STATUS.md:77](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)); the live fixes arrive with the omegahive demo-mode fix pull request (`port/demo-mode-fix-r2`). Keep it for launch after a check on the launch build, or launch without it?
6. **Deployers:** is the missing first-time deployer for a single mind ([STATUS.md:68](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)) needed for launch?
