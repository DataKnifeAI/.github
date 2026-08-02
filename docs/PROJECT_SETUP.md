# Project setup — agent skills & workspace

For **new and existing** DataKnifeAI repositories: review these shared baselines before inventing project-local Cursor skills or Cloud Agent layouts.

Keep this page short. Install steps and skill content live in the linked repos.

## Review checklist

| Resource | When to review | What you get |
|----------|----------------|--------------|
| [`DataKnifeAI/agent-skills`](https://github.com/DataKnifeAI/agent-skills) | Adding Cursor/agent skills, or before writing a one-off skill in a product repo | Shared CLI/workflow skills (`gh`, `glab`, `kubectl`, …); install via Makefile / `install-skills.sh` |
| [`DataKnifeAI/agent-workspace`](https://github.com/DataKnifeAI/agent-workspace) | Standing up Cursor Cloud Agents (managed or self-hosted), or a Coder multi-repo workspace | Git baseline with `agent-skills` as a submodule, hooks placeholder, Coder layout rules |

## Guidance

1. **Prefer shared skills** — If a skill is useful beyond one repo, add or extend it in `agent-skills` instead of duplicating under `.cursor/skills/` in the product repo.
2. **Cloud Agent / pool baseline** — Use `agent-workspace` (clone or fork) as the Cloud Agent git root when you need org skills + hooks without stuffing them into every application repo. Init submodules after clone.
3. **Product repos stay focused** — Application code stays in its own repo; optional thin project skills only when they are truly product-specific.
4. **Align with org docs** — Branding and naming live in this `.github` docs set ([ORG_BRANDING](./ORG_BRANDING.md), [NAMING](./NAMING.md); repository settings guidelines when merged).

## Out of scope here

- Full install commands, skill authoring, or Cloud Agent pool ops — see each repo’s README.
- Bulk-changing every product repo to vendor `agent-skills`; adopt when a project actually needs shared skills or a Cloud Agent baseline.
