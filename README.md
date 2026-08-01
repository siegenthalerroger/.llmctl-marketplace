# .llmctl-marketplace

The published plugin marketplace for [`.llmctl`](https://github.com/siegenthalerroger/.llmctl), a personal collection of agent steering files.

**Everything here except `apm.yml`, this README, and the licence files is generated.** Do not hand-edit `plugins/` or either `marketplace.json` — regenerate instead (see below).

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

That packs every `packages/<name>/` into `plugins/<name>-<version>/` here, rewrites the `source:` paths in [`apm.yml`](apm.yml) to the versions just packed, and runs `apm pack` here to regenerate both manifests:

| File | Consumer |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code, Claude Desktop, Cowork |
| `.agents/plugins/marketplace.json` | Codex |

Pass `--marketplace PATH` (or set `LLMCTL_MARKETPLACE_DIR`) if this repository is not at `../.llmctl-marketplace`.

## Licensing

`.llmctl` does not declare a licence yet (tracked as TODO 7a there), so the authored content here is unlicensed by default. Several bundles also vendor third-party skills consumed as APM dependencies — see [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md). Each bundle's embedded `apm.lock.yaml` records the upstream `repo_url` and a SHA-256 for every file it carries.
