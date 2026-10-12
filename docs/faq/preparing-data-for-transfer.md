---
title: Preparing Data for Transfer
---

# Preparing Data for Transfer

This page answers frequently asked questions regarding data preparation, checksum manifest standards, and payload verification for uploads to GlasgowTRE.

---

### 1. Do I need to create a checksum manifest before transferring data?

**Yes.** We strongly recommend generating a checksum manifest for every dataset uploaded to GlasgowTRE. Transferring multi-gigabyte or terabyte datasets across networks can occasionally result in subtle corruption, truncated files, or network dropouts. Having a pre-computed manifest allows you and the GlasgowTRE system to cryptographically verify bit-for-bit file integrity after arrival.

---

### 2. Which checksum format and algorithm should I use?

GlasgowTRE recommends the industry-standard **GNU Coreutils SHA-256** format:

- **Filename:** `SHA256SUMS`
- **Format:** `<sha256-hex>  <filename>` (two spaces between the 64-character lowercase hexadecimal hash and the filename)
- **Algorithm:** SHA-256 (FIPS 180-4, collision-resistant)

This standard format is natively verified on Linux systems via `sha256sum -c SHA256SUMS` and easily validated across Windows and macOS environments.

---

### 3. Can I use MD5 or a tab-separated manifest instead?

While some legacy workflows use MD5 or custom formats like `<filename><TAB><md5>`, this architecture is **not recommended** for modern research data governance:

1. **Cryptographic Weakness:** MD5 is vulnerable to collision attacks (RFC 6151). While sufficient for accidental bit flips, it fails institutional data security baselines.
2. **Tool Incompatibility:** Inverting columns breaks native check flags (`sha256sum -c` or `md5sum -c`), requiring recipients to write custom parsing scripts.

If your specific data agreement or ingest pipeline strictly requires the legacy tab-separated MD5 format, refer to the [Alternative Recipe in our How-To Guide](../guildes/how-to-prepare-data-transfer-manifest.md#alternative-recipe-legacy-tab-delimited-md5-manifest-manifesttxt).

---

### 4. How do I avoid cross-platform encoding and line-ending issues between Windows and Linux?

When generating checksum manifests on Windows to be verified on Linux:

- **Avoid UTF-8 Byte Order Marks (BOM):** Standard Linux utilities (`sha256sum`) interpret the 3-byte UTF-8 BOM (`EF BB BF`) as part of the first filename or hash, triggering parsing errors. Always emit UTF-8 without BOM (e.g. using `[System.Text.UTF8Encoding]::new($false)` in PowerShell).
- **Line Endings:** While GNU coreutils 8.27+ handles Windows CRLF (`\r\n`) gracefully in standard formats, custom parsers often break. Using POSIX LF (`\n`) is safest across all platforms.
- **Paths and Directory Separators:** Use relative filenames or paths (e.g. `file.dat` or `subfolder/file.dat`) with forward slashes (`/`) rather than Windows backslashes (`\`), and avoid absolute Windows drive paths (`C:\...`). Linux utilities interpret backslashes as literal filename characters rather than directory separators.

---

### 5. Where can I find the step-by-step commands to generate and verify manifests?

For complete step-by-step instructions with command tabs for Linux (Bash), Windows (PowerShell), and Windows (Command Prompt), see our dedicated guide:

👉 **[How to prepare a data transfer manifest](../guildes/how-to-prepare-data-transfer-manifest.md)**

---

### 6. What other steps should I take before transferring large datasets?

- **Consolidate small files:** If transferring millions of small files, consider archiving them into `.tar` or compressed archives first to prevent file system metadata bottlenecks.
- **Check transfer protocol:** For datasets exceeding a few gigabytes, use native **SFTP (Port 2022)** rather than the web browser interface. See the [Data Transfer FAQ](data-transfer.md) for details on resumable transfers and connection parameters.