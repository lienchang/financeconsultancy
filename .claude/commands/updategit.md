# /updategit

You are running the `/updategit` command. Execute the following steps in order. Stop and report to the user if any step fails.

---

## Step 1 — Security Scan (secrets detection)

Search the working tree for common secret patterns before anything is pushed to the internet. Run ALL of the following grep checks and collect findings:

```
# Patterns to search for (case-insensitive, across all tracked files):
- password\s*=\s*['"][^'"]{3,}
- api[_-]?key\s*=\s*['"][^'"]{3,}
- secret\s*=\s*['"][^'"]{3,}
- token\s*=\s*['"][^'"]{3,}
- auth\s*=\s*['"][^'"]{3,}
- private[_-]?key
- BEGIN (RSA|EC|OPENSSH|PGP) PRIVATE KEY
- [A-Za-z0-9+/]{40,}={0,2}   (long base64 strings — flag for review)
- formsubmit\.co/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}  (real email in form action)
```

Use the Grep tool with output_mode "content" to run these searches across the repo. Exclude `.git/` and `node_modules/`.

**If any real secrets are found:** Stop immediately. Report exactly which file and line contains the secret. Do NOT proceed to commit or push. Instruct the user to remove the secret, add the file to `.gitignore` if needed, and re-run `/updategit`.

**If only the FormSubmit placeholder (`YOUR-EMAIL@example.com`) is found:** that is safe — note it in the report but continue.

---

## Step 2 — Check for sensitive files that should not be committed

Using the Glob tool, check whether any of these file patterns exist and are tracked by git:

- `.env`, `.env.*`
- `*.pem`, `*.key`, `*.p12`, `*.pfx`
- `credentials.json`, `secrets.json`, `config.local.*`
- `*.sqlite`, `*.db`

If any are found, check `git ls-files` to see if they are tracked. If tracked, warn the user and stop. If untracked, note they are safely ignored and continue.

---

## Step 3 — Update README.md

Read the current `index.html` to understand any changes since the last README update. Then read `README.md`. If the README is missing sections or is out of date with the current page content (new sections, changed form email, changed hero image URL, etc.), update it. The README must always include:

- Project description
- Live demo link (GitHub Pages URL, derived from the remote: `https://<owner>.github.io/<repo>/`)
- Features list
- Getting started / local dev instructions
- Project structure
- Customisation guide (colours, hero image, form email)
- Deployment notes

Keep the README concise — no marketing fluff.

---

## Step 4 — Update GitHub repo About / description

Use the GitHub CLI to set a short repo description and topic tags. Run:

```bash
gh repo edit --description "Static landing page for an Investment Strategy consultancy — HTML/CSS/JS, no build step" --add-topic landing-page --add-topic finance --add-topic github-pages --add-topic html-css-js
```

If `gh` is not authenticated or the command fails, note it and skip this step (it is non-critical).

---

## Step 5 — Verify GitHub Actions workflow includes security scan

Read `.github/workflows/deploy.yml`. Confirm it contains a `gitleaks` or secret-scan step BEFORE the deploy step. If the security scan step is missing, update the workflow file to add it (see the workflow template in the notes below). Do not remove any existing steps.

**Workflow security scan step to insert before "Upload artifact":**

```yaml
      - name: Secret scan (gitleaks)
        uses: gitleaks/gitleaks-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

## Step 6 — Stage, commit, and push

1. Run `git status` to see what has changed.
2. Stage only the relevant files: `README.md`, `.github/workflows/deploy.yml`, `.claude/commands/updategit.md`, and any other intentionally modified tracked files. Do NOT use `git add -A` blindly — review the file list first.
3. If there is nothing to commit, report "Nothing to commit — repo is already up to date" and stop.
4. Commit with a clear message summarising what changed.
5. Run `git push origin main`.
6. Report the push result and the GitHub Pages URL to the user.

---

## Final report to user

Output a summary table:

| Step | Status | Notes |
|------|--------|-------|
| Security scan | ✓ / ✗ | |
| Sensitive file check | ✓ / ✗ | |
| README updated | ✓ / skipped | |
| Repo About updated | ✓ / skipped | |
| Workflow has secret scan | ✓ / added / already present | |
| Pushed to GitHub | ✓ / ✗ | commit SHA |
| GitHub Pages | deploying | URL |
