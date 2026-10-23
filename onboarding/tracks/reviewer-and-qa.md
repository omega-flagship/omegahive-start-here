# Track: Reviewer and QA

**For you if** you review changes, run the suites and decide whether a change is safe to ship. The standing rule is two independent reviewers before anything is deployed ([start-here README](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md)).

**Total time:** about 8 hours.

## Steps

| # | Time | Do this | Look for |
|---|---|---|---|
| 1 | 30 min | Read the [hive-concepts primer](../primers/hive-concepts.md). | The main parts, so you know what a change touches. |
| 2 | 20 min | Read the `omegahive` [STATUS.md](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md). | The recorded test counts, what is deliberately off, and the known issues. Expect integration bugs; end-to-end testing is limited ([STATUS.md:74](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 3 | 45 min | Read the test map in [10-testing](https://github.com/PhysixSNET/omegahive-schematics/tree/main/10-testing). | Which suite covers which component, and where there is no coverage. |
| 4 | 30 min | Read the reviewer pages in [08-reviewers](https://github.com/PhysixSNET/omegahive-schematics/tree/main/08-reviewers), and the "For reviewers" section of any schematics page in the area you review. | What each part must guarantee. |
| 5 | 90 min | Read the primer [PeTTa and SWI-Prolog](../primers/petta-and-swi-prolog.md), follow the [disposable local hive setup](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md) and run the three suites on a clean clone at an exact commit: hive server, OmegaClaw core and UI ([STATUS.md:15-18](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). | Your counts against the recorded ones. Run one heavy suite at a time and do not edit the tree while it runs. |
| 6 | 60 min | Walk the tours [01: follow an Ask request](https://github.com/PhysixSNET/omegahive/blob/main/.tours/01-follow-an-ask-request.tour) and [06: who can see what](https://github.com/PhysixSNET/omegahive/blob/main/.tours/06-who-can-see-what.tour). | The checks a change on the request path must not skip. |
| 7 | 45 min | Read the cards [policy-and-approvals](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/policy-and-approvals.md), [visibility](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/visibility.md), [budgets](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/budgets.md) and [app-pins](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/app-pins.md). | The guarantees that are review-blocking if a change weakens them. |
| 8 | 45 min | Read [09-security-and-launch](https://github.com/PhysixSNET/omegahive-schematics/tree/main/09-security-and-launch). | The threat model and the launch checklist you will sign against. |
| 9 | 15 min | Read the CI workflow [ci.yml](https://github.com/PhysixSNET/omegahive/blob/main/.github/workflows/ci.yml). | What it runs. It has not yet run on GitHub ([STATUS.md:60](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md)). |
| 10 | 45 min | Do the [disposable-hive exercise](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md) with [hello-app](https://github.com/PhysixSNET/omegahive/tree/main/examples/hello-app). | Write a test that would catch hello-app acting without a grant. |

## Checkpoint

**You can now** reproduce the recorded test counts, name which suite guards each component, and say which guarantees a change must not weaken.

**Prove it:** take one recent commit in `omegahive`. Run only the tests for the area it changed plus a smoke test, at that exact commit, on a clean clone. Write a short review: what it changes, which guarantees it touches, which tests prove them, and one gap with a proposed test.

## Your keep-or-swap questions

Answer these with the rubric in [DECIDE.md](../DECIDE.md).

1. **Suites:** keep the current three suites as they are, or reorganise them into your own CI layout?
2. **CI:** what must the CI run on every change before the first launch, and on what machines?
3. **End to end:** which end-to-end flows must have automated tests before launch?
4. **Review gate:** keep the two-independent-reviewers rule as is, or add automated gates beside it?
5. **Known issues:** for each known issue in STATUS.md, is it launch-blocking?
