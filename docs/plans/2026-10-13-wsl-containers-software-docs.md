# WSL and Container Software Documentation Implementation Plan

> **For Antigravity:** REQUIRED WORKFLOW: Use `.agent/workflows/execute-plan.md` to execute this plan in single-flow mode.

**Goal:** Create comprehensive documentation for Windows Subsystem for Linux (Rocky Linux 10 distro) and Containers/Apptainer under the Software section of the Glasgow TRE handbook.

**Architecture:** Add two dedicated Markdown documentation pages (`docs/software/wsl.md` and `docs/software/containers.md`) and register them in `docs/software/.pages` alongside existing Python and Jupyter documentation, maintaining visual and structural consistency with Glasgow TRE handbook patterns.

**Tech Stack:** MkDocs Material, Markdown, `awesome-pages` plugin, Rocky Linux 10 WSL, Apptainer.

---

### Task 1: Create Windows Subsystem for Linux (WSL) Guide

**Files:**
- Create: `docs/software/wsl.md`
- Modify: `docs/software/.pages`

**Step 1: Write the documentation page `docs/software/wsl.md`**

Create `docs/software/wsl.md` containing:
- Frontmatter title: `Windows Subsystem for Linux (WSL)`
- **Overview**: Glasgow TRE approach to Linux computing, automated provisioning via `glasgowtre-ansible`, pre-configured Rocky Linux 10 distribution on demand.
- **Discovery & Installation Quick Start**:
  - `wsl --list --online` showing available internal Rocky Linux 10 distro.
  - `wsl --install -d rocky-10` command to install.
  - `wsl -d rocky-10` to launch and verify with `cat /etc/os-release`.
- **Filesystem Interoperability & Data Access**:
  - Windows drives mounted under `/mnt/c/` and project volume `/mnt/v/`.
  - Best practices for performance (keeping working directories in Linux filesystem `/home/<user>/` vs shared project data in `/mnt/v/`).
  - Accessing WSL files from Windows Explorer via `\\wsl$\rocky-10\`.
- **IDE Support**:
  - Launching VS Code with `code .` inside the WSL terminal.
  - Cross-link to container documentation (`containers.md`).

**Step 2: Update `docs/software/.pages` to register `wsl.md`**

Update `docs/software/.pages` to include `wsl.md`.

**Step 3: Run verification command to test build**

Run: `~/.local/bin/uv tool run mkdocs build --strict`
Expected: PASS (build succeeds with 0 warnings)

**Step 4: Commit**

```bash
git add docs/software/wsl.md docs/software/.pages
git commit -m "docs: add Windows Subsystem for Linux (WSL) guide"
```

---

### Task 2: Create Containers & Apptainer Guide

**Files:**
- Create: `docs/software/containers.md`
- Modify: `docs/software/.pages`

**Step 1: Write the documentation page `docs/software/containers.md`**

Create `docs/software/containers.md` containing:
- Frontmatter title: `Containers & Apptainer`
- **Overview**: Glasgow TRE container approach—native container execution inside WSL without 3rd-party desktop providers (no Docker Desktop or Podman Desktop licensing/daemons).
- **Why Apptainer for Glasgow TRE**:
  - Unprivileged execution (no root daemon or elevated rights needed).
  - Single-file container image format (`.sif`) for research auditability, reproducibility, and versioning.
  - High Performance Computing (HPC) parity and direct volume access.
- **Apptainer Quick Start & Workflows**:
  - Running a container: `apptainer run <image>.sif`
  - Interactive shell: `apptainer shell --bind /mnt/v/project:/data <image>.sif`
  - Executing specific commands: `apptainer exec <image>.sif python script.py`
  - Converting/building images within the enclave.
- **Rootless OCI Containers**:
  - Lightweight rootless container tools within Rocky Linux 10 WSL.
  - Practical comparison table: when to use Apptainer vs OCI containers.

**Step 2: Update `docs/software/.pages` to register `containers.md`**

Ensure `docs/software/.pages` lists both new files:
```yaml
title: Software
nav:
  - python.md
  - jupyter.md
  - wsl.md
  - containers.md
```

**Step 3: Run verification command to test build**

Run: `~/.local/bin/uv tool run mkdocs build --strict`
Expected: PASS (build succeeds with 0 warnings)

**Step 4: Commit**

```bash
git add docs/software/containers.md docs/software/.pages
git commit -m "docs: add Containers & Apptainer guide"
```

---

### Task 3: Cross-Linking & Navigation Polish

**Files:**
- Modify: `docs/software/wsl.md`
- Modify: `docs/software/containers.md`
- Modify: `docs/plans/task.md`

**Step 1: Verify and polish bi-directional links**

Ensure `wsl.md` links cleanly to `containers.md` and vice versa without broken anchors.

**Step 2: Run verification command to test build**

Run: `~/.local/bin/uv tool run mkdocs build --strict`
Expected: PASS (build succeeds with 0 warnings)

**Step 3: Commit and update tracker**

```bash
git add docs/software/wsl.md docs/software/containers.md docs/plans/task.md
git commit -m "docs: finalize software docs cross-links and task tracker"
```
