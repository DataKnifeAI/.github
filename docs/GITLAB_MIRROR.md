# GitLab group profile mirror

Canonical source: this repo (`DataKnifeAI/.github`).  
Mirror target: [`dk-raas/dkai/gitlab-profile`](https://gitlab.com/dk-raas/dkai/gitlab-profile) (GitLab group README for [`dk-raas/dkai`](https://gitlab.com/groups/dk-raas/dkai)).

## Workflow

[`.github/workflows/mirror-gitlab-profile.yml`](../.github/workflows/mirror-gitlab-profile.yml) runs on push to `main` and `workflow_dispatch`. It remaps paths, then force-pushes with [`push-gitlab-mirror`](https://github.com/DataKnifeAI/github-workflows/tree/main/.github/actions/push-gitlab-mirror) from `DataKnifeAI/github-workflows` (same action other org repos use).

## Path mapping

| GitHub (this repo) | GitLab (`gitlab-profile`) |
|--------------------|---------------------------|
| `gitlab-profile/README.md` | `README.md` (group README) |
| `gitlab-profile/MANUAL_SETUP.md` | `MANUAL_SETUP.md` |
| `docs/*.md` | `docs/*.md` |
| `gitlab-profile/docs/*.md` | `docs/*.md` (overlay; e.g. `PROJECT_SETTINGS.md`) |
| `profile/assets/*` | `assets/*` |

**Not mirrored as the group README:** `profile/README.md` stays the GitHub org landing page only. GitHub root `README.md` is also GitHub-only.

## Secrets / vars

| Name | Where | Required | Purpose |
|------|-------|----------|---------|
| `GITLAB_TOKEN` | Repo secret on `DataKnifeAI/.github`, **or** org secret available to this repo | **Yes** | PAT / project token with `write_repository` (and usually `api`) on `dk-raas/dkai/gitlab-profile` |

Optional workflow inputs (hardcoded defaults today): `gitlab_base_url` = `https://gitlab.com`, `remote_branch` = `main`. No `GITLAB_HOSTNAME` var is required.

Set the repo secret (same pattern as `rancher-deploy` and other MCP/infra mirrors):

```bash
gh secret set GITLAB_TOKEN -R DataKnifeAI/.github
# paste PAT with push access to dk-raas/dkai/gitlab-profile
```

## GitLab project settings for the mirror

The push action **force-pushes** `main`. Match other mirrors (e.g. `devops/rancher-deploy`): protect `main`, **Allowed to push/merge = Maintainers**, **allow force push = on**, approvals **0** (solo-dev). Do not require a pipeline on this meta project unless CI is intentionally added on GitLab.

Full group policy (normal MR path + CI/Mirror exception + token guidance): [`gitlab-profile/docs/PROJECT_SETTINGS.md`](../gitlab-profile/docs/PROJECT_SETTINGS.md).
