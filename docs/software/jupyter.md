---
title: JupyterLab Desktop
---

# JupyterLab Desktop

## Overview

#### Service Offering

Glasgow TRE provides **JupyterLab Desktop** application based on Electron, as an integrated interactive environment mainly for Python for  data science, statistical modeling, machine learning exploration, and reporting. 

Provisioned worstations are pre-configured with a with an virtual environment out of the box, pre-loaded with core analytical libraries (`pip`, `jupyterlab`, `ipykernel`, `pandas`, `polars`, `matplotlib`, and `scipy`) additionally it can `pip install` additional libraries from the internal Glasgow TRE PyPI mirror (`repo.hlz.glasgowtre.ac.uk`) without requiring external internet access. For a list of the available libraries, see the [Python Core](python-core.md) guide.

#### Version & Curated Environment

- **JupyterLab Desktop 4.6.3** (64-bit desktop application)
- **Default Curated Kernel**: `Python 3.12 (default-tre-jupyter-env)`.
- **Pre-Configured Internal Mirrors**: Configured to resolve Python wheels directly from internal Glasgow TRE Python Index. Direct external internet downloads are disabled.

---

## Recommended Workstation Specifications

Interactive notebook analysis and data science pipelines can demand significant memory and compute resources, especially when processing large datasets or deep learning models. It is therefore recommennded to that your workstation to mee the following specifications for optimal performance:

| Resource | Recommended Specification | Notes |
| :--- | :--- | :--- |
| **System Memory (RAM)** | **16 GB to 32 GB** | 16 GB is sufficient for standard tabular data analysis (`pandas`, `polars`). 32 GB+ is recommended for in-memory joins, genomic arrays, or computer vision datasets. |
| **Processor (vCPU)** | **4 to 8 vCPUs** | Accelerates multi-threaded operations in `polars`, `numpy`, and parallelized kernel execution. |
| **GPU Acceleration (vGPU)** | **Optional (4 GB to 16 GB VRAM)** | Required when running PyTorch, TensorFlow, or JAX deep learning models within notebook cells. |
| **Local System Disk (`C:`)** | **50 GB+ free** | Accommodates userspace virtual environments (`%LOCALAPPDATA%\virtualenvs`), package wheel caches, and scratch space. |


!!! note "Recommended Workstation Specifications"

   Please contact Glasgow TRE Support to ask to change your workstations resource allocations if needed. 

---

## Getting Started

You can launch JupyterLab StandAlone using any of the following methods:

- **Desktop Shortcut**: Double-click the **JupyterLab** shortcut on your desktop (`C:\Users\Public\Desktop\JupyterLab.lnk`).
- **Start Menu**: Search for and select **JupyterLab**.
- **PowerShell**:
  ```powershell
  & "C:\Program Files\JupyterLab\Launch-JupyterLab.ps1"
  ```

Upon launch, JupyterLab automatically opens into your project analytical workspace (by default on  `V:\`) and displays the starter **`Welcome_to_GlasgowTRE.ipynb`** notebook with your curated kernel active.

!!! caution "Save Research Notebooks and Data to the Analytical Project Workspace (`V:\`)"

    Always store your notebooks (`.ipynb`), analytical scripts, and datasets on your assigned project drive (`V:\`). Local machine storage (`C:`) is not backed up across sessions or maintenance re-imaging.

---

## How-To Guides

### 1. Install Packages Inside Notebooks (`%pip`)

You can install additional analytical libraries directly from a running notebook cell without leaving JupyterLab or opening a terminal:

1. Open your notebook in JupyterLab.
2. In a code cell, run the `%pip` magic command:
   ```python
   %pip install seaborn statsmodels scikit-learn
   ```
3. Packages are automatically retrieved and installed from the secure internal Glasgow TRE package mirror.
4. Once installed, they should be already be available in the current session. If not, restart the notebook kernel (**Kernel → Restart Kernel…**) to import the newly installed packages.

!!! tip "Torch Packages"
      Both cpu and gpu versions of PyTorch are available on the internal mirror, depending on your workstation's vGPU allocation. If you don't have a vGPU, install the CPU-only version.

---

### 2. Register a Project Environment as a Jupyter Kernel

To make your custom virtual environment selectable in the JupyterLab Launcher and notebook kernel switcher:

```powershell
# Run ipykernel registration from your project virtual environment
uv run python -m ipykernel install --user --name "my_analysis" --display-name "Python (My Analysis)"
```

The kernel specification is saved in `%APPDATA%\jupyter\kernels\my_analysis\` and will appear immediately in the JupyterLab Launcher kernel selector.

### 3. GPU Acceleration in Notebooks (PyTorch / CUDA)

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

### 4. Working with Imported External Notebooks

Notebooks developed outside Glasgow TRE often reference generic kernel names (such as `python3`) that do not exist locally. When opening an imported notebook:

1. If a prompt indicates that the kernel is not found, click the **Kernel selector** in the top-right corner of the notebook toolbar.
2. Select your active curated kernel: **`Python 3.12 (default-tre-jupyter-env)`** (or any custom project kernel you have registered).

---

### 5. Storage Best Practices

Understanding where data, environments, and configurations reside ensures performance and prevents profile synchronization failures:

| Storage Domain | Location | Intended Contents |
| :--- | :--- | :--- |
| **Analytical Workspace (`V:`)** | `V:\<project-name>` | Research notebooks, datasets, scripts, exports. Network share backed up and shared across project members. |
| **Local Machine Storage (`%LOCALAPPDATA%`)** | `%LOCALAPPDATA%\virtualenvs`<br>`%LOCALAPPDATA%\uv` | Python runtime installations, virtual environment directories, package caches, launcher logs. Fast local SSD storage supporting NTFS junctions. |
| **Personal Roaming Space (`%APPDATA%`)** | `%APPDATA%\jupyterlab-desktop`<br>`%APPDATA%\jupyter\kernels` | Lightweight configuration (`settings.json`), registered kernel specs. Roams with your Active Directory profile across workstations. |

!!! warning "Avoid Creating Virtual Environments on Network Shares or Roaming Profiles"

    High-file-count directories (such as Python `virtualenvs` or build caches) and directories requiring NTFS directory junctions or symlinks MUST NOT be placed on network drives (`V:`) or roaming profiles (`%APPDATA%`, `Documents`, `Desktop`). SMB shares do not support NTFS junctions (`os error 1`) and degrade performance. Always locate virtual environments in `%LOCALAPPDATA%`.

---

### 6. Troubleshooting & Support

| Symptom | Probable Cause | Recommended Resolution |
| :--- | :--- | :--- |
| **`%pip` fails with `403 Forbidden` / `Not Found`** | Requested library is missing from the internal Glasgow TRE mirror. | Submit a package request ticket to your TRE representative. |
---

## Related Documentation

- [Python Core](python-core.md) — Manage analytical environments, runtimes, and libraries with Astral `uv`.
- [R Runtime](r.md) — Statistical computing and package management with `renv`.
- [NVIDIA vGPU Acceleration](nvidia-gpu.md) — GPU acceleration for PyTorch, TensorFlow, and deep learning notebooks.
- [3D Slicer](slicer.md) — Medical imaging visualization and AI segmentation.
