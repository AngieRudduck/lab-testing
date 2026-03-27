# Lab Tester Advanced Scenarios

> **Who this is for:** Anyone comfortable with the standard workflow who wants to use the terminal or work with Copilot-created branches.
> **Prerequisite:** You should be confidently using the **Workflow** before attempting anything in this guide.
> **Note:** These scenarios are not required for day-to-day work. They cover situations you may encounter as you gain experience.

---

## Table of contents

- Using the terminal for the workflow
- Useful terminal commands
- Working with a Copilot branch
- Working with a Copilot branch (terminal)

---

## Using the terminal for the workflow

The **Workflow** uses the VS Code GUI. Every step can also be done from the terminal. This section gives you the terminal equivalents.

### Opening the terminal

Press `` Ctrl+` `` in VS Code, or **Terminal** menu → **New Terminal**. Make sure you're in the repo folder.

### The workflow in terminal commands

**Step 1 — Sync main:**

```
git checkout main
git pull origin main
```

**Step 2 — Create a branch:**

```
git checkout -b fix/lab01-issues-42-47-51
```

**Step 3 — Publish the branch:**

```
git push -u origin fix/lab01-issues-42-47-51
```

**Steps 4–6 — Make changes, commit, test** (repeat as needed):

```
# edit files in VS Code, save
git add .
git commit -m "Fix typo in Lab 01 Task 2 Step 5 (Fixes #42)"
git push
```

**Step 7 — Create a PR:** Go to GitHub in your browser → **Compare & pull request**.

**Step 8 — After the content developer merges:**

```
git checkout main
git pull origin main
git branch -d fix/lab01-issues-42-47-51
```

### Branch naming convention

- `fix/labXX-brief-description` for bug fixes
- `update/labXX-brief-description` for content updates
- Lowercase, hyphens, no spaces

### Commit message rules

- Start with a verb: Fix, Update, Add, Remove, Replace
- Reference issue numbers: `(Fixes #42)`
- Keep under 72 characters if possible

---

## Useful terminal commands

Not part of the standard workflow, but helpful for troubleshooting.

| Command | What It Does |
|---|---|
| `git status` | Show modified, staged, and untracked files |
| `git branch` | List local branches (current marked with `*`) |
| `git log --oneline -10` | Show last 10 commits |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git fetch origin` | Download remote branch info without merging |
| `git checkout branch-name` | Switch to a different branch |
| `git branch -d branch-name` | Delete a local branch (merged only) |

> **Tip:** If a command fails, read the error message — Git usually tells you exactly what went wrong.

### Git cheat sheet

Download and keep handy: `https://training.github.com/`

A printable reference for common Git commands. You do not need to memorize these — the workflow tells you what to do at each step.

---

## Working with a Copilot branch

When you assign an issue to GitHub Copilot, Copilot creates a branch and opens a PR with proposed changes. You may be asked to review and refine these.

### How to pick up a Copilot branch (GUI)

- [ ] Sync main: select the **branch name** (bottom-left) → select **main** → select the **sync icon**
- [ ] Open the Command Palette: `Ctrl+Shift+P` → type **Git: Fetch** → select **Fetch From All Remotes**
- [ ] Select the **branch name** (bottom-left) → select the Copilot branch (such as `copilot/fix-42`)
- [ ] Review the changes Copilot made — open each changed file and read the diff
- [ ] Edit anything that needs to be corrected or improved
- [ ] Stage, commit, and sync your changes (same as Steps 5–6 in the standard workflow)
- [ ] Test the full lab end-to-end

> **Important:**
> - The Copilot branch already has a PR — do **not** create a new one
> - Your commits push to the existing PR automatically when you sync
> - Treat Copilot's changes like a first draft — verify everything against the actual product
> - If the changes are fundamentally wrong, tell the content developer instead of trying to salvage them

---

## Working with a Copilot branch (terminal)

```
git checkout main
git pull origin main
git fetch origin
git checkout copilot/fix-42
# review and edit files
git add .
git commit -m "Refine Copilot changes for issue #42: corrected step numbering"
git push origin copilot/fix-42
```

> **If the branch doesn't appear:** Run `git fetch origin` first — it downloads remote branch info.

The existing PR updates automatically — do NOT create a new PR.

**After the content developer merges:**

```
git checkout main
git pull origin main
git branch -d copilot/fix-42
```

---

## Quick reference

### Standard workflow (terminal)

```
git checkout main
git pull origin main
git checkout -b fix/labXX-description
# make edits, save files
git add .
git commit -m "Fix description (Fixes #XX)"
git push
# test the full lab → GitHub → Create PR → wait for review
```

### After PR is merged

```
git checkout main
git pull origin main
git branch -d fix/labXX-description
```

### Copilot branch

```
git checkout main
git pull origin main
git fetch origin
git checkout copilot/branch-name
# review, edit, save
git add .
git commit -m "Refine Copilot changes for issue #XX"
git push origin copilot/branch-name
```

---

## Reference links

| Resource | URL |
|---|---|
| Git Cheat Sheet (GitHub Training Kit) | `https://training.github.com/` |
| Git Documentation | `https://git-scm.com/doc` |
| GitHub Docs — Pull Requests | `https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests` |

---

> **When in doubt: stop and ask.** It is better to ask the content developer than to push changes you are unsure about.
