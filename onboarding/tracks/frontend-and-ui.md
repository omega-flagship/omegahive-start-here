# Track: Frontend and UI

**For you if** you work on the web UI: the shell, the Ask on every page, experiences and looks, and the frame that hosts app views.

**Total time:** about 7.5 hours.

**Note on tiers:** the OmegaTown experience (`hive/ui/src/experiences/omegatown`) is closed-tier. Open pages describe it only as a named box ([start-here README](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md)).

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | What a personal mind is, and why every page has an Ask. |
| 2 | 45 min | Read [Ask and conductor](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/01-ask-and-conductor.md) and the card [ask-and-conductor](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ask-and-conductor.md). | How the conductor steers the screen with typed acts. |
| 3 | 45 min | Walk the tour [01: follow an Ask request](https://github.com/PhysixSNET/omegahive/blob/main/.tours/01-follow-an-ask-request.tour). | Where the UI sends the request and how the reply reshapes the screen. |
| 4 | 45 min | Read [UI, experiences and looks](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md) and the card [ui-shell](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ui-shell.md). | The difference between an experience and a look, and how to add each. |
| 5 | 20 min | Read the UI [README.md](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/README.md) and [BRAND.md](https://github.com/PhysixSNET/omegahive/blob/main/hive/ui/BRAND.md). | How to build and run the UI, and the brand rules (mark, type scale, colour). The wording guard test (`hive/ui/src/wordingGuard.test.ts:55`) blocks the words "goal" and "board" in what people see. |
| 6 | 55 min | Read the primer [The programs contract](../primers/the-programs-contract.md), then [App frame bridge](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/03-app-frame-bridge.md) and the card [app-frame](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-frame.md). | What messages pass between the hive UI and an app view, and what the frame blocks. |
| 7 | 45 min | Walk the tour [03: an app action, click to result](https://github.com/PhysixSNET/omegahive/blob/main/.tours/03-an-app-action-click-to-result.tour). | How a click in an app view becomes an exact-request app action. |
| 8 | 20 min | Read the card [visibility](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/visibility.md). | What the UI may show to whom. The server decides; the UI must not widen it. |
| 9 | 30 min | Read the card [swarms-and-rooms](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/swarms-and-rooms.md) and [goals-and-motivations](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/goals-and-motivations.md). | Which routes current screens should target. |
| 10 | 60 min | Do the exercise [hello-app](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-app) in the [disposable local hive](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md). | Your app's view showing in the frame, and an action from it reaching the app. |
| 11 | 30 min | Read the UI part of [10-testing](https://github.com/PhysixSNET/omegahive-schematics/tree/main/10-testing) and run `npx tsc -b --noEmit` and `npx vitest run` in `hive/ui` ([STATUS.md:17-18](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). | Your counts against the recorded ones. A few tests time out under heavy load and pass alone ([STATUS.md:78](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |

## Checkpoint

**You can now** follow an Ask from the input box to the screen change it causes, add a look, and host an app view in the frame without widening what anyone can see.

**Prove it:** in the sandbox, add a new look that changes only colours and type, switch to it from the Ask, and add a UI test that checks the look applies. Then confirm the Ask still works on the hello-app page.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Shell** ([ui-shell](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ui-shell.md)): keep the current shell and its experiences, or swap in your own front end against the same server API?
2. **Conductor** ([ask-and-conductor](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/ask-and-conductor.md)): keep the typed-act model for steering the screen, or use your own?
3. **App frame** ([app-frame](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-frame.md)): keep the frame bridge for app views, or host apps differently?
4. **Per-person UI:** letting each person reshape the whole interface is mostly finished and untested ([STATUS.md:72](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). Ship it, hold it, or replace it?
5. **Demos:** demo mode was out of date and broken at handover ([STATUS.md:77](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)); the live fixes arrive with the omegahive demo-mode fix pull request (`port/demo-mode-fix-r2`). Keep it, with a browser check on each release, or retire it?
