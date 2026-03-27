# Lab Tester Training Guide

> **Who this is for:** Anyone who works with labs in MicrosoftLearning repositories.
> **When to complete:** Finish all training and setup in this document **before** starting any lab work.
> **Next step:** After completing this guide, move to the **Lab Tester Workflow**.

---

## Table of contents

- Terminology
- Purpose of this training guide
- Setup checklist
- Required training
- Key concepts you must understand
- Lab delivery models
- Exercise modularity
- Understanding repository structure
- Managing multiple repositories
- Issue triage — how to evaluate work
- Reference links

---

## Terminology

In these documents and in the repositories, **lab** and **exercise** are used interchangeably. A single instruction file (such as `01-lakehouse.md`) is one lab — or one exercise. You may also see the term **exercise** used to describe a section within a lab that has multiple tasks. We use **exercise** for public definition, but may refer to them as labs internally.

---

## Purpose of this training guide

This guide prepares you to work with labs in MicrosoftLearning repositories. You support **multiple content developers** across **multiple lab repositories** as a triage and QA resource. The labs cover a range of Microsoft technologies and products. You are not expected to be an expert in every technology. The lab instructions are written so that a person unfamiliar with the product can complete the exercises by following the steps as written. Your job is to follow those steps exactly as a learner would, identify what is broken or confusing, and make appropriate changes.

This requires **adaptability and critical thinking**. You will encounter unfamiliar products, unexpected errors, and ambiguous instructions. When that happens, your approach should be:

1. **Follow the instructions** — do exactly what they say, nothing more
1. **Search the docs** — use Copilot to search Microsoft Learn or check the product documentation
1. **Test it** — try the step in the actual product to see what happens
1. **Ask the content developer** — if you still cannot resolve it, escalate

Your work may start in one of two ways:

1. **An issue is assigned to you** — someone reported a problem with a lab, and you need to investigate and fix it.
2. **You are asked to review a lab** — you go through the lab end-to-end as a learner would, document what works and what doesn't, and fix what's broken.

In both cases, the process is the same:

- Test the lab by following every step exactly as written
- Identify what's broken, confusing, or outdated
- Fix it using the GitHub workflow (sync, branch, commit, PR)
- Test the lab again to make sure your changes don't impact other tasks
- Document your testing results in the PR

Your judgment matters. You need to determine whether a reported issue is a real content problem, a user error, or something outside the scope of the lab. This guide gives you the GitHub skills to do the mechanical work. The rest — following instructions precisely, noticing when something is wrong, and figuring out the right fix — is on you.

---

## Setup checklist

Complete every item in this section before starting training.

### Required software

- [ ] **VS Code** installed — download from `https://code.visualstudio.com/`
- [ ] **Git** installed — download from `https://git-scm.com/downloads`
- [ ] **GitHub account** with contributor access granted to the repository you are testing (you will work directly on the repo — no personal fork)

### Get familiar with VS Code

VS Code is where you do all of your work — editing files, managing branches, committing changes, and using Copilot. If you have not used VS Code before, complete the following before continuing:

- [ ] Watch the introductory videos on the [Visual Studio Code YouTube channel](https://www.youtube.com/@code) — start with the "Getting Started" playlist
- [ ] Read [Personalize VS Code](https://code.visualstudio.com/docs/getstarted/personalize-vscode) to set up your editor
- [ ] Complete the [Introduction to Visual Studio Code](https://aiskillsnavigator.microsoft.com/explore/search/module-5306b2f480ff96d4e84ac71ede4c7287e1683c09c26bec36f145ba8fad2ec4c1) module on AI Skills Navigator

You should be comfortable with:
- Opening folders and files in VS Code
- Using the **Command Palette** (`Ctrl+Shift+P`)
- Navigating the **Source Control** panel (`Ctrl+Shift+G`)
- Using the **Extensions** panel (`Ctrl+Shift+X`)
- Opening and using the **integrated terminal** (`` Ctrl+` ``)
- Recognizing the **status bar** at the bottom of the window (branch name, sync icon, errors)

### Required VS Code extensions

Install from the Extensions panel (`Ctrl+Shift+X`):

- [ ] **GitHub Pull Requests** — search "GitHub Pull Requests" → install the one by GitHub
- [ ] **GitHub Copilot** — search "GitHub Copilot" → install (requires a Copilot license)
- [ ] **GitHub Copilot Chat** — search "GitHub Copilot Chat" → install

### Required MCP servers

MCP (Model Context Protocol) servers give GitHub Copilot the ability to search official documentation and interact with GitHub from within VS Code.

#### Microsoft Docs MCP server

This gives Copilot access to search and retrieve official Microsoft Learn documentation.

- [ ] Open VS Code **Settings** (`Ctrl+,`)
- [ ] Search for `mcp` in the settings search bar
- [ ] Find **MCP Servers** configuration (or open your `settings.json` directly)
- [ ] Add the Microsoft Docs MCP server: https://learn.microsoft.com/api/mcp
- [ ] Verify it works: open Copilot Chat (`Ctrl+Shift+I`) and ask: *"Search Microsoft docs for Microsoft Writing Style Guide"* — you should get results from `learn.microsoft.com`

**What this gives you:**
- Search Microsoft Learn documentation for quick answers
- Fetch full content of a specific documentation page
- Find code examples from official Microsoft docs

#### GitHub MCP server

This gives Copilot the ability to read issues, PRs, and repository content directly from GitHub.

- [ ] In VS Code Settings, add the GitHub MCP server: https://api.githubcopilot.com/mcp/
- [ ] Verify it works: open Copilot Chat and ask: *"List open issues in [owner/repo-name]"* (using the actual repo) — you should see issue results

> **Note**: You might need to start the server from the extensions pane if the results don't match as you expect.

### Clone the repository

You work directly on the assigned repository — no personal fork. All repositories are under the `MicrosoftLearning` organization on GitHub. The content developer will provide the specific repository URL.

- [ ] Open VS Code
- [ ] Press `Ctrl+Shift+P` to open the **Command Palette**
- [ ] Type `Git: Clone` and select it
- [ ] Paste the repository URL provided by the content developer
- [ ] Choose a folder on your computer to store the repository (such as `C:\Repos\`)
- [ ] When VS Code asks "Would you like to open the cloned repository?", select **Open**

After cloning, the remote named `origin` points directly to the repository. All branches you create and push will be on this repository.

> **Note**: Repeat this clone step for each repository you are assigned to test. Each repo gets its own folder.

---

## Required training

Complete the following training **in order**. Each section builds on the previous one and maps directly to skills you will use in the workflow.

### 1. GitHub Skills — First day and first week

`https://learn.github.com/skills`

These are hands-on, interactive courses. Complete them in a browser — they walk you through real GitHub repositories.

- [ ] Complete the **First day on GitHub** courses:
    - Introduction to GitHub
    - Communicate using Markdown
    - GitHub Pages
- [ ] Complete the **First week on GitHub** courses:
    - Introduction to Git
    - Review pull requests
    - Resolve merge conflicts
    - Code with Codespaces
    - Introduction to Repository Management

> **Note**: Some content in these courses may be outdated or show slightly different UI than what you see today. The content developer will discuss any differences with you during onboarding.

### 2. GitHub Foundations (Microsoft Learn)

These two learning paths provide the foundation for everything in the workflow. Complete both parts.

**Part 1** — `https://learn.microsoft.com/training/paths/github-foundations/`

- [ ] Complete all 8 modules (approximately 5 hours 50 minutes)
- Covers: Introduction to Git, Introduction to GitHub, GitHub Products, Code Scanning, Introduction to Copilot, Codespaces, GitHub Projects, Communicating with Markdown

**Part 2** — `https://learn.microsoft.com/training/paths/github-foundations-2/`

- [ ] Complete all 8 modules (approximately 5 hours)
- Covers: Open Source on GitHub, InnerSource, Secure Repositories, GitHub Administration, Authentication, Pull Requests, Search and Organize, Copilot with Python

### 3. GitHub Copilot

On the same GitHub Skills page (`https://learn.github.com/skills`), work through the **Take flight with GitHub Copilot** section:

- [ ] Getting Started with GitHub Copilot
- [ ] Customize your GitHub Copilot Experience
- [ ] GitHub Copilot Code Review

Copilot assists your work but does not replace understanding the content. You need to know how to use it effectively and recognize when its suggestions are wrong.

---

## Key concepts you must understand

After completing the training above, you should be able to explain each of these concepts. If any are unclear, ask the content developer before starting work.

### One repository — no fork

You work directly on the assigned repository. There is no personal fork.

- **`origin`** = the repository you cloned — every branch you create lives here
- When Copilot creates a branch for an issue, it also lives here
- Pull requests go from a **feature branch on this repo** to `main` on this same repo

**Why no fork?** Forks add complexity — syncing forks, confusion about which repo to push to, and extra steps when working with Copilot-created branches. Since you have contributor access, you push directly to the shared repository.

### Branches — what they are

A **branch** is a separate line of work. Think of it like a sticky note on a specific page of a book — it tracks only the changes you intend to make.

| Branch | Purpose | Rule |
|---|---|---|
| `main` | The official, current state of the content | **NEVER make edits directly on `main`**. |
| Feature branch (such as `fix/lab01-step5-typo`) | Your working area for a specific set of fixes | Always create from an **up-to-date** `main`. |

**Critical rule:** You should only ever have **one active feature branch** at a time unless you are certain the branches modify completely different files.

### Why syncing matters

The `main` branch changes when other people's PRs are merged. If you start a branch from an **old** copy of `main`, your changes may conflict with changes that were already merged. **Always pull the latest `main` before creating a branch and before pushing.**

### The GitHub flow

The workflow you will follow every day is the GitHub Flow:

```
1. Sync main locally
2. Create a feature branch
3. Publish the branch to the remote
4. Make changes and commit frequently with meaningful messages
5. Test the entire lab end-to-end
6. Push and open a pull request
7. Wait for the content developer to review and merge
8. Switch back to main and pull the latest
```

You do not merge PRs — the content developer does that after reviewing your work.

This is covered in detail in the **Lab Tester Workflow**.

### Markdown

Lab files are written in Markdown (`.md` files). You must be comfortable with:
- Headings (`#`, `##`, `###`)
- Bold (`**text**`) and italic (`_text_`) or (`*text*`)
- Numbered lists (using `1.` for every item)
- Code blocks (fenced with triple backticks)
- Links and images
- Blockquote notes (`> **Note**: text`)

See the **Reference Guide** for detailed syntax and indentation rules.

### Pull requests

A pull request (PR) is how your changes get reviewed and merged into `main`. You must be comfortable with:
- Creating a PR with a descriptive title and body
- Referencing issue numbers (`Fixes #42`)
- Including test results in the PR description
- Understanding that one branch = one PR

### Copilot is a tool, not a crutch

You should be able to complete the workflow without Copilot. Copilot accelerates your work — it helps you search docs, draft commit messages, and validate formatting — but it does not replace knowing the process. Learn the manual steps first; then use Copilot to work faster.

---

## Lab delivery models

Labs are delivered in two ways. You need to understand both because they affect how you test.

| Model | Description | Who uses it |
|---|---|---|
| **Hosted VM (Skillable)** | A pre-configured virtual machine provided through Skillable. The content developer gives you access during onboarding. | Instructor-led training (ILT) learners and lab testers |
| **Bring your own subscription (BYOS)** | The learner uses their own Azure or Microsoft 365 subscription and follows the lab on their own machine. Setup instructions in the repo (typically in `Allfiles/Labs/00-Setup/` or a setup section at the start of the lab) guide the learner through provisioning. | Self-study learners |

**Why this matters for testing:**
- In the **hosted VM**, clipboard paste may not work — that is why code snippet text files exist in `Allfiles/`.
- In the **BYOS model**, learners start from scratch with no pre-provisioned resources. The setup instructions must be complete and accurate. If a repo has setup instructions, verify they work.
- Unless the content developer tells you otherwise, **test in the Skillable VM**. If you are also asked to verify the BYOS experience, the content developer will tell you explicitly.

---

## Exercise modularity

Exercises should be **independent** — a learner should be able to complete any exercise without depending on work done in a previous exercise. This matters because learners in the BYOS model may skip exercises, and hosted lab platforms may present exercises individually.

### What to check

- Does the exercise assume a resource (table, workspace, file) that was created in an earlier exercise?
- Does the exercise reference data or results from a previous step that the learner would not have if they started here?
- Is there a setup section that all exercises depend on? If so, that is acceptable — the setup is the shared baseline.

### What to do when you find a dependency

- If the exercise depends on a resource from a previous exercise, it needs its own setup step to create that resource — or the instructions need to tell the learner to complete the setup exercise first.
- Note the dependency in your PR description so the content developer can decide whether to restructure or accept it.
- **Some legacy labs have exercise dependencies that have not been refactored yet.** If you find one, flag it — do not silently ignore it, but do not block your PR on it either. Document it as a separate issue if the fix is beyond the scope of your current work.

---

## Understanding repository structure

Every repository in the MicrosoftLearning organization follows a similar folder structure. Before you start editing, you need to know where things live.

### Typical structure

```
repository-root/
├── Allfiles/
│   └── Labs/
│       ├── 01/                           ← supporting assets for Lab 01
│       └── ...                           ← not every lab has a folder
├── Instructions/
│   └── Labs/
│       ├── 01-lab-instructions.md               ← lab instruction files (what you edit)
│       └── Images/                       ← screenshots referenced by lab files
├── .github/                              ← GitHub configuration (do not edit)
├── README.md                             ← repo landing page
└── _build.yml / _config.yml              ← build configuration (do not edit)
```

### Key folders

| Folder | Contains | When you touch it |
|---|---|---|
| `Allfiles/Labs/<number>/` | Supporting assets learners need during the exercise — data files (CSV, JSON), code snippet text files, notebooks, starter files, solution files, zip archives | Only when the lab instructions reference these files **and** something in the asset needs to change (wrong data, outdated code, broken notebook). If your edits don't affect these files, leave them alone. |
| `Instructions/Labs/` | The markdown files learners follow — one `.md` file per lab exercise | Every task — this is where lab content lives |
| `Instructions/Labs/Images/` | Screenshots used in lab files | When adding, replacing, or deleting images |
| `.github/` | Workflows, issue templates | Do not edit unless asked |

### About `Allfiles/Labs/` subfolders

- Each subfolder is numbered to correspond to a lab (for example, `Allfiles/Labs/01/` relates to `Instructions/Labs/01-lakehouse.md`)
- **Not every lab has a subfolder** — many labs have no supporting assets and therefore have no folder here
- Common asset types you may find:
    - **Code snippet text files** (such as `01-Snippets.txt`) — these exist so learners on a hosted VM, where clipboard paste may not work, can open the file and copy code from there
    - **Data files** (CSV, JSON, or zipped archives) — sample data the learner uploads or imports during the exercise
    - **Notebooks** (`.ipynb`) — Jupyter notebooks the learner runs in the lab environment
    - **Starter and solution files** (such as `.pbix` files) — starter files the learner opens at the start, and solution files that show the completed result

### How to find your way around a new repo

1. Open the repo in VS Code after cloning
1. Expand the **Explorer** panel (`Ctrl+Shift+E`) to see the folder tree
1. Look at the `Instructions/Labs/` folder — each `.md` file is one lab exercise
1. Open 2–3 lab files to see how they are structured (YAML front matter, headings, steps)
1. Check the `Images/` folder to see the naming convention
1. Check the `Allfiles/Labs/` folder to see which labs have supporting assets

> **Tip**: Ask Copilot: *"Describe the folder structure of this repository and where the lab instruction files are located."*

> **Note**: Not every repo follows this structure exactly. Some repos have variations. Always explore the repo first and match what you find.

---

## Managing multiple repositories

You support multiple content developers across multiple lab repositories. Each repository is a separate clone on your machine.

### How to stay organized

- Clone each repo into the same parent folder (such as `C:\Repos\`). Each repo gets its own subfolder.
- Open **one repo at a time** in VS Code for simplicity.
- **Each repo has its own `main` branch, its own issues, and its own content developer.** The content developer will tell you which repo to work in and who reviews your PRs.
- Before starting work in any repo, always sync `main` for that repo — branches can go stale quickly when multiple people contribute.

### Prioritizing across repos

The content developer assigns work to you. If multiple content developers assign work at the same time, ask them to agree on priority — or escalate to your manager. As a general rule:

1. **Urgent fixes** (broken labs) take priority regardless of which repo
1. Then **needed fixes** by due date
1. Then **enhancements**

---

## Issue triage — how to evaluate work

When you receive an issue or are asked to review a lab, you need to evaluate what kind of work is required.

### Issue categories

| Category | Description | What You Do |
|---|---|---|
| **Urgent Fix** | Lab is broken — a step errors, a page doesn't load, users can't complete the exercise | Fix immediately. This is top priority. |
| **Needed Fix** | Confusing step, outdated screenshot, typo, numbering wrong | Group with other fixes for the same lab. Fix in one PR. |
| **Enhancement** | The lab works, but something could be improved — clearer wording, a better example, a missing tip | Propose the change. Create a branch, make the edit, and open a PR. Note in the PR description that this is an enhancement, not a bug fix. If you are unsure whether the change is appropriate, discuss with the content developer before starting. |
| **Not Actionable** | Subjective complaint, or a complaint about the product itself rather than the lab content (for example, "the product is slow") | Respond politely. Close if not actionable. |
| **Duplicate** | Same problem already reported in another issue | Comment linking to existing issue, then close. |

### Grouping issues

Do not create one PR per issue. Group related issues:

- Multiple issues affecting the **same lab file** = one branch, one PR
- Write down which issues you will address — you reference them in your PR

**Good:** Issues #42, #47, #51 (all in Lab 01) → one branch `fix/lab01-issues-42-47-51` → one PR

**Bad:** Issue #42 → PR #60, Issue #47 → PR #61, Issue #51 → PR #62 → all edit the same file → merge conflicts

### Researching before you fix

- Open the lab from the GitHub Pages site and try to reproduce the issue
- Read the lab markdown file in the repo
- If the issue involves code, **run the code yourself** in the relevant service, such as Microsoft Fabric or the Azure portal
- Use Copilot Chat to search Microsoft docs: *"Search Microsoft docs for [feature name]"*
- Check if the issue is caused by a deprecated feature or UI change — search the product's release notes or documentation

---

## Self-assessment

Before moving to the workflow, confirm you can answer **yes** to all of these:

- [ ] I can explain what a branch is and why we use them
- [ ] I can explain what `main` is and why I should never edit it directly
- [ ] I know what `origin` means
- [ ] I understand the GitHub Flow (branch → commit → push → PR → merge)
- [ ] I can write basic Markdown (headings, bold, lists, code blocks, links)
- [ ] I know what a pull request is and how to create one
- [ ] I understand why syncing `main` before creating a branch prevents merge conflicts
- [ ] I can categorize an issue (urgent fix, needed fix, enhancement, not actionable, duplicate)
- [ ] I understand why related issues should be grouped into one PR
- [ ] I have VS Code, Git, and the required extensions installed
- [ ] I am comfortable navigating VS Code (Explorer, Source Control, Command Palette, status bar)
- [ ] I have cloned at least one repository and can open it in VS Code
- [ ] I can identify the folder structure of a MicrosoftLearning repo (Instructions, Labs, Images, Allfiles)
- [ ] I know where supporting assets live (`Allfiles/Labs/`) and when to modify them
- [ ] I understand the two lab delivery models (hosted VM and bring your own subscription)
- [ ] I know what exercise modularity means and how to check for dependencies between exercises
- [ ] I can complete the full workflow (sync → branch → edit → commit → test → PR) 

**If you answered "no" to any of the above, revisit the relevant training before proceeding.**

---

## Reference links

| Resource | URL |
|---|---|
| Visual Studio Code YouTube Channel | `https://www.youtube.com/@code` |
| Personalize VS Code | `https://code.visualstudio.com/docs/getstarted/personalize-vscode` |
| Introduction to Visual Studio Code (AI Skills Navigator) | `https://aiskillsnavigator.microsoft.com/explore/search/module-5306b2f480ff96d4e84ac71ede4c7287e1683c09c26bec36f145ba8fad2ec4c1` |
| GitHub Foundations Part 1 (MS Learn) | `https://learn.microsoft.com/training/paths/github-foundations/` |
| GitHub Foundations Part 2 (MS Learn) | `https://learn.microsoft.com/training/paths/github-foundations-2/` |
| Introduction to GitHub (MS Learn) | `https://learn.microsoft.com/training/modules/introduction-to-github/` |
| GitHub Skills — Interactive Courses | `https://learn.github.com/skills` |
| Prompt Engineering with Copilot (AI Skills Navigator) | `https://aiskillsnavigator.microsoft.com/explore/search/module-0f400bf1724d139cdb1f62dba079ad59ed80cc01c6c1dbbd29d5180b867c7879` |
| Write Effective Prompts (AI Skills Navigator) | `https://aiskillsnavigator.microsoft.com/explore/search/module-9cfab2f6a2a95c2f4a59c96f248545c56a3499a4264e14a071e4399d8954167e` |
| Git Cheat Sheet (GitHub Training Kit) | `https://training.github.com/` |
| Microsoft Writing Style Guide | `https://learn.microsoft.com/style-guide/welcome/` |
| MS Learn Style Quick Start | `https://learn.microsoft.com/contribute/content/style-quick-start` |
| Writing Step-by-Step Instructions | `https://learn.microsoft.com/style-guide/procedures-instructions/writing-step-by-step-instructions` |
| MCT User Guide for GitHub | `https://microsoftlearning.github.io/MCT-User-Guide/` |

---

> **Next step:** Open the **Lab Tester Workflow** and work through your first lab.
