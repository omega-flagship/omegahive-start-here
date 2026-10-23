# Keep, harden or swap: the decision rubric

For each component you will choose one of three things:
- **Keep:** use it as it is.
- **Harden:** keep it, but fix named gaps before launch.
- **Swap:** replace it with your own module behind the same seam.

This page gives you the same scale for every component, tells you where the evidence is, and gives you a record to fill in. The decision is yours. This page scores nothing for you.

## 1. The criteria

Score each criterion from 0 to 3. Higher is always better, so for known issues and coupling, a high score means *few* issues and *loose* coupling.

| Criterion | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| **Maturity** | Design only, or never run | Built and unit-tested, never run live | Ran live in an earlier build or on one host | Live in the current release, used routinely |
| **Test depth** | No tests | Smoke tests or happy path only | Unit tests plus failure cases | Unit, integration and an end-to-end or shadow run, all on the default invocation |
| **Security review state** | Never reviewed | Reviewed once, findings open | Two independent reviews, findings closed | Two reviews, plus a threat-model entry and a test for each control |
| **Known issues** | Blocking issue listed in STATUS | Several open issues, or one serious | Minor issues only | None listed, and the evidence is recent |
| **Coupling** | Reaches into many areas' internals | Shares tables or globals with other areas | Talks through a named seam, with a few side paths | Only through one documented seam |
| **Contract clarity** | No written contract | Contract implied by code only | Written contract, partly tested | Written, versioned contract with a conformance test |
| **Fit with the SingularityNET stack** | Conflicts with Hyperon pieces or duplicates them badly | Unrelated stack, with no path to Hyperon pieces | Uses Hyperon pieces, or has a planned seam for them | Runs on Hyperon pieces (MeTTa, PeTTa, AtomSpace) and keeps the seam open for MORK or DAS |

**How to use the scores.**
- **Do not add them up.** A total hides the one score that matters. Read the row.
- **Security 0 or 1 blocks launch** for anything that handles people, money, model calls or code. Harden or swap.
- **Contract clarity 0 or 1 blocks a swap.** You cannot swap safely against an unwritten contract. Write the contract and its conformance test first (section 5).
- **Fit 0** is a reason to swap even when everything else is high.
- **High coupling with low maturity** usually means harden in place first, then decide. Swapping a tangled part moves the tangle.

## 2. How to read the evidence

Score from evidence, not from prose. Use these sources in this order.

1. **The repo's `STATUS.md`.** Every repo has one. It lists what works, what is limited, what is known broken, and the test counts with the exact command. For the platform, read [`omegahive/STATUS.md`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md) ("Test counts", "Limited or deliberately off", "Known issues"). App repos follow the same shape, for example [`omegaplanner/STATUS.md`](https://github.com/PhysixSNET/omegaplanner/blob/main/STATUS.md).
2. **The component card** in [`omegahive-schematics/components/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/components). Each card names the component's seam, its contract, its tests and its open issues, and links to the schematics pages and code lines. Start from the [card register](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/README.md), which lists every card with its tier, state and seam.
3. **The test map** in [`omegahive-schematics/10-testing/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/10-testing). It says which suites guard which component and how to run them. Start from [`01-test-map.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/10-testing/01-test-map.md); [`02-how-to-run.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/10-testing/02-how-to-run.md) has the commands and [`03-gaps.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/10-testing/03-gaps.md) what is not yet tested.
4. **The feature list,** [`omegahive/docs/FEATURES.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/FEATURES.md). Each feature has a state (Live, Built, Held, Planned) and its evidence.
5. **Work that exists elsewhere,** [`omegahive/docs/EARLIER_EXPERIMENTS.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/EARLIER_EXPERIMENTS.md). It grades evidence as Verified, Reviewed record, Reported or Not ready to claim. Use those grades; do not upgrade them.
6. **The code itself,** at the `path:line` the card or page cites.

**Schematics pages by area** (each has "How it works", "Seams and contracts" and "For reviewers"):

| Area | Page |
|---|---|
| Server, state, requests | [`omegahive-schematics/01-system/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/01-system) |
| Ask, conductor, UI, app frame | [`omegahive-schematics/02-ask-and-ui/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/02-ask-and-ui) |
| Minds, supervisor, sandbox, modules, channels | [`omegahive-schematics/03-minds/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/03-minds) |
| MeTTa, beliefs, reasoning, federation | [`omegahive-schematics/04-knowledge/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/04-knowledge) |
| Policy, budgets, visibility, isolation | [`omegahive-schematics/05-governance/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/05-governance) |
| Programs contract, app lifecycle, each open app | [`omegahive-schematics/06-apps/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/06-apps) |
| Threat model and launch checklist | [`omegahive-schematics/09-security-and-launch/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/09-security-and-launch): [threat model](https://github.com/PhysixSNET/omegahive-schematics/blob/main/09-security-and-launch/01-threat-model.md), [launch checklist](https://github.com/PhysixSNET/omegahive-schematics/blob/main/09-security-and-launch/02-launch-readiness-checklist.md) |

**Rules for reading evidence.**
- **A test count proves only what its default command runs.** Check the command in STATUS. Skips are not passes. Without a working PeTTa, most hive tests error rather than skip ([`omegahive/STATUS.md:20-22`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L20-L22)).
- **Built is not live.** "Held for activation", "default off" and "never run live" mean maturity 1 at most.
- **Intended is not built.** A dashed line in the schematics, a theory page or a plan is intent. Theory pages describe design intent unless they say otherwise ([`omegahive/docs/theory/README.md:16`](https://github.com/PhysixSNET/omegahive/blob/main/docs/theory/README.md#L16)), and theory grants no build authority ([`omegahive/docs/START_HERE.md:107`](https://github.com/PhysixSNET/omegahive/blob/main/docs/START_HERE.md#L107)).
- **Note the date and commit.** Evidence from an earlier build, or from the separate V2 body, describes a different body. Score it as "ran in an earlier build" at most.
- **Truth semantics have an owner.** For reasoning libraries, read [`omegahive/docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) before scoring. Any change goes to the domain author first.

## 3. Score sheet

Copy this table into your working notes. The rows are the platform areas and repos as handed over. The last column points you to the known issues already recorded, so you start from the facts.

| Component | Mat. | Tests | Sec. | Issues | Coup. | Contract | Fit | Start from |
|---|---|---|---|---|---|---|---|---|
| Hive server core (routes, state, reconcile) | | | | | | | | [`omegahive-schematics/01-system/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/01-system); [`omegahive/STATUS.md`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md) "Limited end-to-end testing" |
| Universal Ask and conductor | | | | | | | | [`omegahive-schematics/02-ask-and-ui/01-ask-and-conductor.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/01-ask-and-conductor.md); conductor off unless `HIVE_ASK_CONDUCTOR=1` |
| Web UI, experiences and looks | | | | | | | | [`omegahive-schematics/02-ask-and-ui/02-ui-experiences-and-looks.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/02-ui-experiences-and-looks.md); STATUS "Full custom any UI" |
| App frame bridge | | | | | | | | [`omegahive-schematics/02-ask-and-ui/03-app-frame-bridge.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/02-ask-and-ui/03-app-frame-bridge.md) |
| Native mind runtime (OmegaClaw core loop) | | | | | | | | [primer](primers/the-omegaclaw-mind-loop.md); [`omegahive-schematics/03-minds/01-mind-runtime.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/01-mind-runtime.md) |
| Supervisor, drivers, OS sandbox | | | | | | | | [`omegahive-schematics/03-minds/02-supervisor-drivers-sandbox.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/02-supervisor-drivers-sandbox.md); STATUS "Mind sandbox", "Docker driver" |
| Modules and channels | | | | | | | | [`omegahive-schematics/03-minds/03-modules.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/03-modules.md); STATUS "Modules and add-ons not fully ported" |
| Shared spaces and commons (`lib_hive`) | | | | | | | | [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md), [`omegahive-schematics/04-knowledge/02-beliefs-sharing.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md) |
| Reasoning libraries (NAL, PLN, NARS) | | | | | | | | [`omegahive-schematics/04-knowledge/03-reasoning.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/03-reasoning.md); [`omegahive/docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) |
| Attention organ | | | | | | | | [primer](primers/attention-ecan.md); STATUS "Attention" |
| Long-term recall (ChromaDB) | | | | | | | | [`omegahive-schematics/04-knowledge/01-metta-and-atomspace.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/01-metta-and-atomspace.md); default embedder `mock/hash` |
| Federation and mind moves | | | | | | | | [`omegahive-schematics/04-knowledge/04-federation.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/04-federation.md); STATUS "Hive-to-hive connection" |
| Model gateway | | | | | | | | [`omegahive-schematics/03-minds/05-models-and-gateway.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/03-minds/05-models-and-gateway.md), [gateway card](https://github.com/PhysixSNET/omegahive-schematics/blob/main/components/llm-gateway-and-providers.md); [`omegahive-schematics/05-governance/02-budgets-and-spend.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md) |
| Budgets and spend | | | | | | | | [`omegahive-schematics/05-governance/02-budgets-and-spend.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/02-budgets-and-spend.md) |
| Policy gate, approvals, capability tokens | | | | | | | | [`omegahive-schematics/05-governance/01-permissions-and-policy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/01-permissions-and-policy.md); STATUS "Approvals" |
| Visibility and privacy | | | | | | | | [`omegahive-schematics/05-governance/03-visibility-and-privacy.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/05-governance/03-visibility-and-privacy.md) |
| Programs contract and app lifecycle | | | | | | | | [primer](primers/the-programs-contract.md); [`omegahive-schematics/06-apps/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/06-apps); STATUS "Deploying an app with its swarm" |
| Open apps: Tools, Planner, Library | | | | | | | | [`omegahive-schematics/06-apps/apps/`](https://github.com/PhysixSNET/omegahive-schematics/tree/main/06-apps/apps); each repo's `STATUS.md` |
| Closed apps: Studio, Code, Fusion, Social, Purple, Atlas, Truth | | | | | | | | each repo's `STATUS.md` and its own `docs/schematics/` |
| Closed folders in `omegahive`: Evolve, OmegaTown, WhatsApp bridge | | | | | | | | the `SCHEMATICS.md` in each folder |
| Legacy: `omegav2`, `omegahive-candidates` | | | | | | | | [`omegahive/LEGACY.md`](https://github.com/PhysixSNET/omegahive/blob/main/LEGACY.md); each repo's `STATUS.md` |
| Demo mode | | | | | | | | STATUS "Demo mode" (out of date and broken at handover; fixed by the omegahive demo-mode fix pull request, `port/demo-mode-fix-r2`) |

## 4. Decision record

Write one record per component. Keep it short. Link evidence; do not paste it.

```markdown
# Decision: <component>

- **Context:** what the component does, where its seam is, and why it is being decided now.
- **Options:**
  - Keep as is.
  - Harden: <the named gaps to close>.
  - Swap for <X>: <what X is, and which seam it plugs into>.
- **Evidence:** the seven scores, each with a link (STATUS line, card, test map row, code path:line).
- **Decision:** keep, harden or swap, in one sentence.
- **Consequences:** what changes for other components, data, operations and people; what you give up.
- **Conformance test to pass:** the named test or suite, its exact command, and the result that counts as a pass.
- **Owner:** a role, not a name.
- **Date:** YYYY-MM-DD, plus the commit the evidence was read at.
```

### Example (illustrative only)

> **This is an invented example.** The component, scores and facts below describe no real part of this codebase. It shows the shape of a filled-in record.

```markdown
# Decision: document-search service (EXAMPLE)

- **Context:** A service that indexes uploaded documents and answers search queries for minds. Minds reach it
  through one skill, `doc-search`, which calls the service over a small JSON API. It is being decided because the
  team already runs its own search service.
- **Options:**
  - Keep as is.
  - Harden: add a size limit on uploads and a test for refused queries.
  - Swap for the team's search service, behind the same `doc-search` skill and JSON API.
- **Evidence:**
  - Maturity 2: ran live on one host in an earlier build (STATUS, "What works").
  - Test depth 1: happy-path tests only (test map row "doc-search").
  - Security 1: reviewed once; finding "no upload size limit" open (card, "Open issues").
  - Known issues 2: one minor issue, slow re-index (STATUS, "Limited").
  - Coupling 3: only the `doc-search` skill and its API (card, "Seam").
  - Contract 2: the API is written down; no conformance test (card, "Contract").
  - Fit 1: plain Python, no path to the AtomSpace.
- **Decision:** Swap for the team's search service, behind the same seam.
- **Consequences:** The old index is not migrated; documents are re-indexed. The `doc-search` skill and its
  API do not change, so minds and their policy rules need no edits. Operations run one service fewer.
- **Conformance test to pass:** `doc_search_conformance` (written first; see "How to swap"), run against both
  the old and the new service with the same synthetic documents. Pass: every case equal, including refusals.
- **Owner:** search lane owner.
- **Date:** 2026-10-10, evidence read at commit abc1234.
```

## 5. How to swap a module safely

1. **Write or run the conformance test first.** If a conformance test exists, run it against the current component and record the result. If none exists, write one now, from the written contract, and make it pass against the *current* component before you touch anything. Use synthetic data only. Include refusals and error cases, not just the happy path. Existing examples: `python -m hive.programs_check <dir>` for apps ([`omegahive/hive/programs_check.py:1-20`](https://github.com/PhysixSNET/omegahive/blob/main/hive/programs_check.py#L1-L20)), and `tests/hive_lib_smoke.metta` for the commons rules.
2. **Keep the contract.** The new module speaks the same contract version, the same shapes, the same error codes and the same refusals. If the contract must change, that is a separate, versioned change to the contract, reviewed on its own. Do it before the swap, not during it.
3. **Run it behind the same seam.** Plug the new module in where the old one was: the same skill name, module folder, programs entry, hook or route. Do not add a side path. Run the conformance test against the new module and compare the results with step 1, case by case. Then run the tests the test map lists for that seam, and a shadow run end to end. Nothing counts as accepted without a shadow run ([`omegahive/docs/START_HERE.md:107-109`](https://github.com/PhysixSNET/omegahive/blob/main/docs/START_HERE.md#L107-L109)).
4. **Use the two-reviewer rule.** Two independent reviewers check the change and the evidence before it is deployed ([`omegahive-start-here/README.md`](https://github.com/PhysixSNET/omegahive-start-here/blob/main/README.md), "Rules carried over"). Neither reviewer may be the author.

**Also check before you merge.**
- **Tier travels with the code.** A swap does not change the tier of what it touches.
- **Pins.** Apps load only from their pinned release when pinned (`HIVE_APP_PINS`). Update the pin with the release.
- **Truth semantics.** Swapping a reasoning library changes truth semantics. Send it to the domain author and check it against [`omegahive/docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) first.
- **No private data.** Conformance fixtures are invented. Never run a mutating check (for example `programs_check --allow-mutation`) against real records.
