# DataKnifeAI GitLab project settings

Recommended **common pattern** for first-party projects under [dk-raas/dkai](https://gitlab.com/dk-raas/dkai).

Parallel to GitHub [`REPO_SETTINGS`](https://github.com/DataKnifeAI/.github/blob/main/docs/REPO_SETTINGS.md) (branch protection → GitLab protected branches / MR approvals). Solo-maintainer defaults: safe and automatable, not multi-reviewer gates.

Related: [ORG_BRANDING.md](./ORG_BRANDING.md), [PROJECT_SETUP.md](./PROJECT_SETUP.md).  
GitHub → GitLab push mirror details (group profile): [GITLAB_MIRROR.md](https://github.com/DataKnifeAI/.github/blob/main/docs/GITLAB_MIRROR.md) in `DataKnifeAI/.github`.

This document describes the **target** state. Prefer intentional fixes over silent bulk churn.

## Scope

| Kind | Apply? |
|------|--------|
| First-party product / infra / tooling | Yes |
| This meta project (`gitlab-profile`) | Yes (keep surface small) |
| GitHub → GitLab **push mirrors** (most of this group) | Yes — use [normal solo-dev](#new-project-defaults) **plus** the [CI / Mirror exception](#cimirror-exception-github--gitlab-direct-push) |
| Forks of upstream | Partial — don’t impose org branding onto upstream identity |

Group baseline today: `default_branch_protection_defaults` ≈ Maintainers may push/merge, force-push off for **new** projects. Active mirrors override force-push per the exception below.

## Two paths (read this first)

| Path | Who | How `main` moves |
|------|-----|------------------|
| **Normal (humans)** | Maintainers / Developers | Merge request → squash preferred → **0** required approvals → delete source branch |
| **CI / Mirror** | GitHub Actions with `GITLAB_TOKEN` | Direct (often **force**) push to protected `main` via Maintainer-level token |

Humans should still use MRs on GitLab even though Maintainers *can* push. The push/force-push allowance exists so automation is not blocked—not as a habit for interactive work.

## New project defaults

| Setting | Recommended | Notes |
|---------|-------------|--------|
| Default branch | `main` | Match GitHub |
| Visibility | Leave as-is unless intentionally changing | Do not flip public/private in bulk |
| Issues | **On** | Many projects still track on GitHub — either is fine; don’t split casually |
| Wiki | **Off** | Prefer Markdown in-repo (`README` / `docs/`) |
| Squash commits when merging | **On** (`default_on`) | Linear, readable `main` |
| Merge commit / fast-forward | Optional | Squash is the default contributor path |
| Delete source branch on merge | **On** | Avoids stale branches |
| Auto-merge | Optional | Useful once CI is reliable |
| Required approvals | **0** | Solo-dev; raise when a second person exists |
| Pipeline must succeed to merge | **Only when CI is reliable** | Don’t require empty/flaky pipelines |

```bash
# Example (project path URL-encoded)
glab api -X PUT projects/dk-raas%2Fdkai%2Fdevops%2Francher-deploy \
  -f default_branch=main \
  -f issues_enabled=true \
  -f wiki_enabled=false \
  -f squash_option=default_on \
  -f remove_source_branch_after_merge=true
```

## Protected branches (solo-dev + mirror)

Protect `main` on every active first-party project (`master` only if that branch still exists).

### Normal protection shape

| Rule | Recommended (solo) | GitLab mapping |
|------|--------------------|----------------|
| Branch protected | **Yes** | Protected branch `main` |
| Who can **merge** | Maintainers | Allowed to merge: **Maintainers** |
| Who can **push** | Maintainers | Allowed to push: **Maintainers** (enables token push; humans use MRs) |
| Force push | See exception | **Off** for non-mirror-only experiments; **On** for push-mirror targets (below) |
| Code Owner approval | **Off** | Enable only with real `CODEOWNERS` + >1 reviewer |
| Required approvals | **0** | Project approvals / approval rules |

“Allowed to push: **No one**” (MR-only) is stricter and fine for GitLab-native repos that are **not** GitHub push mirrors—but it **blocks** `GITLAB_TOKEN` direct push unless you add that bot/token user explicitly to Allowed to push.

### CI/Mirror exception (GitHub → GitLab direct push)

Most projects under `dk-raas/dkai` receive updates from GitHub Actions via [`push-gitlab-mirror`](https://github.com/DataKnifeAI/github-workflows/tree/main/.github/actions/push-gitlab-mirror) (force-push `HEAD` → `main`). Pull mirroring on GitLab.com Free is unavailable; **push from GitHub** is the supported path.

**Required on each mirrored project:**

| Setting | Value | Why |
|---------|-------|-----|
| Protected `main` | Yes | Stops casual branch deletion / unmanaged history |
| Allowed to push | **Maintainers** | `GITLAB_TOKEN` must authenticate as a Maintainer-capable identity |
| Allowed to merge | **Maintainers** | Human MR path |
| Allow force push | **Yes** | `push-gitlab-mirror` uses `git push --force` |
| Approvals before merge | **0** | Do not gate automated mirror history on review counts |

Optional harder lockdown later: set Allowed to push to **No one**, then add a dedicated Project Access Token / bot **user** to Allowed to push (and keep force-push enabled for that path). Group/org PAT used as Maintainer is the simpler pattern in use today.

#### Token / secret guidance (`GITLAB_TOKEN`)

| Item | Guidance |
|------|----------|
| Where | GitHub **repo** or **org** secret named `GITLAB_TOKEN`, available to repos that call the mirror action / reusable workflow |
| What | GitLab **Personal Access Token**, **Project Access Token**, or **Group Access Token** |
| Scopes | At least `write_repository`; `api` if the workflow also calls GitLab APIs |
| Role | **Maintainer** (or Owner) on the target project(s)—Developer is not enough for protected `main` with Maintainer-only push |
| Auth form | Action uses `https://oauth2:${GITLAB_TOKEN}@gitlab.com/...` |
| Rotation | Rotate in GitLab, then update the GitHub secret; **do not** commit tokens |
| Do not | Revoke shared tokens without replacing the GitHub secret first; that breaks all mirrors |

Create a Project Access Token (example for one project):

1. GitLab → Project → **Settings → Access tokens**
2. Name e.g. `github-mirror`, role **Maintainer**, scopes `write_repository` (+ `api` if needed), set expiry
3. `gh secret set GITLAB_TOKEN -R DataKnifeAI/<repo>` (or set once as an org secret)

For many mirrors, one **group** access token (or a Maintainer PAT) shared via a GitHub **org** secret is operationally simpler than N project tokens.

```bash
# Protect / re-protect main for a push mirror (form-encoded)
glab api -X POST "projects/<id>/protected_branches" \
  -f name=main \
  -f allow_force_push=true \
  -f code_owner_approval_required=false \
  -F "allowed_to_push[][access_level]=40" \
  -F "allowed_to_merge[][access_level]=40"
# access_level 40 = Maintainer; 0 = No one
```

If `main` is already protected, unprotect then re-protect (or use the UI) so push/force-push flags match the table above.

## When the group grows

| Change | Target |
|--------|--------|
| Required approvals | **1+** for human MRs |
| CODEOWNERS | Add and optionally require |
| Push access | Prefer bot-only on Allowed to push; humans MR-only |
| Force push | Narrow to the mirror bot if GitLab plan/UI allows finer grants |
| Group push rules / compliance | Shared floor for new projects |

## Group-level controls (optional later)

| Capability | When to use |
|------------|-------------|
| Group push rules | Commit message / branch name conventions org-wide |
| Group CI/CD variables | Shared non-secret defaults; secrets still least-privilege |
| Group Access Token for mirrors | One token → GitHub org `GITLAB_TOKEN` for many projects |
| Compliance frameworks | Only if you adopt GitLab Ultimate compliance workflows |
| Instance/group runners | Prefer runners you control for Harbor/k8s jobs |

Do **not** invent a parallel `github-workflows` stack on GitLab unless GitLab CI becomes a primary path. Mirrors may carry `.gitlab-ci.yml` opportunistically for image builds.

## Alignment checklist (audit)

For each project under `dk-raas/dkai`:

- [ ] Default branch `main`
- [ ] Wiki **off**, squash **default_on**, remove source branch on merge **on**
- [ ] `main` protected; merge = Maintainers; approvals **0**
- [ ] If GitHub push-mirror: push = Maintainers **and** allow force push **on**
- [ ] Visibility unchanged unless deliberate
- [ ] `GITLAB_TOKEN` present on the GitHub side for that mirror

## Out of scope

- Changing project visibility in bulk.
- Revoking or rotating tokens without an explicit ops request.
- Cursor skills / Cloud Agent baselines — see [PROJECT_SETUP.md](./PROJECT_SETUP.md) (GitHub-canonical).
