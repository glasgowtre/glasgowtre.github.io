# HPC Visual Theme Harmonization Implementation Plan

> **For Antigravity:** REQUIRED WORKFLOW: Use `.agent/workflows/execute-plan.md` to execute this plan in single-flow mode.

**Goal:** Harmonize the Glasgow TRE Handbook website visual theme, branding assets, typography, and button styling with its University of Glasgow sister site, HPC (`https://hpc.gla.ac.uk/`).

**Architecture:** Download and integrate HPC's optimized white vector logo and favicon, configure `mkdocs.yml` with official `Noto Sans` typography and asset paths, and refactor `docs/stylesheets/palette.css` to adopt HPC's `#011451` (light) and `#344374` (slate dark) header colors, navigation bolding, and button states while retiring legacy background-image overrides.

**Tech Stack:** MkDocs Material 9.x, CSS3 Custom Properties, SVG, PNG.

---

### Task 1: Extract and store HPC branding assets

**Files:**
- Create/Overwrite: `docs/images/uog_logos/logo-white.svg`
- Create/Overwrite: `docs/images/uog_logos/favicon.png`

**Step 1: Download `logo-white.svg` and `favicon.png` from `https://hpc.gla.ac.uk/`**

Run:
```bash
curl -fsSL https://hpc.gla.ac.uk/assets/logo-white.svg -o docs/images/uog_logos/logo-white.svg
curl -fsSL https://hpc.gla.ac.uk/assets/favicon.png -o docs/images/uog_logos/favicon.png
```

**Step 2: Verify downloaded assets**

Run:
```bash
grep -q 'viewBox="39.3 39.16 156.39 48.39"' docs/images/uog_logos/logo-white.svg && file docs/images/uog_logos/favicon.png
```
Expected: `viewBox` match and PNG image data output.

**Step 3: Commit**

```bash
git add docs/images/uog_logos/logo-white.svg docs/images/uog_logos/favicon.png
git commit -m "assets: add optimized UoG white vector logo and favicon from HPC sister site"
```

---

### Task 2: Configure MkDocs theme, typography, and assets in `mkdocs.yml`

**Files:**
- Modify: `mkdocs.yml:6-21`

**Step 1: Update `mkdocs.yml` theme configuration**

Update `theme.logo` to `images/uog_logos/logo-white.svg`, `theme.favicon` to `images/uog_logos/favicon.png`, and add `theme.font`:
```yaml
theme:
  name: material
  logo: images/uog_logos/logo-white.svg
  favicon: images/uog_logos/favicon.png
  font:
    text: Noto Sans
    code: Noto Sans Mono
  features:
    - navigation.indexes
    - navigation.instant
    - navigation.instant.progress
    - navigation.path
    - navigation.expand
    - navigation.top
    - navigation.tracking
    - search.highlight
    - search.share
    - content.tooltips
```

**Step 2: Verify `mkdocs.yml` syntax**

Run:
```bash
python3 -c "import yaml; yaml.safe_load(open('mkdocs.yml'))"
```
Expected: Exit code 0 with valid YAML structure.

**Step 3: Commit**

```bash
git add mkdocs.yml
git commit -m "chore(theme): configure Noto Sans fonts and HPC logo/favicon in mkdocs.yml"
```

---

### Task 3: Refactor `docs/stylesheets/palette.css` for HPC visual theme

**Files:**
- Modify: `docs/stylesheets/palette.css`

**Step 1: Update header backgrounds, logo sizing, active navigation, and button styles**

Replace the legacy logo background-image swap and add HPC styling:
1. Header background colors:
   ```css
   /* Light mode: University of Glasgow Navy Blue */
   [data-md-color-scheme="default"] .md-header {
     background-color: #011451;
   }

   /* Dark mode: Slate Navy */
   [data-md-color-scheme="slate"] .md-header {
     background-color: #344374;
   }
   ```
2. Header logo and title dimensions:
   ```css
   .md-header__button.md-logo img {
     height: 2rem;
     width: auto;
     max-width: 300px;
   }

   .md-header__title {
     margin-left: 1rem;
   }
   ```
3. Active navigation item bolding:
   ```css
   .md-nav__item .md-nav__link--active {
     font-weight: 700;
   }
   ```
4. Button colors and hover states:
   ```css
   [data-md-color-scheme="default"] .md-button {
     color: #011451;
     border-color: #011451;
   }
   [data-md-color-scheme="default"] .md-button:hover {
     background-color: #011451;
     color: #ffffff;
     border-color: #011451;
   }

   [data-md-color-scheme="slate"] .md-button {
     color: #ffffff;
     border-color: #ffffff;
   }
   [data-md-color-scheme="slate"] .md-button:hover {
     background-color: #ffffff;
     color: #011451;
     border-color: #ffffff;
   }
   ```

**Step 2: Verify CSS rules**

Check that legacy opacity/filter hacks are removed and new selectors exist:
```bash
grep -q "#344374" docs/stylesheets/palette.css && ! grep -q "brightness(0) invert(1)" docs/stylesheets/palette.css
```
Expected: Exit code 0.

**Step 3: Commit**

```bash
git add docs/stylesheets/palette.css
git commit -m "style(theme): adopt HPC header colors, logo sizing, and button styling"
```

---

### Task 4: Complete theme verification and tracker update

**Files:**
- Modify: `docs/plans/task.md`

**Step 1: Verify all modified files and git status**

Run:
```bash
git status
git diff origin/main
```
Expected: Clean status across `mkdocs.yml`, `docs/stylesheets/palette.css`, and logo assets.

**Step 2: Update task tracking document**

Mark all tasks as Completed in `docs/plans/task.md`.

**Step 3: Commit**

```bash
git add docs/plans/task.md docs/plans/2026-10-08-hpc-visual-theme.md
git commit -m "docs(plans): mark HPC visual theme implementation tasks complete"
```
