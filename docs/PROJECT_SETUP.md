# Project setup — agent skills, rules & workspace

For **new and existing** DataKnifeAI repositories: review these shared baselines before inventing project-local Cursor skills, rules, or Cloud Agent layouts.

Keep this page short. Install steps and skill content live in the linked repos.

## Review checklist

| Resource | When to review | What you get |
|----------|----------------|--------------|
| [`agent-skills` / `rules/`](https://github.com/DataKnifeAI/agent-skills/tree/main/rules) | Any product repo that uses Cursor agents | Org-wide Cursor rule (`dataknifeai-common.mdc`); **vendor** a copy into the product repo (no install script) |
| [`DataKnifeAI/agent-skills`](https://github.com/DataKnifeAI/agent-skills) | Adding Cursor/agent skills, or before writing a one-off skill in a product repo | Shared CLI/workflow skills (`gh`, `glab`, `kubectl`, …); install via Makefile / `install-skills.sh` |
| [`DataKnifeAI/agent-workspace`](https://github.com/DataKnifeAI/agent-workspace) | Standing up Cursor Cloud Agents (managed or self-hosted), or a Coder multi-repo workspace | Git baseline with `agent-skills` as a submodule, hooks placeholder, Coder layout rules |

## Shared Cursor rules (vendor-first)

Canonical source: [`agent-skills/rules/dataknifeai-common.mdc`](https://github.com/DataKnifeAI/agent-skills/blob/main/rules/dataknifeai-common.mdc) (see the [rules README](https://github.com/DataKnifeAI/agent-skills/blob/main/rules/README.md)).

1. **Review** `agent-skills/rules/` before writing org-wide agent defaults in a product repo.
2. **Vendor** (copy and commit) `.cursor/rules/dataknifeai-common.mdc` into each product repo — no install script; day-to-day clones need no extra step.
3. **Thin overrides** — keep the vendored common file unmodified; add `.cursor/rules/<project>.mdc` (or glob-scoped rules) for stack-specific conventions. Template: [`project-override.mdc.example`](https://github.com/DataKnifeAI/agent-skills/blob/main/rules/templates/project-override.mdc.example).
4. **Optional** short root `AGENTS.md` that points at the vendored rule and any project overrides (one screen; do not restate org branding).

When the org baseline changes, refresh product repos by re-copying the canonical file from `agent-skills`.

## Guidance

1. **Prefer shared skills** — If a skill is useful beyond one repo, add or extend it in `agent-skills` instead of duplicating under `.cursor/skills/` in the product repo.
2. **Cloud Agent / pool baseline** — Use `agent-workspace` (clone or fork) as the Cloud Agent git root when you need org skills + hooks without stuffing them into every application repo. Init submodules after clone.
3. **Product repos stay focused** — Application code stays in its own repo; optional thin project skills/rules only when they are truly product-specific.
4. **Align with org docs** — Branding, naming, settings, and presentation: [ORG_BRANDING](./ORG_BRANDING.md), [NAMING](./NAMING.md), [REPO_SETTINGS](./REPO_SETTINGS.md), [REPO_PRESENTATION](./REPO_PRESENTATION.md).

## Out of scope here

- Full install commands, skill authoring, or Cloud Agent pool ops — see each repo’s README.
- Bulk-vendoring rules or skills into every product repo in one pass; adopt when a project is touched.
