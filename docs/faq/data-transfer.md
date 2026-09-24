# Frequently Asked Questions: Data Transfer

This page answers common operational and technical questions regarding data ingress and file transfers into the GlasgowTRE environment.

---

### 1. Is this an HTTPS transfer service, or an HTTP wrapper for an SFTP one?

It is **neither an HTTP wrapper nor a proxy**.

The service runs a unified, native multi-protocol transfer engine ([SFTPGo](https://github.com/drakkan/sftpgo)) supporting both:

- **HTTPS** (web-transfer interface via port `443`)
- **Native SFTP** (via port `2022`)

Both protocols connect directly to the same underlying storage and authentication service. Files uploaded through either protocol arrive in the same target directories with identical permissions and access controls.

---

### 2. Is the service suitable for multiple 500GB individual files (e.g. 23 files totaling ~11.5 TB in one operation)?

The recommended protocol depends heavily on the volume and individual file sizes:

- **SFTP (Port 2022 — Strongly Recommended):** **Yes.** A dedicated SFTP client (such as Cyberduck, FileZilla, WinSCP, or CLI tools like `sftp` / `rsync` over SSH) can queue all 23 files (~11.5 TB total) in a single operation and process the queue automatically without manual intervention.
- **HTTPS (Web Transfer — Not Recommended for Large Files):** While the web interface technically allows queuing multiple files, uploading individual 500GB files via a web browser is very prone to browser tab crashes, memory exhaustion, and HTTP proxy or network timeouts.

!!! warning "Browser Upload Limitations"
    For datasets with individual files larger than a few gigabytes, or total batch sizes in the hundreds of gigabytes or terabytes, always use **native SFTP (Port 2022)** rather than the web browser interface.

---

### 3. Will it process multiple files in parallel or sequentially?

- **HTTPS (Web Transfer):** **Sequentially only.** The web interface transfers 1 file at a time; it only triggers the next upload once the current file completes.
- **SFTP (Port 2022):** While the SFTP protocol inherently supports multiple concurrent connections, **we advise against configuring parallel transfers at this time**. Because the GlasgowTRE service enforces Multi-Factor Authentication (MFA), each new concurrent connection spawned by an SFTP client triggers a separate 2FA prompt/challenge. This can lead to session disruptions, timeout errors, and failed parallel streams.

!!! tip "Client Setting Recommendation: Limit to 1 Transfer at a Time"
    We strongly recommend configuring your SFTP client queue settings to **1 transfer at a time (sequential)**.

!!! note "Roadmap: Parallel Transfers"
    We recognise the importance of parallel transfers for high-volume data and are actively investigating secure mechanisms to enable concurrent streams without repeated MFA prompts in the future.

---

### 4. Does the service support resuming paused or interrupted uploads?

- **HTTPS (Web Transfer):** **No.** The web browser client does not support resumable or chunked uploads. If a browser upload is interrupted or the network drops, the transfer must restart from 0%.
- **SFTP (Port 2022):** **Yes.** Native SFTP clients support resuming/appending to interrupted or paused uploads based on byte offsets. Given 500GB file sizes, resumability is essential to prevent restarting multi-hour transfers from scratch in the event of transient network disruptions or client disconnections.
