# Lab Tester Workflow

> **Prerequisite:** Complete the **Training Guide** before using this workflow.
> **What this is:** The repeatable process you follow for every piece of work. Follow it in order.
> **Related files:** **Reference Guide** (markdown syntax, style, Copilot prompts) • **Advanced Scenarios** (terminal workflow, Copilot branches)

---

## Starting work

Every task starts the same way, whether it comes from an issue or a lab review request.

### 1. Sync main

- [ ] In VS Code, select the **branch name** in the bottom-left corner → select **main**
- [ ] Select the **sync icon** (circular arrows) next to the branch name

> **Stuck?** Ask Copilot: *"Is my local main branch up to date with origin?"*

### 2. Create a branch

- [ ] Select the **branch name** (bottom-left, should say `main`) → select **Create new branch...**
- [ ] Type a name: `fix/lab01-issues-42-47-51` (lowercase, hyphens, no spaces)
- [ ] Press **Enter**
- [ ] Confirm the bottom-left now shows your new branch name — not `main`

### 3. Publish the branch

- [ ] Open the **Source Control** panel (`Ctrl+Shift+G`)
- [ ] Select **Publish Branch** — this pushes the empty branch to the remote so it exists on GitHub

### 4. Make changes

- [ ] Edit the files that need fixing
- [ ] Use **Copilot Chat** to help validate your edits (see the **Reference Guide** for prompts)
- [ ] Save all files (`Ctrl+S`)
- [ ] In the **Source Control** panel, select any changed file to see a **side-by-side diff**
- [ ] Review every change — make sure you only changed what you intended
- [ ] To undo an unintended change, right-click the file → **Discard Changes**

**Copilot prompt ideas:**
    - *"Does this step match the current Microsoft docs for [feature]?"*
    - *"Rewrite this step to match the tone and style of the rest of the file"*
    - *"Check if my changes are consistent with how other labs in this repo describe this process"*

### 5. Commit frequently

- [ ] Stage files: select the **+** next to each file (or **+** on the **Changes** header for all)
- [ ] Type a meaningful commit message in the **Message** box
- [ ] Select the **checkmark** to commit
- [ ] Select **Sync Changes** to push your commit to GitHub - the first time will say **Publish branch**

**Commit early and often**. Each commit should describe what changed and why.

**Examples of good commit messages:**
- `Fix typo in Lab 01 Task 2 Step 5 (Fixes #42)`
- `Update screenshot for new workspace creation UI (Fixes #47)`
- `Fix step numbering in Lab 01 Task 3 (Fixes #51)`

**Examples of bad commit messages:**
- `fixed stuff`
- `changes`
- `update`

### 6. Test the entire lab

> **This is not optional.** Any time you change a lab file or its supporting assets (code, data, images), you must test the full lab.

**Which environment to test in:**

- [ ] Test in the **Skillable VM** unless the content developer tells you otherwise. Skillable is the hosted lab environment where learners complete exercises — the content developer will provide access and instructions during onboarding.
- [ ] If the content developer asks you to verify the **bring your own subscription (BYOS)** experience, follow the setup instructions in the repo (typically in `Allfiles/Labs/00-Setup/` or a setup section at the start of the lab) using your own subscription. Confirm the setup steps are complete and accurate.

**How to test:**

- [ ] Follow **every** step, in order, exactly as written
- [ ] Always start with a **clean environment** — this means starting from scratch. Do not reuse a lab environment, workspace, or resources from a previous test run. If the lab creates resources (such as a workspace, database, or storage account), delete them or use a fresh environment before testing again.
- [ ] Confirm your change works and nothing downstream is broken

**Check exercise modularity:**

- [ ] Verify that each exercise works independently — a learner should be able to complete any exercise without depending on work done in a previous exercise, unless the lab explicitly states otherwise
- [ ] If an exercise depends on a resource from a previous exercise (such as a table, workspace, or file), it needs its own setup step — or the instructions need to direct the learner to complete the setup exercise first
- [ ] If you find a dependency that cannot be resolved in your current PR, document it as a separate issue and note it in your PR description

> **Note**: Some legacy labs have exercise dependencies that have not been refactored yet. Flag these — do not silently ignore them — but do not block your PR on them either.

If your change breaks a later step, fix it before continuing. Do not create a PR with a known broken lab.

### 7. Create a PR

- [ ] Go to the repository on GitHub in your browser
- [ ] Select **Compare & pull request** on the yellow banner
- [ ] Verify: **base** is `main`, **compare** is your branch, both on the same repo
- [ ] Write the PR description — include what you changed and your test results
- [ ] Select **Create pull request**
- [ ] Assign the content developer as a reviewer
- [ ] **Stop.** Wait for the content developer to review and merge

**Example of a good PR description:**

```
Fixes #42, #47, #51.

## Proposed changes
- Fixed typo in Task 2
- Updated screenshot in Task 3
- Fixed step numbering in Task 3
```

> **Copilot can help:** *"Write a PR description for my current branch. I fixed issues #42, #47, and #51 in Lab 01."*

### 8. After the PR is merged

- [ ] If your PR description used `Fixes #XX`, GitHub auto-closes those issues when the PR is merged. Verify the issues are closed — if any were missed, close them manually.
- [ ] Select the branch name (bottom-left) → select **main**
- [ ] Select the **sync icon** to pull the latest
- [ ] The content developer deletes the remote branch when merging
- [ ] To clean up your local copy, open the Command Palette `Ctrl+Shift+P` → `Git: Delete Branch` → select your old branch

---

## Rules

1. **Never edit `main` directly.** All changes go through branches and PRs.
2. **One branch at a time** unless the branches touch completely different files.
3. **Group fixes** to prevent extra administration. Multiple changes → one branch = one PR.
4. **Commit frequently** with meaningful messages that reference issue numbers.
5. **Test the full lab** every time you change a lab file or its supporting assets.
6. **If you see merge conflicts**, ask for help.
7. **When in doubt, ask Copilot** to explain or troubleshoot first.
8. **Still stuck?** Ask for help.

---

## Quick reference

```
STARTING WORK
  1. Branch name (bottom-left) → main → sync icon
  2. Branch name → Create new branch → type name → Enter
  3. Source Control → Publish Branch
  4. Edit files → save → review diffs
  5. Stage (+) → commit message → checkmark (repeat often)
  6. Test the full lab end-to-end
  7. Sync Changes → GitHub → Create PR → wait for review

AFTER MERGE
  1. Branch name → main → sync icon
  2. Ctrl+Shift+P → Git: Delete Branch → select old branch
```
