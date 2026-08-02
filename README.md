# .llmctl-marketplace

The published plugin marketplace for [`.llmctl`](https://github.com/siegenthalerroger/.llmctl), a personal collection of agent steering files.

> [!WARNING]
> **Everything here except `apm.yml`, this README, and the licence files is generated.** Do not hand-edit `plugins/`, either `marketplace.json`, or `THIRD-PARTY-NOTICES.md` — regenerate instead (see below).

## Why a separate repository

A plugin host (claude.ai Cowork, Claude Desktop, Claude Code) clones the marketplace repository and reads each plugin's `source` path exactly as committed. It never runs `apm install`, so a package whose content comes from APM dependencies has to be published as a **packed bundle** with the skills already vendored into it. Keeping those generated bundles out of the source repository is what this repository is for. `apm pack` also refuses to write a marketplace manifest across a `..` boundary, so generation happens in two halves.

## Consuming

```text
/plugin marketplace add siegenthalerroger/.llmctl-marketplace
/plugin install llmctl-core@llmctl-marketplace
```

> [!IMPORTANT]
> This is a **reduced-fidelity** distribution path. A plugin bundle carries **skills** and **commands** only — instructions, MCP servers, and agents do not travel. For the full deploy use `apm install` against [`.llmctl`](https://github.com/siegenthalerroger/.llmctl) directly.

## Regenerating

From a checkout of `.llmctl` with this repository as a sibling directory:

```bash
cd ~/.llmctl
python scripts/pack-marketplace.py     # or: apm run pack-marketplace
```

That packs every `packages/<name>/` into `plugins/<name>-<version>/` here, copies in the licence files each bundle needs, rewrites the `source:` paths in [`apm.yml`](apm.yml) to the versions just packed, regenerates [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md), and runs `apm pack` here to regenerate both manifests:

| File | Consumer |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code, Claude Desktop, Cowork |
| `.agents/plugins/marketplace.json` | Codex |

Pass `--marketplace PATH` (or set `LLMCTL_MARKETPLACE_DIR`) if this repository is not at `../.llmctl-marketplace`.

To cut a release rather than just re-pack, run `apm run release` in `.llmctl`: it derives each package's version from its commits, packs, commits, and tags both repositories. Packages version **independently** — a change to `ops` moves `ops` alone.

### What a bundle contains

| Path | Purpose |
| --- | --- |
| `.claude-plugin/plugin.json` | Manifest; hosts detect a plugin by this path |
| `LICENSE` + `LICENSES/` | The split licence, plus only the texts this bundle needs |
| `apm.yml` | Name, version and SPDX expression — read by `apm pack --check-versions` |
| `apm.lock.yaml` | Upstream repo, resolved commit and SHA-256 per file |
| `skills/`, `agents/`, `commands/`, `instructions/` | The packed content |

## Licensing

Split, inherited from `.llmctl` — **CC-BY-SA-4.0** for the markdown content (skills, agents, instructions, references) and **MIT** for scripts and config. See [LICENSE](LICENSE); full texts are in [LICENSES/](LICENSES/) and inside every bundle.

The content half is copyleft: adapt a skill from a bundle and your adaptation must be CC-BY-SA-4.0 too, with attribution and a note that you changed it. Using it as-is, commercially or not, is unrestricted.

Two things are **not** covered by that split, and both are enumerated in the generated [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md): files carrying their own `license:` frontmatter field, and the third-party skills bundles vendor as APM dependencies (MIT and Apache-2.0). Each bundle ships only the licence texts it actually needs, plus an `apm.lock.yaml` recording the upstream `repo_url`, resolved commit, and a SHA-256 for every file it carries.
