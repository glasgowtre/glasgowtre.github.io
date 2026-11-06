---
title: R Runtime
---

# R Runtime & Package Management

## Overview

#### Service Offering

Glasgow TRE provides the **R statistical computing runtime** for statistical modeling, epidemiological research, bioinformatics, and reproducible data analysis. R is installed machine-wide with binaries integrated into the system path, enabling interactive analysis, batch scripting, and project library isolation via `renv`.

#### Version

- **R 4.6.1** (64-bit release for Windows)
- Primary binaries pre-configured in system `PATH`: `C:\Program Files\R\R-4.6.1\bin\x64\R.exe` and `Rscript.exe`.
- All operations run in user space without requiring local administrative privileges.

#### Offline & Air-Gapped Operation

Workstations operate in a strictly air-gapped network enclave. Public CRAN access is disabled. R package managers and library utilities are configured to resolve packages from internal mirrors or approved local binary archives.

---

## Getting Started

### 1. Interactive Launch

Open **PowerShell** or **Windows Terminal** and verify the R interpreter:

```powershell
# Check interpreter version
R.exe --version

# Check R scripting front-end version
Rscript.exe --version
```

To launch an interactive R console session:

```powershell
R.exe --no-save
```

To exit the interactive session, type `q()` and press Enter.

---

### 2. Executing R Scripts Non-Interactively

Run analysis scripts or inline expressions from the command line using `Rscript`:

```powershell
# Run a script from your analytical project drive
Rscript V:\my-project\analysis.R

# Execute an inline R expression
Rscript -e "cat('Hello from R in Glasgow TRE\n')"
```

---

## How-To Guides

### Managing Isolated Project Libraries with `renv`

To ensure reproducible analysis and avoid library conflicts between projects, use `renv` for project dependency management.

#### 1. Initialize `renv` in Your Project Directory

Navigate to your analytical project directory on the `V:` drive and start R:

```r
# Navigate to project directory and initialize renv
setwd("V:/my-project")
install.packages("renv")
renv::init()
```

This creates a project-local library and an `renv.lock` file that records the exact package versions used.

#### 2. Install Packages from Internal Repositories

Because public internet CRAN endpoints are unreachable, configure package installations to target the internal mirror or install approved local binaries:

```r
# Set repository to internal TRE package mirror (when mirror configured)
options(repos = c(CRAN = "https://storage.dc1.glasgowtre.ac.uk:9021/public/software/r/cran"))

# Install from an approved local zip binary package
install.packages("C:/path/to/approved_package.zip", repos = NULL, type = "win.binary")
```

#### 3. Snapshot Your Project Dependencies

Before sharing analytical code, preparing publications, or submitting results for egress review, snapshot your environment:

```r
renv::snapshot()
```

The resulting `renv.lock` file captures the exact package state for audit and reproduction.

---

### Environment Verification

Confirm that your R environment is operational:

```powershell
Rscript -e "cat('Hello World from R', R.version.string, '\n')"
```

---

## Storage Best Practices

| Storage Location | Recommended Usage |
| :--- | :--- |
| **`V:\<project-name>\`** | Analysis scripts (`.R`), R Markdown files (`.Rmd`), datasets, and `renv.lock` project configurations. Backed up network storage accessible to project members. |
| **`%LOCALAPPDATA%`** | Local package caches and build artifacts. Fast SSD storage avoiding SMB latency. |
| **`%APPDATA%`** | R user configuration files (`.Rprofile`, `.Renviron`). Roams with your profile across workstations. |

!!! caution "Do Not Save Analysis Data to Local C: Drive"

    Always store analytical scripts, outputs, and lockfiles on the assigned project drive (`V:\`). Local scratch drives are not backed up.

---

## Requesting Additional R Packages

If your project requires CRAN or Bioconductor packages that are not present in the environment:

1. Submit a package request ticket through your **Glasgow TRE Representative** or email [tre@glasgow.com](mailto:tre@glasgow.com?subject=R%20Package%20Request).
2. Include the package name, requested version, dependencies, and analytical rationale.
3. Once vetted for security and license compliance, packages are mirrored internally for all project members.

---

## Related Documentation

- [Python Core](python-core.md) — Python runtime and analytical libraries.
- [JupyterLab StandAlone](jupyter.md) — Interactive notebook environments and custom kernels.
- [LibreOffice](libreoffice.md) — Quick inspection of tabular CSV/Excel files.
