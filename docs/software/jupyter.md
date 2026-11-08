---
title: JupyterLab StandAlone
---

# JupyterLab StandAlone

## Overview

#### Service Offering

Glasgow TRE provides **JupyterLab StandAlone** as an integrated interactive computing environment for Python and R data science, statistical modeling, machine learning exploration, and reporting. It comes pre-configured with a curated Python analytical virtual environment out of the box, eliminating complex setup procedures while allowing researchers to install additional packages, create custom kernels, and isolate project environments without administrative privileges.

#### Version & Curated Environment

- **JupyterLab StandAlone 4.6.3** (64-bit desktop application)
- **Default Curated Kernel**: `Python 3.12 (default-tre-jupyter-env)` pre-loaded with core analytical libraries: `pip`, `jupyterlab`, `ipykernel`, `pandas`, `polars`, `matplotlib`, and `scipy`.
- **Pre-Configured Internal Mirrors**: Configured to resolve Python wheels directly from internal Glasgow TRE mirrors (`repo.hlz.glasgowtre.ac.uk`). Direct external internet downloads are disabled.

#### Air-Gapped Operation & Self-Healing Architecture

Workstations feature an automated self-healing launcher wrapper (`Launch-JupyterLab.ps1`). Upon every launch, the wrapper verifies that the curated virtual environment, Jupyter kernel specification, and starter welcome notebook (`Welcome_to_GlasgowTRE.ipynb`) exist in the user profile. If any component is absent or damaged, the launcher repairs it dynamically before starting the interface.

---

## Recommended Workstation Specifications

Interactive notebook analysis and data science pipelines can demand significant memory and compute resources, especially when processing large datasets or deep learning models:

| Resource | Recommended Specification | Notes |
| :--- | :--- | :--- |
| **System Memory (RAM)** | **16 GB to 32 GB** | 16 GB is sufficient for standard tabular data analysis (`pandas`, `polars`). 32 GB+ is recommended for in-memory joins, genomic arrays, or computer vision datasets. |
| **Processor (vCPU)** | **4 to 8 vCPUs** | Accelerates multi-threaded operations in `polars`, `numpy`, and parallelized kernel execution. |
| **GPU Acceleration (vGPU)** | **Optional (4 GB to 16 GB VRAM)** | Required when running PyTorch, TensorFlow, or JAX deep learning models within notebook cells. |
| **Local System Disk (`C:`)** | **50 GB+ free** | Accommodates userspace virtual environments (`%LOCALAPPDATA%\virtualenvs`), package wheel caches, and scratch space. |

---

## Getting Started

You can launch JupyterLab StandAlone using any of the following methods:

- **Desktop Shortcut**: Double-click the **JupyterLab** shortcut on your desktop (`C:\Users\Public\Desktop\JupyterLab.lnk`).
- **Start Menu**: Search for and select **JupyterLab**.
- **PowerShell**:
  ```powershell
  & "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1"
  ```

Upon launch, JupyterLab automatically opens into your project analytical workspace (preferred drive `V:\<project-name>\`, falling back to personal `Documents` if the project share is unmounted) and displays the starter **`Welcome_to_GlasgowTRE.ipynb`** notebook with your curated kernel active.

!!! caution "Save Research Notebooks and Data to the Analytical Project Workspace (`V:\`)"

    Always store your notebooks (`.ipynb`), analytical scripts, and datasets on your assigned project drive (`V:\<project-name>\`). Local machine storage (`C:`) is not backed up across sessions or maintenance re-imaging.

---

## How-To Guides

### 1. Install Packages Inside Notebooks (`%pip`)

You can install additional analytical libraries directly from a running notebook cell without leaving JupyterLab or opening a terminal:

1. Open your notebook in JupyterLab.
2. In a code cell, run the `%pip` magic command:
   ```python
   %pip install seaborn statsmodels scikit-learn
   ```
3. Packages are automatically retrieved and installed from the secure internal Glasgow TRE package mirror (`repo.hlz.glasgowtre.ac.uk`).
4. Once installed, restart the notebook kernel (**Kernel → Restart Kernel…**) to import the newly installed packages.

!!! tip "Pre-configured System `pip.ini`"

    The system-wide configuration (`C:\ProgramData\pip\pip.ini`) automatically directs `%pip` and terminal `pip` commands to the internal mirror with trusted host verification, requiring no extra command-line flags.

---

### 2. Create an Isolated Project Virtual Environment

When working on a research project with distinct package version requirements:

1. Open **PowerShell** or **Windows Terminal**.
2. Navigate to your project directory on the analytical workspace drive:
   ```powershell
   cd V:\my_analysis
   ```
3. Initialize the project and create an isolated virtual environment with `uv`:
   ```powershell
   uv init
   uv venv --python 3.12
   ```
4. Add the analytical packages your project requires, including `ipykernel`:
   ```powershell
   uv add pandas polars matplotlib scipy ipykernel
   ```

!!! info "Consolidated Virtual Environments Directory"

    JupyterLab Desktop is configured with its environment discovery path (`pythonEnvsPath`) pointing to your consolidated virtual environment base directory (`$env:LOCALAPPDATA\virtualenvs`). Environments created in this directory or via JupyterLab Desktop's **Manage Python environments** interface will reside alongside `default-tre-jupyter-env` and be automatically discovered by JupyterLab:

    ```powershell
    uv venv "$env:LOCALAPPDATA\virtualenvs\my_custom_env" --python 3.12
    ```

---

### 3. Register a Project Environment as a Jupyter Kernel

To make your custom virtual environment selectable in the JupyterLab Launcher and notebook kernel switcher:

```powershell
# Run ipykernel registration from your project virtual environment
uv run python -m ipykernel install --user --name "my_analysis" --display-name "Python (My Analysis)"
```

The kernel specification is saved in `%APPDATA%\jupyter\kernels\my_analysis\` and will appear immediately in the JupyterLab Launcher kernel selector.

---

### 4. Running R Notebooks in JupyterLab (`IRkernel`)

Researchers can run interactive R notebooks directly inside JupyterLab StandAlone using the `IRkernel` package:

1. Launch an interactive R session in PowerShell:
   ```powershell
   R.exe --no-save
   ```
2. Register the R kernel for your user profile:
   ```r
   # Install IRkernel if not already present
   install.packages("IRkernel")

   # Register kernel spec in %APPDATA%\jupyter\kernels\ir
   IRkernel::installspec(name = "ir_tre", display_name = "R 4.6.1 (Glasgow TRE)")
   q()
   ```
3. Open or refresh JupyterLab. An **R 4.6.1 (Glasgow TRE)** notebook icon will appear in the Launcher alongside Python.

---

### 5. GPU Acceleration in Notebooks (PyTorch / CUDA)

If your workstation is allocated an NVIDIA vGPU profile, you can verify and utilize GPU acceleration directly inside a notebook cell:

```python
import torch

print(f"PyTorch Version: {torch.__version__}")
print(f"CUDA Available:  {torch.cuda.is_available()}")
if torch.cuda.is_available():
    print(f"Device Name:     {torch.cuda.get_device_name(0)}")
    print(f"Memory Allocated: {torch.cuda.memory_allocated(0) / (1024**2):.2f} MB")
```

Refer to the [NVIDIA vGPU Acceleration](nvidia-gpu.md) guide for full driver and framework configuration details.

---

### 6. Manage and Remove Registered Kernels

To view all active registered kernels:

```powershell
uv run jupyter kernelspec list
```

To remove a project kernel when an analysis is completed or no longer required:

```powershell
uv run jupyter kernelspec remove "my_analysis" -f
```

---

### 7. Command-Line Control via `jlab` CLI

JupyterLab StandAlone includes a dedicated command-line utility (`jlab`) for automation and opening workspaces:

```powershell
# Open current directory in JupyterLab
jlab .

# Open a specific notebook directly
jlab V:\my_analysis\notebook.ipynb

# Open with an explicit Python virtual environment
jlab --python-path "$env:LOCALAPPDATA\virtualenvs\default-tre-jupyter-env\Scripts\python.exe"

# List discovered Python environments
jlab env list

# Inspect application settings and configuration
jlab config list

# Inspect application diagnostic logs
jlab logs show
```

---

### 8. Self-Healing Launcher Diagnostic Controls

The launcher wrapper provides diagnostic parameters for troubleshooting:

```powershell
# Verify or repair virtual environments and kernels without launching the GUI
& "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1" -BootstrapOnly

# Inspect the launcher execution log
Get-Content "$env:LOCALAPPDATA\GlasgowTRE\logs\jupyter-launch.log" -Tail 50
```

---

### 9. Working with Imported External Notebooks

Notebooks developed outside Glasgow TRE often reference generic kernel names (such as `python3`) that do not exist locally. When opening an imported notebook:

1. If a prompt indicates that the kernel is not found, click the **Kernel selector** in the top-right corner of the notebook toolbar.
2. Select your active curated kernel: **`Python 3.12 (default-tre-jupyter-env)`** (or any custom project kernel you have registered).

---

## Storage Best Practices

Understanding where data, environments, and configurations reside ensures performance and prevents profile synchronization failures:

| Storage Domain | Location | Intended Contents |
| :--- | :--- | :--- |
| **Analytical Workspace (`V:`)** | `V:\<project-name>` | Research notebooks, datasets, scripts, exports. Network share backed up and shared across project members. |
| **Local Machine Storage (`%LOCALAPPDATA%`)** | `%LOCALAPPDATA%\virtualenvs`<br>`%LOCALAPPDATA%\uv` | Python runtime installations, virtual environment directories, package caches, launcher logs. Fast local SSD storage supporting NTFS junctions. |
| **Personal Roaming Space (`%APPDATA%`)** | `%APPDATA%\jupyterlab-desktop`<br>`%APPDATA%\jupyter\kernels` | Lightweight configuration (`settings.json`), registered kernel specs. Roams with your Active Directory profile across workstations. |

!!! warning "Avoid Creating Virtual Environments on Network Shares or Roaming Profiles"

    High-file-count directories (such as Python `virtualenvs` or build caches) and directories requiring NTFS directory junctions or symlinks MUST NOT be placed on network drives (`V:`) or roaming profiles (`%APPDATA%`, `Documents`, `Desktop`). SMB shares do not support NTFS junctions (`os error 1`) and degrade performance. Always locate virtual environments in `%LOCALAPPDATA%`.

---

## Troubleshooting & Support

| Symptom | Probable Cause | Recommended Resolution |
| :--- | :--- | :--- |
| **Kernel shows "Disconnected" or fails to start** | Damaged kernel spec or virtual environment in user profile. | Run `& "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1" -BootstrapOnly` to self-heal the environment. |
| **`%pip` fails with `403 Forbidden` / `Not Found`** | Requested library is missing from the internal Glasgow TRE mirror. | Submit a package request ticket to your TRE representative. |
| **`os error 1: Incorrect function` during `uv venv`** | Attempting to create a virtual environment on an SMB network share (`V:` or roaming profile). | Create virtual environments strictly within `%LOCALAPPDATA%\virtualenvs\`. |
| **Launcher log reports environment initialization error** | Corrupted Python runtime cache. | Inspect `$env:LOCALAPPDATA\GlasgowTRE\logs\jupyter-launch.log` and delete corrupted subfolder in `$env:LOCALAPPDATA\uv\python`. |

---

## Requesting Additional Packages

If your project requires packages not currently available on the internal PyPI mirror:

1. Submit a package request through your **Glasgow TRE Representative** or email [tre@glasgow.com](mailto:tre@glasgow.com?subject=JupyterLab%20Package%20Request).
2. Specify the package name, requested version, and analytical rationale.
3. Once security and compliance reviews are completed, packages are mirrored internally for all project members.

---

## Related Documentation

- [Python Core](python-core.md) — Manage analytical environments, runtimes, and libraries with Astral `uv`.
- [R Runtime](r.md) — Statistical computing and package management with `renv`.
- [NVIDIA vGPU Acceleration](nvidia-gpu.md) — GPU acceleration for PyTorch, TensorFlow, and deep learning notebooks.
- [3D Slicer](slicer.md) — Medical imaging visualization and AI segmentation.
