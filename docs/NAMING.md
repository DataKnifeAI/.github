# DataKnifeAI repository naming

How we name new projects so the org stays discoverable, mission-aligned, and not coupled to any single upstream product.

Related: [ORG_BRANDING.md](./ORG_BRANDING.md) (mission, tagline, principles).

## Goals

Name for **what DataKnifeAI owns** in the autonomous agent pipeline—not for whoever’s runtime or model we happen to integrate first.

North-star layers (from the org profile):

| Layer | Intent | Name style (prefer) |
|-------|--------|---------------------|
| **Agents / control plane** | Fleet orchestration, sandboxes, on-demand workers | Evocative single word *or* `agent-*` |
| **Tooling surface** | MCP servers, skills, agent-facing APIs | Descriptive: `<domain>-mcp`, `agent-skills` |
| **GitOps + infra** | Cluster/platform delivery humans and agents trust | Descriptive: `gitops-*`, `<platform>-deploy` |
| **Local + API models** | Inference bootstrap, model serving helpers | Evocative *or* descriptive; say what it installs |
| **Operators & apps** | Workloads that aren’t the pipeline core | `<product>-operator`, domain names |

## Conventions

### Prefer descriptive names when the job is obvious

Use a clear prefix/suffix so search and topics work:

- MCP: `<target>-mcp` (e.g. `rancher-manager-mcp`, `proxmox-ve-mcp`)
- GitOps: `gitops-<scope>` (e.g. `gitops-core`, `gitops-fleet`)
- Operators: `<workload>-operator`
- Shared agent assets: `agent-<thing>` (e.g. `agent-skills`, `agent-workspace`)

Keep repo names lowercase, hyphenated, short. Descriptions carry the mission sentence; names carry the role.

### Evocative names for pipeline “products”

Allowed for control-plane / fleet pieces where a metaphor aids memory (e.g. Nauarchos, Dioptra, Enodios, Freya).

Rules:

1. **One metaphor family per surface** — prefer Greek/command/survey language for the agent fleet; don’t mix random franchises into the same layer.
2. **Explain in the description** — name + short gloss (“Ναύαρχος — fleet admiral”) + what it does in plain English.
3. **Independence** — the evocative name must make sense if we swap runtimes (Cursor, Hermes Agent, custom). It must not be a reskin of an upstream brand.
4. **Light mythos, light game nods** — Titanfall / Data Knife stays an org-level wink, not a repo naming system.

### Upstream products are integrations, not identity

Upstream names (Hermes Agent, Hermes models, Cursor, vLLM, Rancher, …) belong in:

- README “integrates with …” sections
- Topics only on repos whose *primary* job is that integration (e.g. Enodios ↔ Hermes Agent + vLLM)
- Adapter / provider field names in APIs (`runtime: hermes | cursor | custom`)

They do **not** belong in:

- New DataKnifeAI product names or “Hermes-*” repo naming
- Org-wide topics on multi-runtime projects (prefer `agents`, `control-plane`, `mcp`, etc.)
- Framing the fleet as a Hermes ecosystem when the north star is a multi-runtime pipeline

**Enodios** is correctly Hermes-shaped (bootstrap for that stack). **Nauarchos** / **Dioptra** should stay fleet-shaped; mention Hermes as a first/runtime adapter, not as the product identity.

### Topics and descriptions

- Description = role in the pipeline + one clause of purpose (≤ ~160 chars when used as GitHub short description).
- Topics = capability and stack (`agents`, `kubernetes`, `mcp`, `gitops`, …), not every dependency.
- Add an upstream topic only when discovery for that integration is a primary goal of the repo.

## Decision checklist (new repo)

1. Which north-star **layer** is this?
2. Would a stranger find it via a **descriptive** name? If yes → use that.
3. If evocative: does the metaphor survive swapping the first runtime/model? If no → rename before publish.
4. Does the README lead with **DataKnifeAI’s job**, then list integrations?
5. Any upstream mark used only as integration credit, not as our brand?

## Out of scope

- Renaming existing repositories (do that only with an explicit migration plan).
- Trademark legal advice—when in doubt, don’t echo upstream product names in *our* product titles.
