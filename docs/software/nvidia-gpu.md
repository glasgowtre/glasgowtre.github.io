---
title: NVIDIA vGPU Acceleration
---

# NVIDIA vGPU Acceleration & Machine Learning

## Overview

#### Service Offering

Glasgow TRE provisions is able to offer research workstations with **GPU** hardware acceleration based on NVIDIA's vGPU technology.<br>

This allows the researcher to to request the right amount of GPU resource (from 4 GB to 96(2x48) GB) that is appropriate for their work.  

Virtual machines have full access to CUDA cores and CUDA v13 framework for:

-  deep learning and GPU-accelerated computing and training
-  computer vision, 
-  3D medical volume rendering (such as 3D Slicer), and
-  GPU-accelerated Python libraries (`torch`, `tensorflow`, `jax`, `rapids`, `cupy`).


---

### Cuda Version

NVIDIA vGPU drivers are installed on the host hypervisor and are compatible with CUDA v13.0.


### GPU Acceleration in Python


To utilize GPU acceleration within Jupyter notebooks and Python environments, your virtual environment must have an **NVIDIA CUDA-enabled PyTorch build** rather than the standard CPU-only build.

!!! note "PyTorch CPU vs. GPU Builds"

    PyTorch distributes distinct binary wheel variants for CPU and GPU architectures.<br> Package managers (`uv`, `pip`) **will** resolve to the CPU-only package unless explicitly directed to the CUDA build. 

---
#### 1. Acquiring the Correct PyTorch Build (GPU vs. CPU-only)


* **GPU-enabled build (`torch==x.y.z+cuXXX`)**: Bundles pre-compiled CUDA kernels and NVIDIA runtime libraries (e.g., `+cu130`). This build allows PyTorch to offload tensor operations directly to GPU hardware.

* **CPU-only build (`torch==x.y.z` or `torch==x.y.z+cpu`)**: Contains no CUDA runtime binaries or GPU kernels. If installed, PyTorch will run entirely on the system CPU *even if your workstation has an NVIDIA vGPU attached and `nvidia-smi` shows the driver is active.*



!!! warning  "Installing CUDA-enabled PyTorch"
    When installing PyTorch inside your project virtual environment, explicitly specify the **CUDA release tag** hosted on our internal repository:

    ```powershell
    # Using uv (recommended)
    uv pip install "torch==2.14.1+cu130" "torchvision==0.29.1+cu130"

    # Using pip
    pip install "torch==2.14.1+cu130" "torchvision==0.29.1+cu130"
    ```
!!! warning "Avoid Accidental CPU Overwrites by Companion Packages"
    Libraries such as `torchvision`, `torchaudio`, or third-party packages (e.g., `timm`, `monai`, `transformers`) often declare a generic dependency on `torch`. 
    
    If you install them separately without pinning, `pip` may attempt to satisfy their dependency by installing the latest standard CPU wheel from the mirror, overwriting your GPU build. Always install companion packages together with the matching `+cu130` build, or install them with `--no-deps` if their metadata conflicts.

#### 2. Verifying GPU Availability in a Notebook Cell

Run the following snippet inside a Jupyter notebook cell to verify that your environment has loaded the CUDA-compiled PyTorch binary and can communicate with the GPU:
```python
import torch
print(f"PyTorch Version:  {torch.__version__}")
print(f"CUDA Runtime:     {torch.version.cuda}")
print(f"CUDA Available:   {torch.cuda.is_available()}")
if torch.cuda.is_available():
    device_id = 0
    print(f"Device Count:     {torch.cuda.device_count()}")
    print(f"Device Name:      {torch.cuda.get_device_name(device_id)}")
    print(f"Compute Cap:      {torch.cuda.get_device_capability(device_id)}")
    
    # Run a quick tensor computation on the GPU
    x = torch.randn(1000, 1000, device="cuda")
    y = torch.matmul(x, x)
    
    print(f"Memory Allocated: {torch.cuda.memory_allocated(device_id) / (1024**2):.2f} MB")
    print(f"Memory Reserved:  {torch.cuda.memory_reserved(device_id) / (1024**2):.2f} MB")
    print("GPU tensor operation successful!")
else:
    print("\nWARNING: PyTorch is running in CPU-only mode.")
    if "+cu" not in torch.__version__:
        print("Reason: You have installed a CPU-only PyTorch wheel. Reinstall with a +cuXXX variant.")
    else:
        print("Reason: The PyTorch build has CUDA support, but no compatible NVIDIA GPU driver was detected.")
```
---

#### 3. Troubleshooting Common Issues
| Symptom | Cause | Resolution |
| :--- | :--- | :--- |
| `torch.__version__` does not have `+cuXXX` (e.g. `2.5.1` or `2.5.1+cpu`) | A CPU-only wheel was installed. | Run `uv pip install --force-reinstall "torch==2.14.1+cu130"` (or your required CUDA version). |
| `torch.cuda.is_available()` returns `False` despite having a `+cuXXX` version | The VM has no vGPU profile assigned, or the NVIDIA Windows Display Driver is not loaded. | Open PowerShell and run `nvidia-smi`. If `nvidia-smi` fails, contact the TRE Helpdesk to allocate a vGPU. |
| `RuntimeError: operator torchvision::... does not exist` | ABI mismatch between `torch` and `torchvision`. | `torchvision` C++ extensions must be compiled against the exact PyTorch C++ ABI. Ensure both use matching CUDA variants (e.g., `torch==2.14.1+cu130` and `torchvision==0.29.1+cu130`). |


## Critical Storage Best Practices for Deep Learning

Deep learning frameworks place extreme read/write demands on filesystems when loading model weights, caching datasets, and writing checkpoints. Follow these storage guidelines to prevent performance degradation and profile crashes:

!!! danger "Never Store Deep Learning Model Weights or Caches on Network Shares (`V:\`) or Roaming Profiles (`%APPDATA%`)"

    - **Do NOT place caches on network mounts (`V:\` or SMB shares)**: <br>Framework caches (Hugging Face `HF_HOME`, PyTorch `TORCH_HOME`, or training checkpoints) require high-throughput random I/O and POSIX filesystem locking. Network SMB shares suffer from latency and lack robust file locking, leading to corrupt weights and halted jobs.
    - **Do NOT place large models in Roaming folders (`%APPDATA%`, `Desktop`, `Documents`)**:<br> Active Directory Roaming Profiles synchronize these folders across the network during user logon and logoff. Saving gigabytes of model checkpoints here causes logoff hangs and profile synchronization failures.

### Recommended Storage Strategies

| Workload Type | Storage Recommendation | Details |
| :--- | :--- | :--- |
| **Small Transient Caches** | **Local Scratch (`$env:LOCALAPPDATA`)** | Redirect cache environment variables (`HF_HOME`, `TORCH_HOME`) to `$env:LOCALAPPDATA\cache` on local SSD storage. |
| **Heavy Model Weights & Checkpoints** | **Dedicated VM-Attached Storage** | For large foundation models, frequent training checkpoints, or heavy datasets, request dedicated high-IOPS VM-attached block storage from the TRE helpdesk. |
| **Analysis Code & Clean Exports** | **Project Workspace (`V:\`)** | Research scripts, summary logs, and final exported models/tables belong on the project network drive. |

---

## Support & Requesting GPU Capacity

- **Missing GPU or Driver Error**: If `nvidia-smi` reports no devices found or a driver mismatch, contact the service desk.
- **Requesting Larger vGPU Profiles**: If your research project requires additional VRAM (e.g., upgrading from 4 GB to 8 GB+ or 16 GB+ contact  **Glasgow TRE Helpdesk** at email [tre@glasgow.com](mailto:tre@glasgow.com?subject=vGPU%20Allocation%20Request) or contact your TRE representative.
---

## Related Documentation

- [Python Core](python-core.md) — PyTorch and TensorFlow setup with `uv`.
- [JupyterLab StandAlone](jupyter.md) — Interactive GPU-accelerated computing and notebook workflows.
- [3D Slicer](slicer.md) — GPU-accelerated medical volume rendering and MONAI / TotalSegmentator AI segmentation.
