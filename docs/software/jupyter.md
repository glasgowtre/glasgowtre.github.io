---
title: JupyterLab StandAlone
---

# JupyterLab StandAlone

## Overview

#### Service Offering

Glasgow TRE provides **JupyterLab StandAlone** as an integrated desktop interactive computing environment for Python data analysis, machine learning exploration, and reporting. It comes pre-configured with a curated Python analytical virtual environment, eliminating complex environment setups while allowing researchers to install additional packages or create custom kernels without administrative privileges.

#### Version & Curated Kernel

- **JupyterLab StandAlone 4.6.3** (64-bit desktop application)
- **Default Curated Kernel**: `Python 3.12 (default-tre-jupyter-env)` pre-loaded with core analytical libraries: `pip`, `jupyterlab`, `ipykernel`, `pandas`, `polars`, `matplotlib`, and `scipy`.
- **Pre-Configured Internal Mirrors**: Configured to resolve Python wheels directly from internal Glasgow TRE mirrors (`repo.hlz.glasgowtre.ac.uk`). Direct internet downloads are disabled.

#### Air-Gapped Operation & Self-Healing Architecture

Workstations feature a self-healing launcher wrapper. Upon launch, it automatically verifies that the curated virtual environment, Jupyter kernel specification, and welcome notebook (`Welcome_to_GlasgowTRE.ipynb`) exist in the user profile. If absent or damaged, the launcher repairs them dynamically before starting the interface.

---

## Getting Started

You can launch JupyterLab StandAlone in any of the following ways:

- Double-click the **JupyterLab** shortcut on your desktop (`C:\Users\Public\Desktop\JupyterLab.lnk`).
- Select **JupyterLab** from the **Start Menu**.
- Launch from **PowerShell**:
  ```powershell
  & "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1"
  ```

Upon launch, JupyterLab opens directly into your project analytical workspace (preferred drive `V:\`, falling back to `Documents` if unmounted).

!!! caution "Save Research Work to the Analytical Project Workspace (`V:\`)"

    Always store your notebooks, analytical scripts, and datasets on your assigned project drive (`V:\<project-name>\`). Local machine storage (`C:`) is not backed up across sessions or host maintenance.

---

## How-To Guides

### 1. Install Packages Inside Notebooks (`%pip`)

You can install additional analytical libraries directly from a running notebook cell without leaving JupyterLab or opening a terminal:

1. Open your notebook in JupyterLab.
2. In a code cell, run the `%pip` magic command:
   ```python
   %pip install seaborn statsmodels
   ```
3. Packages are automatically fetched from the secure internal Glasgow TRE package mirror (`repo.hlz.glasgowtre.ac.uk`).
4. If prompted, restart the notebook kernel (**Kernel → Restart Kernel…**) to import the newly installed packages.

!!! tip "Pre-configured System `pip.ini`"

    The system-wide configuration (`C:\ProgramData\pip\pip.ini`) directs both `%pip` and terminal `pip` commands to the internal mirror with trusted host verification, requiring no extra command-line flags.

---

### 2. Create an Isolated Project Virtual Environment

If your project requires specific dependency trees or custom package versions:

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

    JupyterLab Desktop is configured with its environment path (`pythonEnvsPath`) pointing to your consolidated virtual environment base directory (`$env:LOCALAPPDATA\virtualenvs`). Environments created in this directory or via JupyterLab Desktop's **Manage Python environments** interface will reside alongside `default-tre-jupyter-env` and be automatically discovered by JupyterLab:

    ```powershell
    uv venv "$env:LOCALAPPDATA\virtualenvs\my_custom_env" --python 3.12
    ```

---

### 3. Register a Project Environment as a Jupyter Kernel

To make your custom virtual environment selectable in the JupyterLab Launcher and notebook kernel switcher:

```powershell
# Navigate to your project virtual environment directory or run with uv
uv run python -m ipykernel install --user --name "my_analysis" --display-name "Python (My Analysis)"
```

The kernel specification is saved in `%APPDATA%\jupyter\kernels\my_analysis\` and will appear immediately in the JupyterLab Launcher kernel selector.

---

### 4. Manage and Remove Registered Kernels

To view all active registered kernels:

```powershell
uv run jupyter kernelspec list
```

To remove a project kernel when an analysis is completed or no longer required:

```powershell
uv run jupyter kernelspec remove "my_analysis" -f
```

---

### 5. Command-Line Control via `jlab` CLI

JupyterLab StandAlone provides the `jlab` command-line utility for automation and opening workspaces:

```powershell
# Open current directory in JupyterLab
jlab .

# Open a specific notebook directly
jlab V:\my_analysis\notebook.ipynb

# Open with an explicit Python virtual environment
jlab --python-path "$env:LOCALAPPDATA\virtualenvs\default-tre-jupyter-env\Scripts\python.exe"

# List discovered Python environments
jlab env list

# Inspect application settings and logs
jlab config list
jlab logs show
```

---

### 6. Working with Imported External Notebooks

Notebooks developed outside Glasgow TRE may reference generic kernel names (such as `python3`) that do not exist locally. When opening an imported notebook:

1. If a prompt indicates that the kernel is not found, click the **Kernel selector** in the top-right corner of the notebook toolbar.
2. Select your active curated kernel: **`Python 3.12 (default-tre-jupyter-env)`** (or any custom project kernel you have registered).

---

## Storage Best Practices

Understanding where data and configurations reside ensures performance and avoids profile synchronization failures:

| Storage Domain | Location | Intended Contents |
| :--- | :--- | :--- |
| **Analytical Workspace (`V:`)** | `V:\<project-name>` | Research notebooks, datasets, scripts, exports. Network share backed up and shared across project members. |
| **Local Machine Storage (`%LOCALAPPDATA%`)** | `%LOCALAPPDATA%\virtualenvs`<br>`%LOCALAPPDATA%\uv` | Python runtime installations, virtual environment directories, package caches, launcher logs. Fast local SSD storage supporting NTFS junctions. |
| **Personal Roaming Space (`%APPDATA%`)** | `%APPDATA%\jupyterlab-desktop`<br>`%APPDATA%\jupyter\kernels` | Lightweight configuration (`settings.json`), registered kernel specs. Roams with your Active Directory profile across workstations. |

!!! warning "Avoid Creating Virtual Environments on Network Shares or Roaming Profiles"

    High-file-count directories (such as Python `virtualenvs` or build caches) and directories requiring NTFS directory junctions or symlinks MUST NOT be placed on network drives (`V:`) or roaming profiles (`%APPDATA%`, `Documents`, `Desktop`). SMB shares do not support NTFS junctions (`os error 1`) and degrade performance. Always locate virtual environments in `%LOCALAPPDATA%`.

---

## Troubleshooting & Support

- **Kernel shows "Disconnected" or fails to start**: Restart JupyterLab or run `& "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1" -NoLaunch` in PowerShell to re-verify the userspace environment.
- **Package installation error (`403 Forbidden` / `Not Found`)**: The requested library is not present on the internal Glasgow TRE package mirror.
- **Requesting new packages**: Contact the helpdesk at [tre@glasgow.com](mailto:tre@glasgow.com?subject=JupyterLab%20Package%20Request) with the package name, version, and research justification.

---

## Related Documentation

- [Python Core](python-core.md) — Manage analytical environments, runtimes, and libraries with Astral `uv`.
- [NVIDIA vGPU Acceleration](nvidia-gpu.md) — GPU acceleration for PyTorch, TensorFlow, and deep learning notebooks.
- [3D Slicer](slicer.md) — Medical imaging visualization and AI segmentation.
- [R Runtime](r.md) — Statistical computing and package management with `renv`.