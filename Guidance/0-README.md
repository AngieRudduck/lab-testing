# Lab Tester Documentation — How to Use These Files

> **Audience:** Anyone who works with labs in MicrosoftLearning repositories.

---

## The files

| File | Purpose | When to use |
|---|---|---|
| **Training Guide** | One-time onboarding. Setup, training, key concepts, issue triage, self-assessment. | Before starting any work. Complete once, then refer back as needed. |
| **Workflow** | Repeatable process for every task. Sync → branch → edit → commit → test → PR. GUI-only. | Every time you pick up new work. Follow it in order. |
| **Reference Guide** | Formatting rules, writing style, images, PR template, Copilot prompts. Use as a lookup or attach to an agent chat as context. | While working — when you need to check formatting or conventions. |
| **Advanced Scenarios** | Terminal workflow, useful Git commands, Copilot branches. | When you are comfortable with the GUI workflow and want to use the terminal, or when working with Copilot-created branches. |

---

## Reading order

```
1. Training Guide      — complete all setup and training (one time)
2. Workflow            — learn the repeatable process (use daily)
3. Reference Guide     — keep open while working (look up as needed)
4. Advanced Scenarios  — optional: terminal workflow, Copilot branches
```

---

## How these files connect

```
Training Guide
  ├── Defines terminology (lab = exercise)
  ├── Sets up the environment (software, extensions, MCP servers, clone)
  ├── Gets familiar with VS Code
  ├── Completes required training courses
  ├── Teaches key concepts (branches, GitHub Flow, markdown, PRs, Copilot)
  ├── Explains lab delivery models (hosted VM and bring your own subscription)
  ├── Explains exercise modularity (independence between exercises)
  ├── Explains repository structure (folders, files, navigation)
  ├── Covers managing multiple repositories
  ├── Teaches issue triage (how to evaluate and group work)
  └── Self-assessment → confirms readiness
        │
        ▼
Workflow (daily use)
  ├── Repeatable process (sync → branch → edit → commit → test → PR)
  ├── Testing guidance (environment selection, modularity checks)
  ├── Rules to follow
  └── Quick reference card
        │
        ├── Reference Guide (lookup while working)
        │     ├── Markdown syntax and indentation rules
        │     ├── Microsoft Writing Style Guide summary
        │     ├── Working with images
        │     ├── PR description template
        │     └── Copilot prompts and modes
        │
        └── Advanced Scenarios (when ready)
              ├── Terminal workflow (same steps, terminal commands)
              ├── Useful Git commands for troubleshooting
              └── Copilot branches (GUI and terminal)
```
