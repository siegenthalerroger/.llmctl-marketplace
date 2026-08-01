# Third-party notices

Some plugin bundles in this repository vendor skills authored elsewhere and consumed by [`.llmctl`](https://github.com/siegenthalerroger/.llmctl) as pinned APM dependencies. `apm pack` copies skill files only — it does not copy upstream `LICENSE` files — so the notices are collected here.

> [!WARNING]
> This file is currently **maintained by hand and is not verified against what is actually packed**. Generating it from each bundle's embedded `apm.lock.yaml` is tracked as TODO 7a in `.llmctl`. Until that lands, re-check it after every dependency change.

Each bundle's `apm.lock.yaml` records the upstream `repo_url`, the resolved commit, and a SHA-256 per file, which is the authoritative record of what a given bundle contains.

## llmctl-workflow

| Skill | Upstream | Licence |
| --- | --- | --- |
| `using-git-worktrees` | [obra/superpowers](https://github.com/obra/superpowers) | MIT |
| `receiving-code-review` | [obra/superpowers](https://github.com/obra/superpowers) | MIT |
| `tdd` | [mattpocock/skills](https://github.com/mattpocock/skills) | MIT |
| `resolving-merge-conflicts` | [mattpocock/skills](https://github.com/mattpocock/skills) | MIT |
| `lint-fix` | [rshade/agent-skills](https://github.com/rshade/agent-skills) | Apache-2.0 |

## llmctl-core

| Skill | Upstream | Licence |
| --- | --- | --- |
| `grilling` | [mattpocock/skills](https://github.com/mattpocock/skills) | MIT |
| `grill-me` | [mattpocock/skills](https://github.com/mattpocock/skills) | MIT |

## llmctl-ops

| Skill | Upstream | Licence |
| --- | --- | --- |
| `terraform-skill` | [antonbabenko/terraform-skill](https://github.com/antonbabenko/terraform-skill) | Apache-2.0 |

## Licence texts

- MIT — <https://opensource.org/license/mit>
- Apache-2.0 — <https://www.apache.org/licenses/LICENSE-2.0>

MIT requires the copyright notice and permission notice to accompany redistribution; Apache-2.0 requires the licence, attribution notices, and a statement of changes. Full upstream texts are reachable from each repository linked above.
