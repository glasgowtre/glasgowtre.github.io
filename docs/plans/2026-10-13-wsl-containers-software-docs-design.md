# Design Document: WSL and Container Documentation

## Section 1: Page Structure & Navigation

### File Locations
1. `docs/software/wsl.md` — Windows Subsystem for Linux (WSL) Guide
2. `docs/software/containers.md` — Containers & Apptainer Guide
3. `docs/software/.pages` — Updated navigation order:
   ```yaml
   title: Software
   nav:
     - python.md
     - jupyter.md
     - wsl.md
     - containers.md
   ```

### Visual & Stylistic Alignment
- Follows the design language established in [`python.md`](file:///mnt/c/Users/nv15r/src/glasgowtre/glasgowtre.github.io/docs/software/python.md) and the Glasgow TRE material palette.
- Includes concise bulleted **Overview**, code block **Quick Start / Demo**, informative callout admonitions (`!!! info`, `!!! tip`), and clear command breakdowns.

---

## Section 2: `docs/software/wsl.md` Specification

### 1. Header & Overview
- **Title**: Windows Subsystem for Linux (WSL)
- **Our Approach**: Glasgow TRE provides native Linux capability within Windows workstations. Rather than forcing a pre-installed instance on all workstations, the platform provisions access to an approved enterprise Linux distribution.
- **Distribution**: Pre-configured **Rocky Linux 10** WSL distribution tailored for scientific computing and TRE compliance.
- **Enterprise Provisioning**: WSL features and distro access are pre-configured through Glasgow TRE automated workstation management (`glasgowtre-ansible`).

### 2. Quick Start / Demo
- Listing available distributions:
  ```powershell
  wsl --list --online
  ```
- Installing the Rocky 10 distribution:
  ```powershell
  wsl --install -d rocky-10
  ```
- Launching and verifying:
  ```powershell
  wsl -d rocky-10
  cat /etc/os-release
  ```

### 3. File System Access & Interoperability
- Navigating Windows project shares from WSL:
  - Windows drives mounted under `/mnt/c/`, `/mnt/v/` (project data share).
- Best practice tips:
  - Keep high-performance I/O and compiled code inside the Linux filesystem (`/home/<user>/...`) or map to `/mnt/v/` for persistent shared artifacts.
  - Accessing WSL files from Windows Explorer via `\\wsl$\rocky-10\`.

### 4. Developer Tools & IDE Integration
- Opening VS Code inside WSL:
  ```bash
  code .
  ```
- VS Code Remote - WSL extension integration for development directly within the Linux environment.
- Linking to the container workflows described in [Containers & Apptainer](containers.md).

---

## Section 3: `docs/software/containers.md` Specification

### 1. Header & Overview
- **Title**: Containers & Apptainer
- **No Third-Party Desktop Runtimes**: Glasgow TRE enables native container execution inside WSL without requiring heavy third-party desktop utilities (such as Docker Desktop or Podman Desktop), avoiding licensing, elevated privilege, and background service overhead.
- **Primary Scientific Runtime**: **Apptainer** (formerly Singularity) is provided as the primary container system for reproducible research, batch computing, and HPC parity.
- **OCI Container Support**: Lightweight rootless container tools available natively within the Rocky Linux 10 WSL environment.

### 2. Why Apptainer for Glasgow TRE?
- Unprivileged user execution (no root daemon or elevated rights required).
- Single-file container image format (`.sif`), making experiments easily portable, versionable, and auditable.
- Native access to host GPUs and filesystem paths without complex network virtualization.

### 3. Quick Start & Common Workflows
- **Running an Apptainer Container**:
  ```bash
  apptainer run my_analysis.sif
  ```
- **Interactive Shell inside a Container**:
  ```bash
  apptainer shell --bind /mnt/v/project:/data my_analysis.sif
  ```
- **Executing a Specific Command**:
  ```bash
  apptainer exec my_analysis.sif python script.py
  ```
- **Building / Converting Images**:
  - Converting OCI/Docker archive images to SIF format or building from definition files within the enclave.

### 4. Rootless OCI Container Workflows
- Running standard OCI containers within WSL using native rootless tools (e.g. `podman` inside the Rocky 10 WSL instance).
- Comparison table: When to choose **Apptainer** (scientific workloads, pipelines, HPC parity) vs. **OCI containers** (microservices, web servers, developer tools).
