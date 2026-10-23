# Who are you?

Pick the track that matches your role. Each track is an ordered path of short steps. Every step links to the one place where that fact lives: a primer, a component card, a schematics page, a code tour or a sandbox exercise. Each track ends with a checkpoint task and your keep-or-swap questions.

**Whatever your role, start with the [hive-concepts primer](../primers/hive-concepts.md).** Keep the [glossary](../GLOSSARY.md) open beside you. Each track names the other primers it needs. When you are ready to decide whether to keep, harden or swap a component for your own module, use [DECIDE.md](../DECIDE.md). Rolling the tracks out to a whole team? [PROGRAM.md](../PROGRAM.md) has a four-week plan, the prerequisites between tracks, and who signs off what.

| Track | For you if you … |
|---|---|
| [MeTTa and Hyperon researcher](metta-hyperon-researcher.md) | know MeTTa, AtomSpace, NAL or PLN and want to see how minds and the shared commons use them. |
| [Security and privacy](security-and-privacy.md) | own the threat model, sign-in, visibility, sandboxing and approvals. |
| [Backend and infrastructure](backend-and-infrastructure.md) | run the hive server, its state, its supervisor and its deployments. |
| [Frontend and UI](frontend-and-ui.md) | work on the shell, the Ask, experiences, looks and the app frame. |
| [App owner](app-owner.md) | own one app repo and need to know how it plugs into the hive. |
| [Module and model integrator](module-and-model-integrator.md) | want to swap in your own module, mind organ or model provider. |
| [Reviewer and QA](reviewer-and-qa.md) | review changes, run the suites and decide what is safe to ship. |
| [Product and launch](product-and-launch.md) | plan what ships, what is known broken and what must be true before launch. |

## How the tracks fit together
- **Order:** do the steps in order. Later steps assume the earlier ones.
- **Time:** the estimates are for reading carefully and trying things once. Exercises run in a disposable local hive with invented data only (see [examples/SANDBOX.md](https://github.com/PhysixSNET/omegahive/blob/main/examples/SANDBOX.md)). It is not a security sandbox: it runs as you, minds get no OS isolation, and apps are trusted host code. Use a disposable VM or container for anything adversarial.
- **Built versus intended:** schematics draw built parts with solid lines and intended parts with dashed lines ([LEGEND.md](https://github.com/PhysixSNET/omegahive-schematics/blob/main/LEGEND.md)). Treat anything dashed as a plan, not as code.
- **Known issues:** the current list is in [omegahive STATUS.md](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md). Read it before you trust a demo; demo mode is out of date and broken (STATUS.md:77).
