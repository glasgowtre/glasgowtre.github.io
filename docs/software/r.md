---
title: R Runtime
---

# R Runtime & Package Management

## Overview

#### Service Offering

Glasgow TRE provides the **R statistical computing runtime** for epidemiological analysis, biostatistics, econometrics, bioinformatics, and reproducible data science. R is installed machine-wide with 64-bit binaries pre-configured in the system `PATH`, enabling interactive terminal analysis, non-interactive batch scripting via `Rscript`, R Markdown reporting, and project library isolation using `renv`.

#### Version & Configuration

- **R 4.6.1** (64-bit release for Windows)
- **Primary Executables in System `PATH`**:
  - `C:\Program Files\R\R-4.6.1\bin\x64\R.exe` — Interactive R console
  - `C:\Program Files\R\R-4.6.1\bin\x64\Rscript.exe` — Scripting and batch execution front-end
- **Userspace Operation**: All analytical scripts, project library environments, and package installations execute in userspace without requiring local administrative privileges.

#### Offline & Air-Gapped Operation

Workstations operate within a strictly isolated, air-gapped network enclave. Direct internet access to public CRAN or Bioconductor mirrors is blocked by firewall policy. All package installations resolve from internal Glasgow TRE package mirrors or pre-vetted local binary `.zip` archives.

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

## Getting Started

### 1. Interactive Launch

Open **PowerShell**, **Windows Terminal**, or **Command Prompt** and verify that the R runtime is available:

```powershell
# Verify R interpreter version
R.exe --version

# Verify R scripting front-end version
Rscript.exe --version
```

To launch an interactive R console session:

```powershell
R.exe --no-save
```

!!! tip "Exiting the R Console"

    To exit an interactive R session, type `q()` and press Enter. When prompted `Save workspace image? [y/n/c]:`, enter `n` to avoid leaving stale `.RData` files in your working directory.

---

### 2. Executing R Scripts Non-Interactively (`Rscript`)

Execute standalone analysis scripts or inline code expressions using `Rscript`:

```powershell
# Run a script from your analytical project workspace
Rscript V:\my-project\analysis.R

# Execute an inline R expression
Rscript -e "cat('Hello from R in Glasgow TRE\n')"

# Pass arguments to an R script
Rscript V:\my-project\process_cohort.R --cohort-id 42 --export-dir V:\my-project\outputs
```

---

## How-To Guides

### 1. Managing Project Libraries with `renv`

To ensure analytical reproducibility and prevent library version conflicts between projects, use `renv` to maintain isolated project-specific package libraries:

#### Initialize `renv` in Your Project Directory

1. Navigate to your project directory on the analytical workspace drive (`V:\`):
   ```powershell
   cd V:\my-project
   ```
2. Start R and initialize `renv`:
   ```r
   # Inside project directory in R
   install.packages("renv")
   renv::init()
   ```
3. `renv` creates a project-local library and an `renv.lock` file that records the exact package versions and sources.

#### Snapshot and Restore Dependencies

Before sharing your code with collaborators or submitting results for air-lock egress review, snapshot your environment:

```r
renv::snapshot()
```

When a collaborator opens the project on their workstation, they can recreate the exact environment with:

```r
renv::restore()
```

---

### 2. Configuring the Internal CRAN Mirror

Workstations resolve packages through the internal Glasgow TRE package mirror:

```r
# Set repository to the internal CRAN mirror
options(repos = c(CRAN = "https://storage.dc1.glasgowtre.ac.uk:9021/public/software/r/cran"))
```

To make this permanent across all your R sessions, add this line to your personal `.Rprofile` located in your profile directory (`%USERPROFILE%\Documents\.Rprofile` or `%APPDATA%\.Rprofile`):

```r
# %USERPROFILE%\Documents\.Rprofile
local({
  r <- getOption("repos")
  r["CRAN"] <- "https://storage.dc1.glasgowtre.ac.uk:9021/public/software/r/cran"
  options(repos = r)
})
```

---

### 3. Installing Pre-Approved Local Binary Packages

If you have been supplied with approved binary package zip archives through the data transfer air-lock:

```r
# Install a pre-approved Windows binary package
install.packages("C:/path/to/package_archive.zip", repos = NULL, type = "win.binary")
```

!!! important "Windows Requires Binary Packages (`type = 'win.binary'`)"

    Standard Windows research workstations do not include full C/C++/Fortran build toolchains (Rtools). Always install pre-compiled Windows binary packages (`.zip`) rather than source tarballs (`.tar.gz`).

---

### 4. Running R in JupyterLab StandAlone (`IRkernel`)

You can run interactive R notebooks side-by-side with Python in JupyterLab StandAlone:

1. Launch R in PowerShell:
   ```powershell
   R.exe --no-save
   ```
2. Install and register the `IRkernel` package:
   ```r
   install.packages("IRkernel")
   IRkernel::installspec(name = "ir_tre", display_name = "R 4.6.1 (Glasgow TRE)")
   q()
   ```
3. Launch JupyterLab from your desktop or Start Menu. The **R 4.6.1 (Glasgow TRE)** notebook option will appear in the Launcher.

---

### 5. Recommended Analytical Workflows

#### Reading Large Datasets Efficiently

When working with tabular health data, use modern column-oriented libraries instead of base R `read.csv()`:

```r
# Fast CSV ingestion with data.table
library(data.table)
cohort <- fread("V:/my-project/data/cohort.csv")

# Parquet file ingestion with arrow
library(arrow)
df <- read_parquet("V:/my-project/data/genomic_matrix.parquet")
```

#### Generating and Exporting Publication Figures

Always save rendered plots directly to your project workspace (`V:\`):

```r
library(ggplot2)

p <- ggplot(cohort, aes(x = age, y = bmi, color = outcome)) +
  geom_point(alpha = 0.6) +
  theme_minimal() +
  labs(title = "Glasgow TRE Cohort Analysis", x = "Age", y = "BMI")

# Save high-resolution figure to analytical project workspace
ggsave("V:/my-project/outputs/figure1.png", plot = p, width = 8, height = 6, dpi = 300)
```

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
