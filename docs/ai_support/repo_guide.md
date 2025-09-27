# Using a PAT (Template – No Secrets)
Do **not** paste tokens in this repo. Store a fine-grained PAT as a GitHub Actions Secret:
- Repo Settings → Secrets and variables → Actions → **New repository secret**
- Name it: `MIRROR_TOKEN`
- Scope it **only** to the public mirror repository with minimal permissions.

In workflows, reference it **only** as `${{ secrets.MIRROR_TOKEN }}`. Never commit a PAT to git.
