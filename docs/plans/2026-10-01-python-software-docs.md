# Python Software Documentation Implementation Plan

> **For Antigravity:** REQUIRED WORKFLOW: Use `.agent/workflows/execute-plan.md` to execute this plan in single-flow mode.

**Goal:** Add a Software & Python documentation section to the Glasgow TRE Handbook website detailing Python runtime management with Astral `uv` and an A-Z catalog of available PyPI packages.

**Architecture:** Update site navigation in `docs/.pages` to introduce `software`, configure section metadata in `docs/software/.pages`, and generate `docs/software/python.md` containing runtime management architecture, researcher workflows, and consolidated A-Z package tables sourced from `repo-config/ansible/files/pypi_packages.csv`.

**Tech Stack:** MkDocs Material, `mkdocs-awesome-pages-plugin`, Python 3, Markdown.

---

### Task 1: Navigation Structure Setup

**Files:**
- Modify: `docs/.pages:1-6`
- Create: `docs/software/.pages`

**Step 1: Update root navigation in `docs/.pages`**
Add `software` to the nav list between `guildes` and `faq`.

**Step 2: Create section navigation in `docs/software/.pages`**
Create `docs/software/.pages` defining title "Software" and nav list referencing `python.md`.

**Step 3: Verify navigation configuration files**
Verify YAML syntax and file existence for both `.pages` files.

**Step 4: Commit**
```bash
git add docs/.pages docs/software/.pages
git commit -m "docs(nav): add software section to site navigation"
```

---

### Task 2: Python Documentation & Package Directory Implementation

**Files:**
- Create: `docs/software/python.md`
- Source Reference: `/mnt/c/Users/nv15r/src/glasgowtre/repo-config/ansible/files/pypi_packages.csv`

**Step 1: Generate the A-Z package catalog data**
Process `/mnt/c/Users/nv15r/src/glasgowtre/repo-config/ansible/files/pypi_packages.csv` using Python to normalize library names, consolidate versions, and group them into letter sections with markdown tables.

**Step 2: Compose `docs/software/python.md`**
Assemble the complete document containing:
- Title and Overview
- Python Runtime Management:
  - Astral `uv` toolchain deployed system-wide (`C:\Program Files\uv`).
  - Standalone CPython runtimes sourced from `astral-sh/python-build-standalone`.
  - Versions available: all releases between `3.12.0` and `3.14.13` (including betas and release candidates) for Windows (`x86_64-pc-windows-msvc`) and Linux (`x86_64-unknown-linux-gnu`).
  - Dell PowerScale S3 / internal HTTP mirror endpoints with `only-managed` preference.
  - Air-gapped PyPI package mirror (`repo.hlz.glasgowtre.ac.uk`).
  - System-wide `pip.ini` and `pip.conf` configuration.
- Practical Researcher Workflows:
  - Listing & installing Python versions (`uv python list`, `uv python install 3.12.13`).
  - Initializing projects and virtual environments (`uv init`, `uv venv --python 3.12`).
  - Installing dependencies (`uv add`, `uv pip install`, Jupyter `%pip install`).
  - Running scripts, JupyterLab, and ephemeral commands (`uv run`).
  - IDE integration in VS Code and PyCharm.
- A-Z Available Packages Catalog:
  - Alphabet quick-jump links (`[A](#a) | [B](#b) ...`).
  - Level-3 headings and Markdown tables for each letter (`### A`, `### B`, etc.).
  - Admonition callout box for requesting new libraries or version upgrades.

**Step 3: Write `docs/software/python.md`**
Write the assembled content to `docs/software/python.md`.

**Step 4: Verify generated markdown content and links**
Ensure all headings, anchor links, and table formatting are valid and render properly.

**Step 5: Commit**
```bash
git add docs/software/python.md
git commit -m "docs: add python runtime management guide and package catalog"
```

---

### Task 3: Quality Review and Verification

**Files:**
- Verify: `docs/.pages`
- Verify: `docs/software/.pages`
- Verify: `docs/software/python.md`

**Step 1: Check git status and diff**
Review all changes made across the repository.

**Step 2: Verify total package count against source CSV**
Confirm that all 301 canonical packages from `pypi_packages.csv` are accounted for in the generated document.

**Step 3: Update task tracker**
Update `docs/plans/task.md` to reflect completion of all tasks.

**Step 4: Commit task tracker**
```bash
git add docs/plans/task.md
git commit -m "docs: update task tracker for python documentation"
```
