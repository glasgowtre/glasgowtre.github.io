---
title: LibreOffice
---

# LibreOffice Productivity Suite & Document Tooling

## Overview

- **Our Approach**: Glasgow TRE provides a standardized, centrally managed deployment of the LibreOffice productivity suite across secure Windows 11 research workstations. Researchers can inspect, author, and process spreadsheets, manuscripts, and reports directly via the desktop graphical interface, or leverage headless command-line document conversions in automated analytical pipelines without requiring local administrative privileges.

- **Deployed Version**: The platform provides **LibreOffice 26.8.1** (64-bit Windows release).

- **Installation Location**: LibreOffice is installed machine-wide to `C:\Program Files\LibreOffice` with program binaries located in `C:\Program Files\LibreOffice\program`.

- **Machine PATH Integration**: Executables (`soffice.exe` and `soffice.com`) reside in `C:\Program Files\LibreOffice\program`. By default, the binary directory is not appended to the system machine `PATH`; command-line invocations and automation scripts reference the console wrapper binary `C:\Program Files\LibreOffice\program\soffice.com` directly.

- **Automated Provisioning**: LibreOffice installation, air-gap policy enforcement, background update service suppression, and shortcut creation are automatically provisioned and validated via Glasgow TRE configuration management (`glasgowtre.software.libreoffice`).

- **Desktop Quick Reference**: An application shortcut is deployed to `C:\Users\Public\Desktop\LibreOffice.lnk` for all users, preserving Glasgow TRE's Public Desktop invariant and avoiding roaming profile shortcut duplication.

---

## Quick Start & Execution

LibreOffice is pre-installed machine-wide and available immediately upon logging into your research workstation.

### 1. Graphical Interface (GUI) Launching

You can launch LibreOffice through any of the following standard methods:

- **Public Desktop Shortcut**: Double-click the **LibreOffice** shortcut located on your desktop (`C:\Users\Public\Desktop\LibreOffice.lnk`).
- **Windows Start Menu**: Open the Start Menu and navigate to **LibreOffice**.
- **Individual Applications**: From the LibreOffice start center, access any of the integrated suite tools:
    - **Writer**: Word processing and structured documentation.
    - **Calc**: Spreadsheet analysis, data entry, and CSV inspection.
    - **Impress**: Presentations and slide decks.
    - **Draw**: Technical vector graphics, flowcharts, and diagramming.
    - **Base**: Lightweight database front-end.
    - **Math**: Formula and mathematical equation editor.

### 2. Command-Line & Headless Verification

For command-line execution and headless document pipelines, LibreOffice provides a dedicated console wrapper binary: **`soffice.com`**. 

!!! tip "Console Wrapper vs. GUI Binary"
    Always use `soffice.com` rather than `soffice.exe` when running commands in PowerShell or Windows Terminal. The `.com` wrapper attaches cleanly to the active terminal and streams standard output (`stdout`) and error messages (`stderr`), whereas `soffice.exe` runs asynchronously in the Windows GUI subsystem without terminal output.

Open **PowerShell** or **Windows Terminal** and verify the installed version:

```powershell
# Verify LibreOffice version from PowerShell
& "C:\Program Files\LibreOffice\program\soffice.com" --version
```

Example output:

```text
LibreOffice 26.8.1.2 6810(e6810...)
```

### 3. Headless Document Conversion

Analytical workflows often require converting research documentation, tabular data, or generated reports to standardized formats (such as PDF) without launching an interactive graphical window. LibreOffice supports batch document conversion using the `--headless` flag.

#### Converting Documents to PDF

To convert a Microsoft Word (`.docx`), Rich Text (`.rtf`), or plain text (`.txt`) file into a PDF:

```powershell
# Convert a Word document to PDF in the project directory
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to pdf "V:\my-project\reports\summary.docx" --outdir "V:\my-project\reports"

# Convert a plain text file to PDF
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to pdf "V:\my-project\outputs\findings.txt" --outdir "V:\my-project\outputs"
```

#### Converting Spreadsheets to PDF or CSV

You can also convert spreadsheets (`.xlsx`, `.ods`) to PDF or export specific sheets to CSV:

```powershell
# Convert an Excel spreadsheet to PDF
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to pdf "V:\my-project\data\tables.xlsx" --outdir "V:\my-project\data"

# Convert an OpenDocument Spreadsheet to CSV
& "C:\Program Files\LibreOffice\program\soffice.com" --headless --convert-to csv "V:\my-project\data\metrics.ods" --outdir "V:\my-project\data"
```

#### Key Headless Command Flags

| Flag | Purpose | Example |
| :--- | :--- | :--- |
| `--headless` | Runs without displaying a graphical interface or taskbar icon. | `soffice.com --headless ...` |
| `--convert-to <format>` | Specifies target export format (e.g. `pdf`, `csv`, `html`, `docx`). | `--convert-to pdf` |
| `--outdir <directory>` | Specifies destination directory where exported files are saved. | `--outdir "V:\my-project\reports"` |

!!! important "Always Quote File Paths"
    When passing file paths to `soffice.com` in PowerShell, enclose paths with spaces or drive letters in double quotes. Note that if a directory path ends with a trailing backslash immediately before a closing double quote (e.g. `"V:\my-project\"`), Windows argument parsers may escape the quote. Use `"V:\my-project"` without the trailing backslash.

---

## Air-Gap Lockdown & Update Policy

Glasgow TRE operates as a secure, air-gapped research enclave with no outbound internet connectivity. Standard software update checks, telemetry pings, and cloud sync services fail and can generate timeout errors or system logs.

LibreOffice in Glasgow TRE is locked down using a multi-layered defense-in-depth policy to ensure completely silent, offline operation:

### 1. Installer-Level Update Suppression

During automated provisioning via the MSI package, public properties explicitly suppress initial update registrations:

```ini
ALLUSERS=1 CREATEDESKTOPLINK=1 RebootYesNo=No ISCHECKFORPRODUCTUPDATES=0
```

Setting `ISCHECKFORPRODUCTUPDATES=0` prevents the Windows installer from scheduling periodic update checks upon first launch.

### 2. Disablement of Background Maintenance Service

The Windows background service **`LibreOfficeMaintenance`** (responsible for scheduling and staging background updates) is stopped and set to `disabled`. This prevents unauthorized background update attempts and eliminates service execution overhead.

### 3. Finalized Machine Policy (`noupdate.xcd`)

LibreOffice enforces enterprise configuration through XML Configuration Data (`.xcd`) files placed in `C:\Program Files\LibreOffice\share\registry\`. Glasgow TRE deploys a custom configuration file, **`noupdate.xcd`**, with all properties marked with `oor:finalized="true"`.

Because properties are finalized at the machine level, they cannot be overridden by user profiles or dialog settings:

- **Modern MAR Updater Disabled (LibreOffice 24.8+)**: The Mozilla ARchive (MAR) update engine is disabled and its endpoint URL cleared:
  ```xml
  <oor:component-data oor:name="Update" oor:package="org.openoffice.Office">
    <node oor:name="Update" oor:op="fuse">
      <prop oor:name="Enabled" oor:type="xs:boolean" oor:op="replace" oor:finalized="true">
        <value>false</value>
      </prop>
      <prop oor:name="URL" oor:type="xs:string" oor:op="replace" oor:finalized="true">
        <value></value>
      </prop>
    </node>
  </oor:component-data>
  ```
- **Legacy Update Check Job Disabled**: The legacy background `UpdateCheck` job is deactivated:
  ```xml
  <oor:component-data oor:name="Jobs" oor:package="org.openoffice.Office">
    <node oor:name="Jobs">
      <node oor:name="UpdateCheck" oor:op="fuse">
        <node oor:name="Arguments">
          <prop oor:name="AutoCheckEnabled" oor:type="xs:boolean" oor:op="replace" oor:finalized="true">
            <value>false</value>
          </prop>
        </node>
      </node>
    </node>
  </oor:component-data>
  ```
- **Suppressed Telemetry and Crash Reporting**: Automatic crash reporting (`CrashReport=false`) and anonymous usage metric logging (`CollectUsageInformation=false`) are disabled.
- **Suppressed Startup Prompts and External Links**: The "Tip of the Day" dialog (`ShowTipOfTheDay=false`), unknown file extension checks (`PerformFileExtCheck=false`), and periodic community donation/involvement prompts (`LastTimeGetInvolvedShown` and `LastTimeDonateShown` set to maximum timestamps) are suppressed.

### 4. Removal of Legacy Online Update Module

Any default `C:\Program Files\LibreOffice\share\registry\onlineupdate.xcd` file is deleted from the installation directory. This removes the legacy update check trigger completely and eliminates the "Check for Updates..." item from the LibreOffice **Help** menu.

---

## Storage Domains & Profile Management

LibreOffice respects Glasgow TRE's separation of user configuration and project analytical data:

### 1. User Settings & Roaming Profiles (`%APPDATA%`)

User-specific preferences, dictionaries, custom templates, and toolbars are stored in:

```text
%APPDATA%\LibreOffice\4\user\
```

- **Active Directory Roaming**: Because `%APPDATA%` roams across workstations via Active Directory Folder Redirection and Roaming Profiles, your custom interface settings and dictionaries follow your user account across workstation logins.
- **Enforced Security Baseline**: Even though personal preferences roam, the machine-level finalized configuration in `C:\Program Files\LibreOffice\share\registry\noupdate.xcd` takes precedence, ensuring security and air-gap restrictions remain strictly enforced.
- **Document Recovery**: Automatic recovery backups are saved locally under `%APPDATA%\LibreOffice\4\user\backup\`, protecting against data loss without impacting network share latency.

### 2. Project Analytical Documents (`V:\` Drive)

All research data, analytical spreadsheets, manuscript drafts, and exported documents **must** be stored on your assigned project network share:

```text
V:\<project-name>\
```

!!! caution "Do Not Save Research Documents to Local Drives"
    Local workstation drives (`C:\`) and temporary folders (`%TEMP%`, `%LOCALAPPDATA%`) are non-persistent or local to a single physical host. Always save research documents and final deliverables to the project drive (`V:\`), which is backed up, encrypted, and accessible to authorized team members.

---

## Related Documentation

- [Python Runtime & Package Management](python.md) — Automating analytical data processing and manipulating Excel/CSV files via `pandas`, `openpyxl`, and `polars`.
- [Jupyter Notebooks](jupyter.md) — Interactive notebook computing and reporting.
- [Data Transfer Guidelines](../faq/data-transfer.md) — Secure procedures for importing data and exporting approved research results.
