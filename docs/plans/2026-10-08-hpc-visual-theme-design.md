# Design Document: Visual Theme Harmonization with HPC Sister Site

**Date:** 2026-10-08  
**Status:** Approved  
**Author:** GlasgowTRE Team  

---

## 1. Executive Summary

This document specifies the design for aligning the visual theme, assets, and typography of the Glasgow TRE Handbook (`glasgowtre.github.io`) with its University of Glasgow sister site, [HPC](https://hpc.gla.ac.uk/). 

By adopting the digital experience styling from the HPC site, GlasgowTRE achieves brand consistency across University research computing services, eliminates legacy CSS workarounds for logo rendering, and introduces polished light/dark theme headers, custom interactive button styles, and official typography (`Noto Sans` / `Noto Sans Mono`).

---

## 2. Upstream HPC Visual Theme Analysis

Inspection of `https://hpc.gla.ac.uk/` reveals the following core design elements:

1. **Header Colors & Theme Palette**:
   - **Light Mode Header**: `#011451` (Official University of Glasgow Navy Blue).
   - **Dark Mode Header**: `#344374` (Muted Slate Navy harmonized with Material dark slate surfaces).
   - **Primary / Accent Tokens**: Indigo palette base with targeted component overrides.
2. **Branding Assets**:
   - **Header Vector Logo** (`assets/logo-white.svg`): Tightly cropped viewBox (`39.3 39.16 156.39 48.39`) featuring the white crest and "University of Glasgow" logotype with authentic light blue (`#99d9f7`) and green (`#029048`) crest accents.
   - **Favicon** (`assets/favicon.png`): 201×201 high-resolution UoG crest on a transparent background.
3. **Typography**:
   - Text font: `Noto Sans` (300, 400, 700).
   - Code font: `Noto Sans Mono` (400, 700).
4. **Custom Component Styling (`stylesheets/digital_experience_template.css`)**:
   - Header logo height constrained to `2rem` with auto width (max `300px`).
   - Title offset (`margin-left: 1rem`).
   - Navigation active links highlighted with `font-weight: 700`.
   - Distinct button styling: `#011451` borders on light scheme; white borders on dark slate scheme with inverted hover states.

---

## 3. Architecture & Asset Specifications

### 3.1 Assets
- **Logo**:
  - Saved to `docs/images/uog_logos/logo-white.svg`.
  - Extracted from `https://hpc.gla.ac.uk/assets/logo-white.svg`.
  - Used in `mkdocs.yml` under `theme.logo`.
- **Favicon**:
  - Saved to `docs/images/uog_logos/favicon.png`.
  - Extracted from `https://hpc.gla.ac.uk/assets/favicon.png`.
  - Used in `mkdocs.yml` under `theme.favicon`.

### 3.2 Typography
Configured in `mkdocs.yml`:
```yaml
theme:
  font:
    text: Noto Sans
    code: Noto Sans Mono
```

### 3.3 CSS Rules (`docs/stylesheets/palette.css`)
Refactor `palette.css` to integrate the HPC digital experience template while retaining `--gla-*` brand color tokens:

1. **Header Overrides**:
   ```css
   [data-md-color-scheme="default"] .md-header {
     background-color: #011451;
   }

   [data-md-color-scheme="slate"] .md-header {
     background-color: #344374;
   }
   ```
2. **Logo & Header Sizing**:
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
   *Note: Remove the previous `background-image` light mode replacement and `filter: brightness(0) invert(1)` hack.*
3. **Navigation Links**:
   ```css
   .md-nav__item .md-nav__link--active {
     font-weight: 700;
   }
   ```
4. **Button Styling**:
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

---

## 4. Implementation Steps

1. Fetch and store `logo-white.svg` and `favicon.png` from `https://hpc.gla.ac.uk/` into `docs/images/uog_logos/`.
2. Update `mkdocs.yml` with the new logo, favicon, and `Noto Sans` font configurations.
3. Update `docs/stylesheets/palette.css` with HPC header, logo, nav, and button styles, cleaning up redundant background-image rules.
4. Verify asset integrity and layout consistency.
