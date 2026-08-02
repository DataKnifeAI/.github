<p align="center">
  <img src="https://raw.githubusercontent.com/DataKnifeAI/.github/main/profile/assets/dataknifeai-org-logo.png" alt="DataKnifeAI" width="240" height="240" />
</p>

# DataKnifeAI

**Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.**

DataKnifeAI is an organization for learning and solving problems with AI tooling. We put AI to work in ways people can operate and evolve over time: automation carries the repeatable pieces, and we favor boring reliability over fragile cleverness. When it fits, we prefer open software that preserves user agency.

> **North star:** a fully autonomous agent pipeline that can hand off work to run in the background—leveraging API LLMs and local LLMs—so people set direction while agents execute, monitor, and iterate without constant babysitting.

The name nods lightly to a tool for getting into systems—applied here to AI development, not game fiction.

## What we're building toward

| Layer | Intent |
|-------|--------|
| **Agent control plane** | Fleet orchestration, sandboxes, and on-demand workers on Kubernetes |
| **Tooling surface** | MCP servers and skills so agents can act on real infrastructure and APIs |
| **GitOps + infra** | Repeatable cluster and platform delivery that agents (and humans) can trust |
| **Local + API models** | Run where it fits—self-hosted inference when you want agency, cloud APIs when you want reach |

## For new and existing projects

Before inventing project-local Cursor skills or Cloud Agent layouts, review the shared baselines:

- **[agent-skills](https://github.com/DataKnifeAI/agent-skills)** — shared Cursor skills for the org
- **[agent-workspace](https://github.com/DataKnifeAI/agent-workspace)** — Cloud Agent / Coder workspace baseline (vendors `agent-skills`)

Short checklist: [PROJECT_SETUP.md](https://github.com/DataKnifeAI/.github/blob/main/docs/PROJECT_SETUP.md).

## Featured projects

### Agent pipeline & control plane

- **[nauarchos](https://github.com/DataKnifeAI/nauarchos)** — Kubernetes control plane for agent fleets (classes, sandboxes, dependencies, on-demand workers)
- **[dioptra](https://github.com/DataKnifeAI/dioptra)** — Agent fleet status board (k8s · Cursor/Hermes · issue backlog)
- **[enodios](https://github.com/DataKnifeAI/enodios)** — One-script Linux setup for Hermes Agent + vLLM self-hosting
- **[agent-workspace](https://github.com/DataKnifeAI/agent-workspace)** — Starting workspace for Cursor Cloud Agents (managed and self-hosted pools)
- **[agent-skills](https://github.com/DataKnifeAI/agent-skills)** — Shared Cursor/agent skills across DataKnifeAI projects

### MCP tools (agents ↔ infrastructure)

- **[rancher-manager-mcp](https://github.com/DataKnifeAI/rancher-manager-mcp)** — Rancher Manager API
- **[proxmox-ve-mcp](https://github.com/DataKnifeAI/proxmox-ve-mcp)** — Proxmox VE infrastructure
- **[unifi-network-mcp](https://github.com/DataKnifeAI/unifi-network-mcp)** / **[unifi-protect-mcp](https://github.com/DataKnifeAI/unifi-protect-mcp)** / **[unifi-manager-mcp](https://github.com/DataKnifeAI/unifi-manager-mcp)** — UniFi network, Protect, and site management
- **[gitops-mcp](https://github.com/DataKnifeAI/gitops-mcp)** — GitOps workflows via MCP

### GitOps & platform infra

- **[rancher-deploy](https://github.com/DataKnifeAI/rancher-deploy)** — IaC for Rancher Kubernetes on Proxmox
- **[gitops-core](https://github.com/DataKnifeAI/gitops-core)** / **[gitops-fleet](https://github.com/DataKnifeAI/gitops-fleet)** / **[gitops-tools](https://github.com/DataKnifeAI/gitops-tools)** / **[gitops-dev](https://github.com/DataKnifeAI/gitops-dev)** — Certificate, fleet, tools, and app GitOps
- **[coder-templates](https://github.com/DataKnifeAI/coder-templates)** — Custom Coder workspace templates
- **[github-workflows](https://github.com/DataKnifeAI/github-workflows)** — Reusable GitHub Actions for the org

### Operators & apps

- **[palworld-operator](https://github.com/DataKnifeAI/palworld-operator)** / **[windrose-operator](https://github.com/DataKnifeAI/windrose-operator)** — Game-server operators on Kubernetes
- **[high-command-api](https://github.com/DataKnifeAI/high-command-api)** / **[high-command-ui](https://github.com/DataKnifeAI/high-command-ui)** / **[high-command-mcp](https://github.com/DataKnifeAI/high-command-mcp)** — Real-time game-data API, UI, and MCP surface
- **[freya](https://github.com/DataKnifeAI/freya)** — Kubernetes-ready ComfyUI / SwarmUI with GPU support

## Principles

- **Maintainable** — clear structure people can operate and evolve over time
- **Automated** — repeatable workflows over one-off heroics
- **Stable** — boring reliability over fragile cleverness
- **Freedom-respecting** — prefer open and free (as in freedom) software that preserves user agency when it fits

## Explore

Browse all repositories: **[github.com/DataKnifeAI](https://github.com/DataKnifeAI)**

Contributions and experiments welcome where they advance maintainable, automatable AI systems—especially pieces of the agent handoff pipeline.
