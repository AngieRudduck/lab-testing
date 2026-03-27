# Lab content style and formatting reference

> **What this is:** The formatting rules and conventions for lab content in MicrosoftLearning repositories. Use as a reference while working, or attach to an agent chat as context so the agent follows the same standards.

---

## Table of contents

- Markdown rules
- Microsoft Writing Style Guide summary
- Working with images
- PR description template
- Using Copilot to help with your work

---

## Markdown rules

Lab files use Markdown (`.md`). Follow these conventions. When a repo's existing files differ from what is listed here, match the repo — open 2–3 other lab files in the same folder and use them as your reference.

> **Tip**: Ask Copilot: *"What formatting conventions does this repo use for notes, code blocks, and numbered steps? Show me examples from existing lab files."*

### YAML front matter

Every lab file must start with YAML front matter. Not all repos use every field — match the fields used in other lab files in the same repo.

```yaml
---
lab:
  title: Create a Microsoft Fabric Lakehouse
  module: Get started with lakehouses in Microsoft Fabric
  description: In this lab, you'll create a Microsoft Fabric lakehouse...
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Fabric
---
```

- **title**: Lab title — update if the lab title changes
- **module**: Corresponding Learn module title — don't modify unless asked
- **description**: Short summary of the lab objectives — update if the lab scope changes
- **duration**: Estimated time to complete — update if your testing shows the estimate is significantly off
- **level**: Difficulty level — don't modify unless asked
- **islab**: Tracking item — don't modify unless asked
- **primarytopics**: Topic tags — don't modify unless asked

### Lab story

Each lab should include a lab story that sets up the scenario and lists the learning objectives. Format may vary by repo — match the existing pattern.

### Headings

Use **sentence case** — capitalize only the first word and proper nouns. One H1 per file.

```markdown
# Lab Title (H1 — only ONE per file)

## Task Name (H2 — main sections)

### Sub-section (H3 — if needed)
```

### Numbered steps

Use `1.` for every step. Markdown auto-numbers them when rendering in the html page.

**CORRECT:**

```markdown
1. Do the first thing.
1. Do the second thing.
1. Do the third thing.
```

Renders as 1, 2, 3.

**WRONG — do NOT manually number:**

```markdown
1. Do the first thing.
2. Do the second thing.
3. Do the third thing.
```

> **Note:** Some older files use manual numbering. Convert to auto-numbering only if your edit requires reordering.

### Sub-steps

Indented with **4 spaces** (not a tab):

```markdown
1. In the Explorer pane, expand **Schemas** > **dbo** > **Tables**.
    1. Verify that the **DimProduct** table exists.
    1. Check that it contains three rows.
```

### Keeping content inside a numbered step

All content that belongs to a step — images, notes, code blocks, bullets — **must be indented 4 spaces**. If not indented, the auto-numbering breaks and the list restarts at 1.

**Images inside a step (4 spaces):**

```markdown
1. When your new workspace opens, it should be empty.

    ![Screenshot of an empty workspace.](./Images/new-workspace.png)
```

**Notes inside a step (4 spaces):**

```markdown
1. On the menu bar on the left, select **Create**.

    > **Note**: If the **Create** option is not pinned to the sidebar, select the ellipsis (**...**) first.
```

**Bullet sub-items inside a step (4 spaces):**

```markdown
1. View the new lakehouse, and note the pane on the left:
    - The **Tables** folder contains tables you can query using SQL.
    - The **Files** folder contains data files in OneLake storage.
```

**Code blocks inside a step — understanding the indentation:**

This is the trickiest formatting rule. Here is how it works:

- The **fence lines** (` ``` `) must be indented **4 spaces** so they stay inside the numbered list item
- The **code content** between the fences uses **3 spaces** of indentation
- This is the established pattern in MicrosoftLearning repos

Here is a visual breakdown showing what goes where (dots represent spaces):

```
1. Enter the following SQL query:

••••```sql           ← fence: 4 spaces (keeps it inside the list)
•••SELECT Item      ← code: 3 spaces
•••FROM sales;      ← code: 3 spaces
••••```              ← fence: 4 spaces
```

Here is the actual markdown:

````markdown
1. Enter the following SQL query:

    ```sql
   SELECT Item, SUM(Quantity * UnitPrice) AS Revenue
   FROM sales
   GROUP BY Item;
    ```
````

**How to check your work:** Open the file in VS Code and use the **minimap** or **ruler** to count spaces visually, or select the whitespace characters by enabling **View** → **Render Whitespace** in VS Code. If the code renders as a separate block disconnected from the step when you preview the file, the indentation is wrong.

> **Tip**: When in doubt, find a code block in an existing lab file in the same repo and count the spaces — then match exactly.

**What happens if you don't indent:**

```markdown
1. First step.

> **Note**: This note is at column 0.

1. This renders as "1" again — the list restarted!
```

The note at column 0 breaks the list. The second step renders as 1 instead of 2.

### Bold and italic

- **Bold** UI elements the user interacts with: `**Workspaces**`
- *Italicize* new terms on first use: `*data lakehouse*`

### Code

Inline: `` `SELECT * FROM dbo.DimProduct` ``

Blocks with language identifier:

````markdown
```sql
CREATE TABLE dbo.DimProduct
(
    ProductKey INTEGER NOT NULL,
    ProductName VARCHAR(50) NOT NULL
);
GO
```
````

Common identifiers: `sql`, `python`, `dax`, `json`, `kusto`, `powershell`, `csharp`. Use whatever matches the code.

### Notes, tips, and warnings

```markdown
> **Note**: You need a Microsoft Fabric trial to complete this exercise.

> **Tip**: If the table does not appear, select **Refresh** from the toolbar.

> **Important**: Do not delete the workspace until you have completed all tasks.
```

Do not use `[!NOTE]` or `[!TIP]` syntax (such as `> [!NOTE]`). That syntax is used on the Microsoft Learn platform (`learn.microsoft.com`), but lab exercises are rendered as GitHub Pages, which does not support it. On GitHub Pages, `[!NOTE]` renders as plain text instead of a styled callout. Use the blockquote format shown above instead.

**Match the convention already in use in the repo you are working in.**

> **Tip**: Tell Copilot to match the formatting and tone in the instruction file.

### Links

```markdown
Navigate to the [Azure portal](https://portal.azure.com) at `https://portal.azure.com`.
```

When a step includes a URL, hyperlink the name and also display the raw URL in backticks so the reader can use either.

---

## Microsoft Writing Style Guide summary

Full guide: `https://learn.microsoft.com/style-guide/welcome/`

You can also search from Copilot Chat: *"Search Microsoft docs for writing step-by-step instructions style guide"*

### Key principles

| Principle | Rule |
|---|---|
| **Use everyday words** | "select" not "elect to choose" |
| **Use active voice** | "Select **Create**" not "The **Create** button should be selected" |
| **Address the user as "you"** | "You will see..." not "The user will see..." |
| **Be concise** | One idea per sentence |
| **Sentence case for headings** | "Create a data warehouse" not "Create A Data Warehouse" |
| **Bold UI elements** | select **Workspaces** not select "Workspaces" |
| **Use "select" not "click"** | "Select" is device-agnostic |

### Common phrasing

| Do this | Not this |
|---|---|
| Select **Create** | Click on the **Create** button |
| In the left menu, select **Workspaces** | Navigate to the left side bar, and then click on the **Workspaces** icon |
| Sign in to the service | Log in to the service |
| The workspace opens | The workspace will get opened |
| If prompted, select **Yes** | If you are prompted with a question, you should select **Yes** |

---

## Working with images

### Where images live

Typically `Instructions/Labs/Images/`. Match the path used in existing lab files in the repo.

### Naming convention

- Lowercase, hyphens between words, descriptive (example: `new-workspace.png`)
- Some repos prefix with a lab number for lab-specific images (such as `01-new-workspace.png`)
- Match whatever naming convention the repo already uses

### Adding a new image

1. Screenshot and crop to the relevant area only
2. Save as `.png` in the repo's image folder (typically `Instructions/Labs/Images/`)
3. Reference in markdown:

```markdown
![Screenshot of a new workspace.](./Images/new-workspace.png)
```

Alt text is **required** for accessibility. Match the image path format used in the same file.

### Replacing an existing image

Save the new screenshot with the **same filename** in the images folder. The markdown reference does not change. Stage the image file in your commit.

### Deleting an image

Search the repo first (`Ctrl+Shift+F` → search for the filename). Only delete if it's referenced in one place. If referenced in multiple files, update all references.

---

## PR description template

Copy and fill in when creating a pull request:

```
Fixes #XX, #XX.

## Proposed changes
- [describe each change]
```

---

## Using Copilot to help with your work

> This section is for human reference. When providing this file as agent context, the agent can skip this section.

Open Copilot Chat with `Ctrl+Shift+I`. Switch between **Ask** (research) and **Agent** (edits) at the top of the panel.

| Mode | What it does | When to use |
|---|---|---|
| **Ask** | Answers questions. Does not change files. | Research, understanding code, checking docs |
| **Agent** | Reads files, runs commands, edits files. | Drafting fixes, find-and-replace, applying patterns |

You are responsible for every edit in your PR, even if Copilot wrote it. Always review.

### Research (Ask mode)

- *"What does this SQL query do?"* (with code selected)
- *"Search Microsoft docs for the PREDICT function in Fabric — is this still the current approach?"*
- *"Summarize issue #42 in this repository"*
- *"Should I use 'click' or 'select' according to the Microsoft Writing Style Guide?"*

### Editing (Agent mode)

- *"Convert the manually numbered steps to auto-numbered (all using 1.)"*
- *"Replace all instances of 'click' with 'select' in this file"*
- *"Write a commit message for the changes I've staged"*
- *"Write a PR description for my current branch"*

### Troubleshooting (Ask mode)

- *"This Python code throws a NameError on line 12. What's wrong?"*
- *"I accidentally committed to main. How do I undo this?"*
- *"Why is this numbered list restarting at 1 after the code block?"*

### Rules

1. **Be specific.** Include file names, step numbers, issue numbers.
2. **Verify everything.** Copilot can be confidently wrong.
3. **Don't blindly accept Agent edits.** Read every change.
4. **Copilot is not a substitute for testing.**

---

## Reference links

| Resource | URL |
|---|---|
| Microsoft Writing Style Guide | `https://learn.microsoft.com/style-guide/welcome/` |
| MS Learn Style Quick Start | `https://learn.microsoft.com/contribute/content/style-quick-start` |
| Writing Step-by-Step Instructions | `https://learn.microsoft.com/style-guide/procedures-instructions/writing-step-by-step-instructions` |
| Text Formatting Guidelines | `https://learn.microsoft.com/contribute/content/text-formatting-guidelines` |
| Microsoft Learn Contributor Guide | `https://learn.microsoft.com/contribute/` |
