---
title: LibreOffice
---

# LibreOffice

## Overview

#### Approach

You can use LibreOffice in the Glasgow TRE to open and check CSV and Excel files, make quick edits, read documents, and write short notes or reports without leaving the environment.

!!! info "Not an Office Workstation"

    The TRE is mostly oriented for analysis, rather than office work. 
    
    For data processing, repeatable analysis, and large or complex datasets, use [Python](python-core.md) or [Jupyter notebooks](jupyter.md). LibreOffice is best for quick inspection and light editing.

#### Version

The platform provides **LibreOffice 26.8.1** (64-bit), installed for all users. No administrator rights are needed to use it.


#### Offline Operation

Glasgow TRE has no internet access. Update checks, online help, and telemetry are switched off.

---

## Getting Started

You can start LibreOffice in either of these ways:

- Double-click the **LibreOffice** shortcut on your desktop.
- Open the **Start Menu** and select **LibreOffice**.

You can also open a file directly: right-click it in File Explorer, choose **Open with**, and select the LibreOffice application you want.

!!! caution "Save Work to Your Project Drive"

    Always save research files to your project drive (`V:\<project-name>\`). Local drives are not backed up, and files saved there may be lost.

---

## How-To Guides

Beyond the basic usage of LibreOffice, you can use it to convert files to other formats, such as PDF or CSV. The following are some common tasks that may be useful.

### Export a document to PDF

1. Open the document.
2. Choose **File → Export as → Export as PDF…**.
3. Select your options, click **Export**, and save to your project folder on `V:\`.

!!! important "Check Before Exporting Results"

    Files that leave the TRE must go through the approved export process. See [Data Transfer Guidelines](../faq/data-transfer.md).

### Convert files from the command line

For many files at once, use the command line. Open **PowerShell** and run LibreOffice in headless mode with `soffice.com`:

```powershell
# Convert a Word document to PDF
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to pdf "V:\my-project\reports\summary.docx" --outdir "V:\my-project\reports"

# Convert an Excel spreadsheet to CSV
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to csv "V:\my-project\data\tables.xlsx" --outdir "V:\my-project\data"
```

| Flag | Purpose |
| :--- | :--- |
| `--headless` | Runs without opening a window. |
| `--convert-to <format>` | Target format, for example `pdf`, `csv`, `docx`, or `xlsx`. |
| `--outdir <directory>` | Folder where the converted file is saved. |

!!! tip "Use `soffice.com`, Not `soffice.exe`"

    The `.com` version prints output in your terminal. Always put file paths in double quotes and do not end a path with a backslash (use `"V:\my-project"`, not `"V:\my-project\"`).

---

## Settings and Troubleshooting

- **Your settings roam with you**: preferences, dictionaries, and templates are saved in your user profile and follow you between workstations.
- **Document recovery**: if LibreOffice closes unexpectedly, reopen it and choose **Recover** when prompted.
- **Large files**: Calc is not designed for very large datasets. If a file is slow to open or exceeds the sheet row limit (about 1 million rows), use [Python](python-core.md) instead.
- **Need help or a missing feature?** Contact the helpdesk at [tre@glasgow.com](mailto:tre@glasgow.com?subject=LibreOffice%20Query).

---

## Related Documentation

- [Python Core](python-core.md) — Process spreadsheets and CSV files with `pandas`, `openpyxl`, and `polars`.
- [Jupyter Notebooks](jupyter.md) — Interactive analysis and reporting.
- [Data Transfer Guidelines](../faq/data-transfer.md) — Importing data and exporting approved results.
