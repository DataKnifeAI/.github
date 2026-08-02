# DataKnifeAI

**Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.**

DataKnifeAI is an organization for learning and solving problems with AI tooling. We put AI to work in ways people can operate and evolve over time: automation carries the repeatable pieces, and we favor boring reliability over fragile cleverness. When it fits, we prefer open software that preserves user agency.

> **North star:** a fully autonomous agent pipeline that can hand off work to run in the background—leveraging API LLMs and local LLMs—so people set direction while agents execute, monitor, and iterate without constant babysitting.

This GitLab group (`dk-raas/dkai`) is the **mirror / secondary** home for DataKnifeAI projects. Canonical development and org profile live on GitHub: **[github.com/DataKnifeAI](https://github.com/DataKnifeAI)**.

## Group layout

| Subgroup | Purpose |
|----------|---------|
| [`mcp-servers`](https://gitlab.com/dk-raas/dkai/mcp-servers) | MCP servers (agents ↔ infrastructure) |
| [`devops`](https://gitlab.com/dk-raas/dkai/devops) | GitOps, Rancher deploy, infra |
| [`high-command`](https://gitlab.com/dk-raas/dkai/high-command) | High Command API / UI |
| [`tools`](https://gitlab.com/dk-raas/dkai/tools) | Shared tools (e.g. Freya) |
| [`game-servers`](https://gitlab.com/dk-raas/dkai/game-servers) | Game-server related projects |

## Org docs (this project)

| Doc | Purpose |
|-----|---------|
| [`docs/ORG_BRANDING.md`](docs/ORG_BRANDING.md) | Mission, profile copy, avatar guidance |
| [`docs/NAMING.md`](docs/NAMING.md) | Project naming (same policy as GitHub) |
| [`docs/PROJECT_SETTINGS.md`](docs/PROJECT_SETTINGS.md) | GitLab protected branches / MR defaults (solo-dev) |
| [`docs/PROJECT_SETUP.md`](docs/PROJECT_SETUP.md) | Pointers to shared agent baselines (GitHub-canonical) |

## Featured projects (GitLab mirrors)

Paths may live under subgroups. Prefer GitHub for the freshest source of truth when both exist.

### GitOps & platform

- [rancher-deploy](https://gitlab.com/dk-raas/dkai/devops/rancher-deploy)
- [gitops-core](https://gitlab.com/dk-raas/dkai/devops/gitops-core) / [gitops-tools](https://gitlab.com/dk-raas/dkai/devops/gitops-tools) / [gitops-mcp](https://gitlab.com/dk-raas/dkai/devops/gitops-mcp)

### MCP tools

- [rancher-manager-mcp](https://gitlab.com/dk-raas/dkai/mcp-servers/rancher-manager-mcp)
- [proxmox-ve-mcp](https://gitlab.com/dk-raas/dkai/mcp-servers/proxmox-ve-mcp)
- [unifi-network-mcp](https://gitlab.com/dk-raas/dkai/mcp-servers/unifi-network-mcp) / [unifi-protect-mcp](https://gitlab.com/dk-raas/dkai/mcp-servers/unifi-protect-mcp) / [unifi-manager-mcp](https://gitlab.com/dk-raas/dkai/mcp-servers/unifi-manager-mcp)

### Apps

- [high-command-api](https://gitlab.com/dk-raas/dkai/high-command/high-command-api) / [high-command-ui](https://gitlab.com/dk-raas/dkai/high-command/high-command-ui)
- [freya](https://gitlab.com/dk-raas/dkai/tools/freya)

Newer agent-pipeline repos (nauarchos, dioptra, enodios, agent-skills, …) currently live primarily on GitHub; mirror when needed.

## Principles

- **Maintainable** — clear structure people can operate and evolve over time
- **Automated** — repeatable workflows over one-off heroics
- **Stable** — boring reliability over fragile cleverness
- **Freedom-respecting** — prefer open and free (as in freedom) software that preserves user agency when it fits

## Explore

- GitLab group: **[gitlab.com/dk-raas/dkai](https://gitlab.com/dk-raas/dkai)**
- GitHub org: **[github.com/DataKnifeAI](https://github.com/DataKnifeAI)**
