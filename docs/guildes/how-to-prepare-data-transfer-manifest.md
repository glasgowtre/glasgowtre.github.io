---
title: How to prepare a data transfer manifest
description: Step-by-step guide for generating and verifying SHA-256 and MD5 file integrity manifests across Linux and Windows before transferring data to GlasgowTRE.
---

# How to prepare a data transfer manifest

## Objective

Generate a checksum manifest for your dataset before uploading to GlasgowTRE, and verify file integrity upon arrival to guarantee that no files were corrupted, truncated, or modified during transit.

---

## Before you begin

Make sure you have:

- A local directory containing the files you intend to transfer.
- Terminal access on your operating system:
    - **Linux / macOS**: Bash or Zsh with standard core utilities (`sha256sum`, `find`, `sort`).
    - **Windows**: PowerShell 5.1 / PowerShell 7+ or Command Prompt (`cmd.exe`).
- Read permissions on all data files and write permissions to create the manifest file.

---

## Step 1: Open a terminal in the target data directory

Navigate to the directory containing your payload files:

=== "Linux (Bash)"

    ```bash
    cd /path/to/data-folder
    ```

=== "Windows (PowerShell)"

    ```powershell
    Set-Location "C:\path\to\data-folder"
    ```

=== "Windows (Command Prompt)"

    ```cmd
    cd /d "C:\path\to\data-folder"
    ```

---

## Step 2: Generate the manifest (Recommended: SHA-256)

The standard GlasgowTRE format follows the GNU Coreutils checksum standard (`<hash>  <filename>`) using **SHA-256**. The output file is named `SHA256SUMS`.

Run the appropriate command for your operating system:

=== "Linux (Bash)"

    ```bash
    find . -type f ! -name "SHA256SUMS" -exec sha256sum {} + \
      | sed 's|  \./|  |' \
      | sort -k2 > SHA256SUMS
    ```

    !!! tip "Flat and nested directory support"
        The `find` command above recursively discovers files across all subfolders, normalizes relative paths (`subfolder/file.ext`), and safely excludes the manifest itself. It works identically for flat directories containing only root-level files.

=== "Windows (PowerShell)"

    ```powershell
    [System.IO.File]::WriteAllLines(
        "$PWD\SHA256SUMS",
        [string[]]@(
            Get-ChildItem -File -Recurse |
                Where-Object Name -ne 'SHA256SUMS' |
                Sort-Object FullName |
                ForEach-Object {
                    $hash = (Get-FileHash -LiteralPath $_.FullName -Algorithm SHA256).Hash.ToLower()
                    $relPath = $_.FullName.Substring($PWD.Path.Length).TrimStart('\').Replace('\', '/')
                    "$hash  $relPath"
                }
        ),
        [System.Text.UTF8Encoding]::new($false)
    )
    ```

    !!! note "UTF-8 without BOM, POSIX path separators, and literal paths"
        Using `[System.IO.File]::WriteAllLines` with `[System.Text.UTF8Encoding]::new($false)` prevents Windows PowerShell 5.1 from injecting a Byte Order Mark (BOM). Normalizing directory separators with `.Replace('\', '/')` produces POSIX-standard relative paths (`subfolder/file.ext`) required by Linux `sha256sum -c`. Passing `-LiteralPath` ensures filenames or directories containing brackets (`[` and `]`) are hashed accurately without wildcard interpretation errors.

=== "Windows (Command Prompt)"

    ```cmd
    powershell -NoProfile -Command ^
      "[System.IO.File]::WriteAllLines('SHA256SUMS', " ^
      "[string[]]@(Get-ChildItem -File -Recurse | " ^
      "Where-Object Name -ne 'SHA256SUMS' | " ^
      "Sort-Object FullName | " ^
      "ForEach-Object { " ^
      "  $hash = (Get-FileHash -LiteralPath $_.FullName -Algorithm SHA256).Hash.ToLower(); " ^
      "  $rel = $_.FullName.Substring($PWD.Path.Length).TrimStart('\').Replace('\', '/'); " ^
      "  ($hash + '  ' + $rel) " ^
      "}), " ^
      "[System.Text.UTF8Encoding]::new($false))"
    ```

    !!! tip "Nested subdirectories and archiving"
        All commands above recursively process files across all nested subdirectories out of the box, preserving relative folder paths. If your dataset contains tens of thousands of small files, archiving them into a single compressed archive before transfer is still recommended for transfer performance (see [FAQ Question 6](../faq/preparing-data-for-transfer.md#6-what-other-steps-should-i-take-before-transferring-large-datasets)).

---

## Step 3: Verify the manifest locally before transfer

Verify the manifest against your local files before uploading to confirm the checksums were recorded accurately.

=== "Linux (Bash)"

    ```bash
    sha256sum -c SHA256SUMS
    ```

=== "Windows (PowerShell)"

    ```powershell
    Get-Content SHA256SUMS |
        Where-Object { $_ -match '\S' } |
        ForEach-Object {
            $expectedHash, $file = $_ -split '\s+', 2
            $valid = (Test-Path -LiteralPath $file) -and
                ((Get-FileHash -LiteralPath $file -Algorithm SHA256).Hash.ToLower() -eq $expectedHash.ToLower())
            $status = if ($valid) { "OK" } else { "FAILED" }
            [PSCustomObject]@{ File = $file; Status = $status }
        }
    ```

=== "Windows (Command Prompt)"

    ```cmd
    powershell -NoProfile -Command ^
      "Get-Content SHA256SUMS | " ^
      "Where-Object { $_ -match '\S' } | " ^
      "ForEach-Object { " ^
      "  $expectedHash, $file = $_ -split '\s+', 2; " ^
      "  $valid = (Test-Path -LiteralPath $file) -and " ^
      "    ((Get-FileHash -LiteralPath $file -Algorithm SHA256).Hash.ToLower() -eq $expectedHash.ToLower()); " ^
      "  $status = if ($valid) { 'OK' } else { 'FAILED' }; " ^
      "  [PSCustomObject]@{ File = $file; Status = $status } " ^
      "}"
    ```

### Verification checkpoint

Every file must report `OK`:

=== "Linux (Bash)"

    ```text
    dataset_part1.tar.gz: OK
    metadata.csv: OK
    raw_data/sample_01.fastq: OK
    raw_data/sample_02.fastq: OK
    ```

=== "Windows (PowerShell)"

    ```text
    File                     Status
    ----                     ------
    dataset_part1.tar.gz     OK    
    metadata.csv             OK    
    raw_data/sample_01.fastq OK    
    raw_data/sample_02.fastq OK    
    ```

=== "Windows (Command Prompt)"

    ```text
    File                     Status
    ----                     ------
    dataset_part1.tar.gz     OK    
    metadata.csv             OK    
    raw_data/sample_01.fastq OK    
    raw_data/sample_02.fastq OK    
    ```

If any file displays `FAILED` or `MISSING`, investigate whether the file was modified, in use, or locked before proceeding.

---

## Step 4: Transfer files and manifest to GlasgowTRE

1. Upload your data files alongside the generated `SHA256SUMS` file into your GlasgowTRE target folder using SFTP (Port 2022) or the web transfer service.
2. Ensure `SHA256SUMS` sits in the exact same directory as the payload files it describes.

See [How to use GlasgowTRE secure web file transfer service](how-to-connect-to-service.md) for transfer service login instructions.

---

## Step 5: Verify file integrity after transfer

Once the upload completes, or once you sign in to your GlasgowTRE workstation, verify that the files arrived intact without bit rot or packet corruption.

Run the verification command inside the destination directory:

=== "Linux (Bash)"

    ```bash
    sha256sum -c SHA256SUMS
    ```

    To suppress noise and only print files that fail:
    ```bash
    sha256sum --quiet -c SHA256SUMS
    ```

=== "Windows (PowerShell)"

    ```powershell
    Get-Content SHA256SUMS |
        Where-Object { $_ -match '\S' } |
        ForEach-Object {
            $expectedHash, $file = $_ -split '\s+', 2
            $valid = (Test-Path -LiteralPath $file) -and
                ((Get-FileHash -LiteralPath $file -Algorithm SHA256).Hash.ToLower() -eq $expectedHash.ToLower())
            $status = if ($valid) { "OK" } else { "FAILED" }
            [PSCustomObject]@{ File = $file; Status = $status }
        }
    ```

=== "Windows (Command Prompt)"

    ```cmd
    powershell -NoProfile -Command ^
      "Get-Content SHA256SUMS | " ^
      "Where-Object { $_ -match '\S' } | " ^
      "ForEach-Object { " ^
      "  $expectedHash, $file = $_ -split '\s+', 2; " ^
      "  $valid = (Test-Path -LiteralPath $file) -and " ^
      "    ((Get-FileHash -LiteralPath $file -Algorithm SHA256).Hash.ToLower() -eq $expectedHash.ToLower()); " ^
      "  $status = if ($valid) { 'OK' } else { 'FAILED' }; " ^
      "  [PSCustomObject]@{ File = $file; Status = $status } " ^
      "}"
    ```

### Verification checkpoint

- A return code of `0` and `OK` on all items confirms complete cryptographic integrity.
- If any file fails verification, re-transfer that specific file.

---

## Troubleshooting

| Symptom | Root Cause | Resolution |
| :--- | :--- | :--- |
| `No such file or directory` during `-c` verification | The manifest file was run from a different directory than where the files reside. | Run the verification command directly within the folder containing both the manifest and data files. |
| Verification fails on the first file on Linux (`: no such file`) | The manifest was generated on Windows with a UTF-8 BOM (`EF BB BF`). | Re-generate using the provided PowerShell snippet which explicitly enforces `[System.Text.UTF8Encoding]::new($false)`. |
| Linux verification fails with `No such file or directory` on nested files (`\subdir\file: FAILED open or read`) | The manifest was generated on Windows with backslashes (`\`) instead of POSIX slashes (`/`). | Re-generate using the provided PowerShell snippet (which converts paths with `.Replace('\', '/')`), or convert existing separators on Linux via `tr '\\' '/' < SHA256SUMS \| sha256sum -c`. |
| PowerShell throws `InvokeMethodOnNull` or generates empty hashes on paths with `[` or `]` | `Get-FileHash` treats square brackets as wildcard pattern boundaries when `-LiteralPath` is omitted. | Re-generate using the provided snippets which specify `-LiteralPath` for all hashing and path validation calls. |
| Linux `md5sum -c` fails with `no properly formatted checksum lines found` on `manifest.txt` | The  manifest contains Windows CRLF line endings (`\r\n`) that append `\r` to the hash field. | Run the verification command which uses `sub(/\r$/, "", $2)` in awk to strip carriage returns before piping to `md5sum -c`. |
| `FAILED` checksum on large files | The upload was interrupted, truncated, or suffered network corruption. | Re-transfer the affected file via SFTP (port 2022) with resume capability enabled. |
| Subdirectories reported as directories during hash generation | Using wildcards like `sha256sum *` attempts to pass directories directly to the hashing binary. | Use the recommended `find . -type f` command which filters exclusively for files and traverses nested directories. |

---

## Related documentation

- [How to use GlasgowTRE secure web file transfer service](how-to-connect-to-service.md)
- [Data Transfer FAQ](../faq/data-transfer.md)
- [Preparing Data for Transfer FAQ](../faq/preparing-data-for-transfer.md)
