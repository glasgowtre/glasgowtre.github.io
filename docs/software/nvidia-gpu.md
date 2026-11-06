---
title: NVIDIA vGPU Acceleration
---

# NVIDIA vGPU Acceleration & Machine Learning

## Overview

#### Service Offering

Glasgow TRE provisions high-performance research workstations with **NVIDIA virtual GPU (vGPU)** hardware acceleration. This enables GPU-accelerated computing for deep learning inference and training, computer vision, 3D medical volume rendering (such as 3D Slicer), and GPU-accelerated Python libraries (`torch`, `tensorflow`, `jax`, `rapids`, `cupy`).

#### Driver Architecture & Licensing

- **Driver Release Train**: Version **580** (Display Driver version **582.78**, DCH 64-bit)
- **Delegated License Service (NLS/DLS)**: vGPU licenses are automatically managed and renewed via the internal Glasgow TRE Delegated License Service. Workstations obtain licenses on startup without requiring manual researcher intervention.

---

## GPU Monitoring & CLI Commands

Open **PowerShell** or **Windows Terminal** to inspect GPU hardware status, utilization, and memory allocation:

### 1. Basic Status & Driver Overview

```powershell
nvidia-smi
```

This displays the active GPU model (e.g. NVIDIA L40S vGPU profile), driver version, CUDA version support, power draw, and VRAM utilization.

### 2. Continuous Monitoring

Query real-time GPU compute and memory utilization metrics every 2 seconds:

```powershell
nvidia-smi --query-gpu=utilization.gpu,utilization.memory,memory.used,memory.total --format=csv -l 2
```

### 3. Verify vGPU License Status

Confirm that the workstation is licensed with the internal license manager:

```powershell
nvidia-smi -q | Select-String -Pattern "vGPU Software License Status" -Context 0,2
```

Expected output indicates `Status: Licensed`.

---

## Machine Learning Framework Integration

Verify CUDA availability within your analytical environments:

### PyTorch CUDA Check

```powershell
python -c "import torch; print('CUDA Available:', torch.cuda.is_available()); print('Device Name:', torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'None')"
```

### TensorFlow GPU Check

```powershell
python -c "import tensorflow as tf; print('GPUs Available:', tf.config.list_physical_devices('GPU'))"
```

### JAX GPU Devices Check

```powershell
python -c "import jax; print('JAX Devices:', jax.devices())"
```

---

## Critical Storage Best Practices for Deep Learning

Deep learning frameworks place extreme read/write demands on filesystems when loading model weights, caching datasets, and writing checkpoints. Follow these storage guidelines to prevent performance degradation and profile crashes:

!!! danger "Never Store Deep Learning Model Weights or Caches on Network Shares (`V:\`) or Roaming Profiles (`%APPDATA%`)"

    - **Do NOT place caches on network mounts (`V:\` or SMB shares)**: Framework caches (Hugging Face `HF_HOME`, PyTorch `TORCH_HOME`, or training checkpoints) require high-throughput random I/O and POSIX filesystem locking. Network SMB shares suffer from latency and lack robust file locking, leading to corrupt weights and halted jobs.
    - **Do NOT place large models in Roaming folders (`%APPDATA%`, `Desktop`, `Documents`)**: Active Directory Roaming Profiles synchronize these folders across the network during user logon and logoff. Saving gigabytes of model checkpoints here causes logoff hangs and profile synchronization failures.

### Recommended Storage Strategies

| Workload Type | Storage Recommendation | Details |
| :--- | :--- | :--- |
| **Small Transient Caches** | **Local Scratch (`$env:LOCALAPPDATA`)** | Redirect cache environment variables (`HF_HOME`, `TORCH_HOME`) to `$env:LOCALAPPDATA\cache` on local SSD storage. |
| **Heavy Model Weights & Checkpoints** | **Dedicated VM-Attached Storage** | For large foundation models, frequent training checkpoints, or heavy datasets, request dedicated high-IOPS VM-attached block storage from the TRE helpdesk. |
| **Analysis Code & Clean Exports** | **Project Workspace (`V:\`)** | Research scripts, summary logs, and final exported models/tables belong on the project network drive. |

---

## Support & Requesting GPU Capacity

- **Missing GPU or Driver Error**: If `nvidia-smi` reports no devices found or a driver mismatch, contact the service desk.
- **Requesting Larger vGPU Profiles**: If your research project requires additional VRAM (e.g., upgrading from 4 GB to 8 GB+ or 16 GB+ for full-resolution 3D medical segmentation or large language model inference), submit an infrastructure request to your **Glasgow TRE Representative** or email [tre@glasgow.com](mailto:tre@glasgow.com?subject=vGPU%20Allocation%20Request).
