---
title: Windows Subsystem for Linux (WSL)
---

# Windows Subsystem for Linux (WSL 2)

## Overview

#### Service Offering

Glasgow TRE supports **Windows Subsystem for Linux 2 (WSL 2)** on Windows 11 research workstations. WSL 2 provides a complete, native Linux execution environment alongside Windows tools, allowing researchers to run Linux CLI utilities, shell scripts, Python/C/C++ pipelines, and bioinformatics packages within the secure enclave.

#### Version & Distribution Baseline

- **WSL 2 Runtime**: Version 3.0.1+ with managed Linux virtualization kernel.
- **Approved Baseline Distribution**: **Rocky Linux 10 (Glasgow TRE)** (`rocky-10`), matching the enterprise server baseline used across Glasgow TRE infrastructure.
- **Internal Offline Distribution Index**: Workstations are pre-configured with a machine-wide `DistributionInfo.json` manifest (`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss\DistributionListUrl`) pointing to internal mirror endpoints. Standard WSL CLI commands (`wsl --list --online`, `wsl --install`) discover and fetch approved distributions entirely offline without external internet access.

---

## Getting Started

### 1. Verify WSL Installation & Status

Open **PowerShell** or **Windows Terminal** to verify the subsystem:

```powershell
wsl --version
wsl --status
```

Expected output confirms WSL version 3.0.1 or higher with the WSL 2 virtualization architecture enabled.

---

### 2. View Available Approved Distributions

To list approved distributions available from the internal Glasgow TRE software catalog:

```powershell
wsl --list --online
```

Output:
```text
The following is a list of valid distributions that can be installed:
  NAME            FRIENDLY NAME
  rocky-10        Rocky Linux 10 (Glasgow TRE)
```

---

### 3. Install the Default Linux Distribution

Approved distributions are installed on demand:

```powershell
# Install Rocky Linux 10 without launching immediately
wsl --install rocky-10 --no-launch

# Or install and launch an interactive shell directly
wsl --install rocky-10
```

During the initial launch, follow the one-time prompt to configure your Linux username and password.

---

## Working in WSL & Storage Domains

WSL integrates seamlessly with Windows file drives, but respecting storage domain boundaries is crucial for performance and data safety:

### 1. Project Analytical Data (`/mnt/v`)

Your analytical project workspace drive (`V:\`) is automatically mounted inside WSL under `/mnt/v`:

```bash
# Navigate to your project directory inside WSL
cd /mnt/v/my-project
ls -la
```

!!! caution "Store Research Data and Code on `/mnt/v`"

    Always store your analytical datasets, code repositories, and outputs on `/mnt/v` (Windows `V:\`). This network share is resilient, backed up, and accessible across your research team.

### 2. Virtual Disk Storage (`%LOCALAPPDATA%`)

WSL 2 distribution root filesystems are stored as virtual hard disks (`.vhdx`) in `%LOCALAPPDATA%\Packages\` on the local workstation drive (`C:`):

- **Fast Local I/O**: Local SSD storage delivers maximum read/write performance for compilation, package installation, and container operations.
- **Do Not Move to Roaming Shares (`H:`)**: Network SMB shares do not support local virtual disk block caching and will cause WSL execution failures.

---

## Managing WSL Distributions

Common commands for managing WSL from PowerShell:

```powershell
# Check status and version of all installed distributions
wsl --list --verbose

# Run a specific distribution
wsl -d rocky-10

# Run a single command non-interactively
wsl -d rocky-10 -- uname -a

# Terminate a running distribution
wsl --terminate rocky-10

# Shut down the entire WSL subsystem
wsl --shutdown
```

---

## Air-Gapped Software Delivery Notice

All WSL packages and distribution images are securely mirrored from internal storage (`storage.dc1.glasgowtre.ac.uk:9021`). Direct external internet access is disabled. If your research workflow requires additional Linux packages, toolchains, or container runtimes within WSL, contact your **Glasgow TRE Representative** or email [tre@glasgow.com](mailto:tre@glasgow.com?subject=WSL%20Software%20Request).
