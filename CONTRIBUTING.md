# Contributing to start-here

This repo is the front door to the OmegaHive handover: the repo map and tiers ([`README.md`](README.md)), and the onboarding kit in [`onboarding/`](onboarding/). It holds no code. The work is keeping it accurate, short and correctly linked.

## Where things go
Each fact lives in exactly one place. This repo links down to the layer below and does not repeat it.

| Layer | Holds |
|---|---|
| `omegahive-start-here` (here) | Who are you? Learning tracks (`onboarding/tracks/`), primers (`onboarding/primers/`), the glossary (`onboarding/GLOSSARY.md`), and the keep-or-swap rubric (`onboarding/DECIDE.md`) |
| `omegahive-schematics` | Component cards, the threat model and launch checklist, the test map, and the diagram sections |
| `omegahive` (code) | Code tours (`.tours/`) and sandbox exercises (`examples/`) |

If what you want to write is about how one component works, it belongs in a schematics page or card. Link to it from here.

## Add a page
- **A primer:** `onboarding/primers/<topic>.md`. Explain one idea from zero to useful, on one page. Cite the code for every claim about how this build behaves. List it in [`onboarding/README.md`](onboarding/README.md).
- **A track:** `onboarding/tracks/<role>.md`. An ordered list of short steps. Each step links to the one place the fact lives, says how long it takes, and says what you should know after it. End with a checkpoint task and the keep-or-swap questions. List it in [`onboarding/tracks/README.md`](onboarding/tracks/README.md).
- **A glossary term:** one or two lines in [`onboarding/GLOSSARY.md`](onboarding/GLOSSARY.md), with a link to where the term is explained.

## Links and code refs
- **Inside this repo:** relative links, for example `[DECIDE.md](../DECIDE.md)`. Anchors follow GitHub's heading rules: lower case, spaces become `-`, punctuation dropped.
- **Other repos:** full links of the form `https://github.com/PhysixSNET/<repo>/blob/main/<path>`, or `/tree/main/<folder>` for a folder. Add `#L10-L20` to point at lines.
- **Code refs:** `path:line` or `path:start-end` in backticks, against the `omegahive` repo at the commit the page names, for example `` `omegahive/hive/core/budgets.py:294` ``. Lines drift, so name the symbol too.

## House rules
- **Plain language.** Short sentences, active voice, no hype. Written for expert engineers who are new to this codebase.
- **Accuracy.** Cite what you actually read. Intended things cite where the intent is written down. Never present intended as built.
- **Privacy.** No personal names, family, emails, home-folder paths, hostnames, ports or real ids. Name people by role.
- **Tiers.** Say which tier each repo is in. Describe closed-tier pieces only by name and by how they connect to the hive.
- **Diagrams.** Prefer linking to a schematics diagram. If you draw one here, use mermaid and follow the diagram rules in the `omegahive-schematics` [CONTRIBUTING](https://github.com/PhysixSNET/omegahive-schematics/blob/main/CONTRIBUTING.md#add-a-diagram): label lines of 26 characters or fewer, no ` · ` lists, at most 14 nodes, quoted labels, and `classDef intended` declared when you use `:::intended` or `-.->`. The checker enforces them here too.

## Check your work locally
You need Python 3.9 or later (CI uses 3.12) and, to render diagrams, Node 22.

Clone the repos side by side, then run from this repo:

```sh
# links, anchors and the mermaid house rules (errors fail)
python3 tools/check_docs.py

# also check code refs (warnings) and cross-repo links (errors)
python3 tools/check_docs.py --omegahive ../omegahive --root ..
```

`--root` looks for each sibling as `<root>/<repo>` or `<root>/apps/<repo>`. `--strict` turns warnings into errors. `tools/check_docs.py` is the same script as in `omegahive-schematics`; change both together.

The [`docs` workflow](.github/workflows/docs.yml) runs the checker and renders any mermaid diagrams on each push and pull request. CI has no sibling checkouts, so there it only lists cross-repo links and skips code refs. Run the full check locally before you ask for review.

## Review
Every change needs two independent reviewers, neither of them the author. A review is void if the change is altered after it.
