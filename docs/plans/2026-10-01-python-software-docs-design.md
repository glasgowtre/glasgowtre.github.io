# Design Document: Python Runtime Management & Package Directory Documentation

**Date:** 2026-10-01  
**Status:** Approved  
**Author:** GlasgowTRE Team  

---

## 1. Executive Summary

This document establishes the architecture and content design for introducing the **Software** section into the Glasgow TRE Handbook website (`glasgowtre.github.io`). Specifically, it details the addition of a comprehensive **Python** documentation page (`docs/software/python.md`) that outlines how Python runtimes are managed within the secure, air-gapped environment using Astral `uv`, how standalone CPython executables are sourced and mirrored, practical researcher workflows, and a complete catalog of available PyPI packages grouped alphabetically from `A` to `Z`.

---

## 2. Information Architecture & Navigation

### 2.1 Navigation Updates
- **Top-Level Navigation (`docs/.pages`)**:
  Include `software` in the main handbook navigation between `guildes` and `faq`:
  ```yaml
  nav:
    - index.md
    - guildes
    - software
    - faq
  ```
- **Software Sub-navigation (`docs/software/.pages`)**:
  Establish the software category configuration:
  ```yaml
  title: Software
  nav:
    - python.md
  ```

### 2.2 Page Route
- File path: `docs/software/python.md`
- URL path: `/software/python/`
- Breadcrumb: `Home > Software > Python`

---

## 3. Python Runtime Management Specification

### 3.1 Toolchain & Architecture
- **Tool**: Astral `uv` deployed system-wide (`C:\Program Files\uv` on Windows analytics workstations).
- **Security & Privileges**: All Python environment management, runtime switching, and dependency installations take place in user space without requiring local administrator rights.
- **Python Binary Distribution**:
  - Python binaries are sourced upstream from [`astral-sh/python-build-standalone`](https://github.com/astral-sh/python-build-standalone).
  - Version coverage includes all releases from `3.12.0` to `3.14.13` (including beta and RC builds).
  - Supported platforms: Windows (`x86_64-pc-windows-msvc`) and Linux (`x86_64-unknown-linux-gnu`).
  - Binaries are mirrored internally to internal HTTP/PowerScale S3 object storage (`python-install-mirror`).
- **Enforcement**:
  - `C:\ProgramData\uv\uv.toml` sets `python-preference = "only-managed"` to ensure workstations strictly pull and run mirrored runtimes.
- **Package Repository (PyPI Mirror)**:
  - Glasgow TRE hosts an internal air-gapped Pulp mirror serving curated wheels and source distributions (`repo.hlz.glasgowtre.ac.uk`).
  - Pre-configured `C:\ProgramData\pip\pip.ini` (Windows) and `/etc/pip.conf` (Linux) allow standard `pip` and Jupyter `%pip` commands to resolve dependencies automatically.

### 3.2 Practical User Workflows
1. **Discovering & Installing Runtimes**:
   - `uv python list`
   - `uv python install 3.12.13` (multiple versions installable side-by-side)
2. **Project & Virtual Environment Creation**:
   - `uv init my_project`
   - `uv venv --python 3.12`
3. **Dependency Management**:
   - `uv add pandas polars jupyterlab` (pinned cleanly in `uv.lock`)
   - `uv pip install -r requirements.txt`
   - JupyterLab `%pip install <package>` support
4. **Execution**:
   - `uv run script.py`
   - `uv run jupyter lab`
   - Ephemeral testing: `uv run --python 3.12 --with pandas script.py`
5. **IDE Detection**: Automatic discovery by VS Code and PyCharm via `.venv`.

---

## 4. PyPI Package Directory Specification

### 4.1 Data Pipeline & Normalization
- Data source: `repo-config/ansible/files/pypi_packages.csv` (reflecting Snapshot Version 3 documented in `production_packages_report.md`).
- Library names are normalized according to PEP 503 conventions (lowercase, standardized dashes).
- When a library has multiple supported releases in the mirror (e.g., `numpy` versions `1.26.4` and `2.5.3`), releases are consolidated into a single entry with versions separated by commas.

### 4.2 Presentation & Navigation
- **Quick-Jump Alphabet Bar**: Anchor links (`[A](#a) | [B](#b) | ... | [Z](#z)`) placed at the top of the package section.
- **A-Z Headings**: Level-3 headings (`### A`, `### B`, etc.) for each letter with available packages.
- **Table Structure**:
  | Package | Available Version(s) |
  | :--- | :--- |
  | `package-name` | `version_1, version_2` |
- **Support & Request Box**: Admonition block detailing how researchers can request additional libraries or version updates via their TRE representative.
