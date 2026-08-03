# DataKnifeAI `.github`

Organization profile and community files for [DataKnifeAI](https://github.com/DataKnifeAI).

| Path | Purpose |
|------|---------|
| [`profile/README.md`](profile/README.md) | Public org landing page (rendered at https://github.com/DataKnifeAI) |
| [`profile/assets/`](profile/assets/) | Org logo assets (1024 header + 384/512 upload sizes) |
| [`docs/ORG_BRANDING.md`](docs/ORG_BRANDING.md) | Canonical mission, profile copy, and avatar guidance |
| [`docs/NAMING.md`](docs/NAMING.md) | Repository naming for the agent pipeline (descriptive vs evocative; upstream integrations) |
| [`docs/PROJECT_SETUP.md`](docs/PROJECT_SETUP.md) | For new/existing projects: review [agent-skills](https://github.com/DataKnifeAI/agent-skills) and [agent-workspace](https://github.com/DataKnifeAI/agent-workspace) |
| [`docs/REPO_SETTINGS.md`](docs/REPO_SETTINGS.md) | Recommended repo settings, branch protection, and security defaults |
| [`docs/GITLAB_MIRROR.md`](docs/GITLAB_MIRROR.md) | GitHub → GitLab group-profile mirror (paths + secrets) |
| [`gitlab-profile/`](gitlab-profile/) | GitLab group README + GitLab-only docs (mirrored to GitLab) |
| [`docs/GITLAB_MIRROR.md`](docs/GITLAB_MIRROR.md) | Mirror workflow, path mapping, and required secrets |

The profile README displays the **1024×1024** logo only. Smaller PNGs are retained for GitHub/GitLab avatar upload—see the branding doc.

## GitLab group profile mirror

Pushes to `main` (and manual **workflow_dispatch**) sync a **mapped** tree to [`dk-raas/dkai/gitlab-profile`](https://gitlab.com/dk-raas/dkai/gitlab-profile) — the [dk-raas/dkai](https://gitlab.com/groups/dk-raas/dkai) group README project.

Workflow: [`.github/workflows/mirror-gitlab-profile.yml`](.github/workflows/mirror-gitlab-profile.yml)  
Push action: [`DataKnifeAI/github-workflows` → `push-gitlab-mirror`](https://github.com/DataKnifeAI/github-workflows/tree/main/.github/actions/push-gitlab-mirror) (same pattern as MCP/infra repos; this workflow remaps paths first).

### Path mapping

GitHub org profile layout ≠ GitLab group README layout, so content is **not** mirrored as-is.

| GitHub (this repo) | GitLab (`gitlab-profile`) |
|--------------------|---------------------------|
| `gitlab-profile/README.md` | `README.md` (group overview) |
| `gitlab-profile/MANUAL_SETUP.md` | `MANUAL_SETUP.md` |
| `docs/*.md` | `docs/*.md` |
| `gitlab-profile/docs/*.md` | `docs/*.md` (overlay; e.g. `PROJECT_SETTINGS.md`) |
| `profile/assets/*` | `assets/*` |

**Not mirrored as the group README:** `profile/README.md` stays GitHub-only (org landing). Root `README.md` here is also GitHub meta and is not pushed to GitLab.

### Required secrets

| Name | Where | Purpose |
|------|--------|---------|
| `GITLAB_TOKEN` | Repo secret on `DataKnifeAI/.github`, **or** an org secret available to this repo | GitLab PAT / project token with `write_repository` (and usually `api`) on `dk-raas/dkai/gitlab-profile` |

Optional input (hardcoded default in the workflow): GitLab base URL `https://gitlab.com` (same as other mirrors; no `GITLAB_HOSTNAME` var required).

Set the secret (do not commit tokens):

```bash
# Reuse the same token used by other DataKnifeAI mirror repos (e.g. rancher-deploy)
gh secret set GITLAB_TOKEN -R DataKnifeAI/.github
# paste token when prompted
```

### GitLab branch protection

The push action **force-pushes** `main` (same as other DataKnifeAI mirrors). On `gitlab-profile`, protect `main` but allow Maintainers to force-push (see sibling projects such as `dk-raas/dkai/devops/rancher-deploy`). Keep required approvals at **0** for solo-dev; human edits should still prefer MRs when not relying on the mirror job.
