---
title: R
---

# R Runtime & Package Management

## Overview

#### Service Offering

Glasgow TRE provisions workstations with the **R statistical computing runtime** for researchers who require statistical modeling, data science, and analytical programming.

Provisioned Windows 11 workstations have **R 4.6.1** installed machine-wide with 64-bit binaries pre-configured in the system `PATH`. This enables interactive console analysis, batch scripting via `Rscript`, and execution through external analytical IDEs such as [JupyterLab StandAlone](jupyter.md).

#### Pre-Installed Analytical Libraries

To support immediate, offline data processing from the moment you log in, the provisioned R environment includes a pre-installed, pre-compiled suite of top-level libraries and their dependencies in the system library:

| Package | Version Category | Primary Analytical Purpose |
| :--- | :--- | :--- |
| **`renv`** | Environment Isolation | Reproducible project-local dependency management and lockfile tracking. |
| **`dplyr`** | Data Transformation | Grammar of data manipulation (filtering, mutating, grouping, summarizing). |
| **`ggplot2`** | Data Visualization | Declarative grammar of graphics for exploratory data analysis and figures. |
| **`tidyr`** | Data Reshaping | Tidying data structures (pivoting longer/wider, nesting, missing value handling). |
| **`data.table`** | High-Performance Ingestion | Fast, multi-threaded aggregation, grouping, and disk streaming via `fread()`. |
| **`readr`** | Tabular Ingestion | Fast parsing of rectangular text data (`.csv`, `.tsv`, `.txt`). |
| **`readxl`** | Spreadsheet Ingestion | Direct extraction of tabular data from legacy (`.xls`) and modern (`.xlsx`) Excel sheets. |
| **`haven`** | Statistical Data Ingestion | Importing cohorts saved in SAS (`.sas7bdat`), SPSS (`.sav`), or Stata (`.dta`) formats. |
| **`arrow`** | Columnar & Parquet Storage | High-throughput zero-copy reads, dataset partitioning, and Apache Parquet ingestion. |

#### Version & Configuration

- **R 4.6.1** (64-bit release for Windows)
- **Primary Executables in System `PATH`**:
  - `C:\Program Files\R\R-4.6.1\bin\x64\R.exe` — Interactive R console
  - `C:\Program Files\R\R-4.6.1\bin\x64\Rscript.exe` — Scripting and batch execution front-end
- **Userspace Operation**: All user analytical scripts, project library environments, and cache directories execute within userspace without requiring local administrative privileges.

#### Offline & Air-Gapped Operation

Workstations operate within a strictly isolated, air-gapped network enclave. Direct internet access to public CRAN or Bioconductor mirrors is blocked by firewall policy. All package installations resolve from internal Glasgow TRE package mirrors or pre-vetted local binary `.zip` archives.

---

## Getting Started

### Launching R

You can launch R in several ways depending on your workflow:

1. **PowerShell / Terminal**:
   Open Windows PowerShell or Windows Terminal and invoke `R` for the interactive console:
   ```powershell
   R
   ```
2. **Batch Script Execution**:
   Execute standalone research scripts non-interactively using `Rscript`:
   ```powershell
   Rscript "V:\my-project\scripts\analysis.R"
   ```
3. **JupyterLab Notebooks**:
   Open [JupyterLab StandAlone](jupyter.md) from your desktop shortcut and select the **R** kernel.

!!! tip "Verify Installed Core Libraries"

    You can verify that all bundled top-level libraries are ready for use by running this check in PowerShell:
    ```powershell
    Rscript -e "libs <- c('renv', 'dplyr', 'ggplot2', 'tidyr', 'data.table', 'readr', 'readxl', 'haven', 'arrow'); invisible(sapply(libs, library, character.only = TRUE)); cat('All core R libraries loaded successfully.\n')"
    ```

---

## How-To Guides

### Ingesting Research Data Formats

The bundled libraries support direct reading of all standard research formats without requiring additional packages:

```r
library(dplyr)
library(readr)
library(readxl)
library(haven)
library(arrow)
library(data.table)

# 1. Delimited Text / CSV (readr or data.table)
df_csv <- read_csv("V:/my-project/data/cohort.csv")
dt_fast <- fread("V:/my-project/data/large_cohort.csv")

# 2. Excel Workbooks (readxl)
df_excel <- read_excel("V:/my-project/data/clinical_table.xlsx", sheet = "Cohort1")

# 3. Statistical Legacy Formats (haven)
df_spss  <- read_sav("V:/my-project/data/survey.sav")
df_stata <- read_dta("V:/my-project/data/longitudinal.dta")
df_sas   <- read_sas("V:/my-project/data/registry.sas7bdat")

# 4. Columnar Apache Parquet (arrow)
df_parquet <- read_parquet("V:/my-project/data/genomics.parquet")
```

### Managing Project Reproducibility with `renv`

To ensure study reproducibility without conflicting with other projects, initialize an `renv` environment inside your project workspace on the `V:` drive:

1. In R, navigate to your project directory and initialize `renv`:
   ```r
   setwd("V:/my-project")
   renv::init()
   ```
2. `renv` creates a project-local library while linking to existing pre-installed system packages, saving disk space.
3. Once your analysis scripts are validated, snapshot your environment:
   ```r
   renv::snapshot()
   ```
   This generates a portable `renv.lock` file in `V:\my-project\` that documents the exact package dependency graph.

!!! caution "Do Not Locate Virtual Environments on SMB Roaming Shares"

    Always keep temporary build directories and package caches in local machine storage (`%LOCALAPPDATA%`). Roaming profiles (`%APPDATA%`) and SMB shares do not support NTFS directory junctions and degrade file access latency.

---

## Recommended Workstation Specifications

Statistical computations in R, particularly data wrangling on large tabular cohorts or fitting complex mixed-effects models, are primarily memory-bound:

| Resource | Recommended Specification | Notes |
| :--- | :--- | :--- |
| **System Memory (RAM)** | **16 GB to 64 GB** | R holds data objects entirely in RAM by default. For datasets exceeding 5 million rows, 32 GB to 64 GB is strongly recommended. |
| **Processor (vCPU)** | **4 to 8 vCPUs** | Speeds up vectorized matrix operations, parallel computing (`parallel`, `future`), and `data.table` multi-threaded sorting. |
| **Project Storage (`V:\`)** | **Variable by project** | Persistent, backed up analytical share for storing datasets (`.csv`, `.parquet`, `.rds`), scripts, and `renv.lock` files. |
| **Local Disk (`C:`)** | **30 GB+ free** | Required for local R package caches (`%LOCALAPPDATA%`) and temporary disk buffering. |

---

## Storage Best Practices

Understanding where R stores packages, temporary files, and configurations is essential to prevent latency and roaming profile sync issues:

| Storage Location | Purpose | Guidelines |
| :--- | :--- | :--- |
| **`V:\<project-name>\`** | Research scripts (`.R`), datasets, outputs, figures, and `renv.lock` files. | Permanent, network-backed project storage accessible to all project members. |
| **`%LOCALAPPDATA%\R\`** | Local package libraries (`win-library\4.6`), compilation caches. | Fast local NVMe storage. Keeps large collections of small package files off network shares. |
| **`%APPDATA%`** | Lightweight R configuration files (`.Rprofile`, `.Renviron`). | Roams with your Active Directory profile across workstations. |

!!! caution "Do Not Install R Libraries Directly on Network Shares"

    Do not configure `R_LIBS_USER` pointing directly to an SMB share (`V:` or UNC paths) unless using `renv` with local cache links. High file-count operations over SMB degrade performance and can trigger file locking errors.

---

## Troubleshooting & Support

| Symptom | Probable Cause | Recommended Resolution |
| :--- | :--- | :--- |
| **`package 'xyz' is not available for this version of R`** | Package is not available on the internal Glasgow TRE mirror. | Submit an R package request ticket to your TRE representative. |
| **`cannot open URL ... /src/contrib/...`** | R is attempting to reach external CRAN over the blocked public internet. | Verify that `options(repos = ...)` points to the internal mirror endpoint. |
| **`installation of package '...' had non-zero exit status`** | Attempted to compile a source package (`.tar.gz`) without Rtools compilers. | Request the pre-compiled Windows binary version (`.zip`). |
| **`Error: cannot allocate vector of size ...`** | Dataset exceeded available system RAM. | Switch to chunked processing, use `arrow::open_dataset()`, or request increased workstation RAM. |

---

## Requesting Additional R Packages

If your research requires CRAN or Bioconductor packages that are not currently available on the internal repository:

1. Submit a package request through your **Glasgow TRE Representative** or email [tre@glasgow.com](mailto:tre@glasgow.com?subject=R%20Package%20Request).
2. Include the package name, exact version required, list of dependencies, and analytical rationale.
3. Packages are vetted for security and license compliance, downloaded, and made available on the internal mirror.

---

## Related Documentation

- [Python Core](python-core.md) — Python runtime and package management with Astral `uv`.
- [JupyterLab StandAlone](jupyter.md) — Interactive notebook environment supporting both Python and R kernels.
- [LibreOffice](libreoffice.md) — Tabular spreadsheet viewing for quick data inspection.
- [Data Transfer Guidelines](../faq/data-transfer.md) — Importing data and exporting approved results.