# Manual setup — publish `gitlab-profile` on GitLab

**Ongoing sync:** after bootstrap, prefer the GitHub Actions workflow in `DataKnifeAI/.github` (see [docs/GITLAB_MIRROR.md](https://github.com/DataKnifeAI/.github/blob/main/docs/GITLAB_MIRROR.md)). This file remains for one-time project/group wiring.

Auth blockers observed during scaffolding: `glab` had **no token** (`glab auth status` → 401), and the Cursor GitLab MCP server was **unauthenticated**. Use these steps after logging in.

## 0. Authenticate

```bash
glab auth login
# HTTPS + token (api, write_repository) or web flow
glab auth status
glab api user   # should print your user JSON
```

## 1. Create the group README project

**Option A — GitLab UI (recommended, wires Group README automatically)**

1. Open https://gitlab.com/groups/dk-raas/dkai/-/edit  
2. **Settings → General → Group README → Add README**  
3. Confirm creation of project `gitlab-profile`  
4. Replace the generated `README.md` with the content from this scaffold (or push from git — below)

**Option B — CLI**

```bash
glab repo create gitlab-profile \
  --group dk-raas/dkai \
  --description "DataKnifeAI group profile and org docs (GitLab parallel to GitHub .github)" \
  --visibility public \
  --defaultBranch main

# Then open Group Settings → General → Group README and point/add README
# (UI “Add README” is the reliable way to attach it to the group overview)
```

## 2. Push this scaffold

```bash
cd /mnt/game2/git/dkai-gitlab-profile
git init -b main
git remote add origin git@gitlab.com:dk-raas/dkai/gitlab-profile.git
git add README.md docs assets MANUAL_SETUP.md
git commit -m "$(cat <<'EOF'
docs: add DataKnifeAI GitLab group profile and org docs

EOF
)"
git push -u origin main
# Prefer MR if the project already has protected main with content:
# git checkout -b docs/gitlab-profile-bootstrap
# git push -u origin HEAD
# glab mr create --fill
```

## 3. Update group description

Paste tagline (+ GitHub link) at https://gitlab.com/groups/dk-raas/dkai/-/edit, or:

```bash
glab api -X PUT groups/dk-raas%2Fdkai \
  -f description="$(cat <<'EOF'
Learn and solve problems with AI tools—built to stay maintainable through automation, and aligned with software freedom.

Canonical org: https://github.com/DataKnifeAI
EOF
)"
```

## 4. Avatar

Already set to `dataknifeai-org-logo-v1c-256.png`. Optional upgrade: upload `assets/dataknifeai-org-logo-v1c-384.png` on the same edit page.

## 5. Do not create

- A second `org-docs` project unless `gitlab-profile` feels too crowded — put docs under `docs/` here first.
- Mirrors of `agent-skills` / `agent-workspace` solely for parity.
- Group wiki as the org doc home (versioned Markdown in this project is better).
