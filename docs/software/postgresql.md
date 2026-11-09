---
title: PostgreSQL
---

# PostgreSQL & PostGIS

## Overview

#### Service Offering

Glasgow TRE can provision research workstations with an:

-  enterprise-grade **PostgreSQL** relational database management system, equipped with
-  the **PostGIS** spatial database extension and
-  the **pgAdmin 4** graphical administration interface.

The environment enables researchers to take advantage of the powers of a Relational database to store-analyse-transform using SQL on structure and unstructred datasets. The setup also allows the database to be interfaced with analytical programming environments such as Python, R, and Jupyter notebooks using popular database drivers and ORMs (e.g sqlalchemy, psycopg, django). 


!!! Note "Read Postgres Documentation"

    Users who want to use PostgreSQL and PostGIS to their full potential are encouraged to read the official documentation at [https://www.postgresql.org/docs/](https://www.postgresql.org/docs/) and [https://postgis.net/documentation/](https://postgis.net/documentation/).

    GlasgowTRE Stuff are unable to provide support for postgres or postgis beyond the scope of provisioning and basic configuration. Users are expected to be familiar with the use of relational databases and SQL.

!!! Warning "Data Backup"

    Postgresql's PGDATA folder is stored on the local system drive. The data is not backed up by the TRE. The researcher is responsible for exporting and backing up their research data to the project drive (`V:\`) using appropriate tools. 

    See bellow for details and basic instructions on how to export and backup your research data.

#### Pre-Configured Environment

Workstations provisioned with PostgreSQL arrive **fully pre-configured out of the box**:

- **PostgreSQL 18.6** (EnterpriseDB 64-bit release for Windows, version 18).
- **pgAdmin 4**: The graphical administration desktop application is pre-installed, with shortcuts available on the **Public Desktop** and in the **Start Menu**.
- **PostGIS 3.6.2 Extension**: The spatial database extension is pre-installed and activated in the default database (`CREATE EXTENSION IF NOT EXISTS postgis;`).
- **Spatial Foundation (GDAL)**: PostGIS 3.6.2 is built on and powered by **GDAL 3.9.2** (providing raster/vector geospatial format drivers including GeoPackage, Shapefile, and GeoParquet), alongside **GEOS 3.14.1** (topology geometry engine), **PROJ 8.2.1** (cartographic projections and coordinate transformations), and **SFCGAL 2.2.0**.
- **System `PATH` Integration**: The PostgreSQL binary directory (`C:\Program Files\PostgreSQL\18\bin`) is registered machine-wide in the system `PATH`, making command-line utilities such as `psql`, `pg_dump`, and `pg_restore` immediately available in any PowerShell or Command Prompt terminal.

#### Default Credentials & Localhost Authentication

- **Default Superuser**: `postgres`
- **Passwordless Localhost Access (`trust`)**: The cluster client authentication (`pg_hba.conf`) is pre-configured with **`trust`** for loopback connections (`127.0.0.1/32` and `::1/128`). **No password is required to log in from localhost.** Researchers can connect immediately via `psql`, pgAdmin 4, Python, and R without configuring or managing database passwords in connection strings.
- **Remote Host Security**: Inbound network connections from non-local hosts are governed by `scram-sha-256` password authentication and filtered by Windows Firewall.

---

## Recommended Workstation Specifications

Relational databases and spatial geospatial calculations (such as raster intersections and polygon transformations) can demand significant memory and disk I/O. For optimal performance, workstations running PostgreSQL and PostGIS should meet the following resource allocations:

| Resource | Recommended Specification | Notes |
| :--- | :--- | :--- |
| **Processor (vCPU)** | **4 to 8 vCPUs** | PostgreSQL 18 is pre-tuned for parallel query processing (`max_worker_processes = 8`, `max_parallel_workers = 6`, `max_parallel_workers_per_gather = 3`). |
| **System Memory (RAM)** | **16 GB minimum** (**32 GB recommended**) | 16 GB is sufficient for standard relational queries. 32 GB is strongly recommended when performing large table joins, spatial indexing (`GIST`), or in-memory raster analysis. |
| **Local System Disk (`C:`)** | **20 GB+ free disk space** | The database cluster files reside at `C:\ProgramData\PostgreSQL\18\data`. At least 20 GB free space on drive `C:` is required for cluster operation, temporary sort files, and WAL logs. |
| **Project Analytical Drive (`V:`)** | **Variable (per project)** | Persistent research data, raw CSV/Parquet inputs, and exported SQL database dumps (`pg_dump`) must always be saved to your assigned project folder on `V:\`. |

!!! info "Requesting Workstation Resource Adjustments"

    If your research dataset requires higher memory or processor allocations, contact Glasgow TRE Support at [tre@glasgow.com](mailto:tre@glasgow.com?subject=PostgreSQL%20Resource%20Allocation%20Request) to request an upgrade to your workstation specification.

!!! caution "Store Research Data and Backups on Drive `V:\`"

    The PostgreSQL database cluster resides locally on the workstation system drive (`C:\ProgramData\PostgreSQL\18\data`). Local drives are not backed up across workstation re-imaging or maintenance cycles. Always export project schemas and analytical datasets (`pg_dump` or CSV exports) to your project drive (`V:\<project-name>\`).

---

## Getting Started

!!! Note "No password is required for localhost connections"

    The PostgreSQL cluster is pre-configured with **`trust`** authentication for loopback connections. 
    
    You can connect from pgAdmin 4, `psql`, Python, and R without a password as the '**postgres**' superuser. 


### 1. Graphical Administration with pgAdmin 4

You should have a pgAdmin 4 link both in your Desktop and in the Start Menu. Using the link it will start the pgAdmin 4 application, which provides an web-based desktop interface for browsing databases, writing SQL queries, inspecting table schemas, and visualizing spatial geometry layers.

1. Launch pgAdmin 4:
   - Double-click the **pgAdmin 4** shortcut on your desktop (`C:\Users\Public\Desktop\pgAdmin 4.lnk`).
   - Or open the **Start Menu** and choose **PostgreSQL 18 → pgAdmin 4**.
2. Connect to the local database:
   - In the **Browser** pane on the left, expand **Servers**.
   - If prompted to register a new server connection:
     - **General Tab**: Set **Name** to `Local PostgreSQL 18`.
     - **Connection Tab**:
       - **Host name/address**: `127.0.0.1` (or `localhost`)
       - **Port**: `5432`
       - **Maintenance database**: `postgres`
       - **Username**: `postgres`
       - **Password**: Leave blank / empty (localhost `trust` authentication).
   - Click **Save**.
3. Open the **Query Tool** (**Tools → Query Tool**) to execute SQL commands and inspect results.

---

### 2. Command-Line Administration with `psql`

`psql` command should be available to you from your terminal.

```powershell
# Connect to the default database as user postgres (no password required)
psql -U postgres
```

To connect directly to a specific database or port:

```powershell
psql -h 127.0.0.1 -p 5432 -U postgres -d postgres
```

---

## PostGIS Spatial Database Extension

Glasgow TRE workstations bundle **PostGIS 3.6.2**, built on **GDAL 3.9.2**, **GEOS 3.14.1**, and **PROJ 8.2.1**. This spatial stack allows researchers to store, query, and manipulate geographical objects (points, lines, polygons, multi-polygons, and rasters) using SQL.

### Verifying the Spatial Stack

You can verify the active PostGIS and GDAL versions at any time by running:

```sql
SELECT PostGIS_Full_Version();
```

Example output:
```text
POSTGIS="3.6.2 3.6.2" [EXTENSION] PGSQL="180" GEOS="3.14.1-CAPI-1.20.1" PROJ="8.2.1" GDAL="GDAL 3.9.2, released 2024/05/10" LIBXML="2.11.5" LIBJSON="0.17" LIBPROTOBUF="1.4.1" WAGYU="0.5.0 (Internal)"
```

---

## Connecting from Analytics Toolchains


### 1. Python (`psycopg`, `SQLAlchemy`, and `GeoPandas`)

Workstations provisioned with Python can query PostgreSQL directly using `psycopg` (or `psycopg2`) and `SQLAlchemy`:

#### Basic Query with `psycopg`

```python
import psycopg

# Connect to local PostgreSQL without password
with psycopg.connect("host=127.0.0.1 port=5432 user=postgres dbname=postgres") as conn:
    with conn.cursor() as cur:
        cur.execute("SELECT version();")
        db_version = cur.fetchone()[0]
        print(f"Connected to: {db_version}")
```

#### Reading Spatial Data with `GeoPandas`

```python
import geopandas as gpd
from sqlalchemy import create_engine

# Create SQLAlchemy connection engine
engine = create_engine("postgresql+psycopg://postgres@127.0.0.1:5432/postgres")

# Read PostGIS spatial table directly into a GeoDataFrame
query = "SELECT id, catchment_name, geom FROM study_catchments;"
gdf = gpd.read_postgis(query, con=engine, geom_col="geom")

print(f"Loaded {len(gdf)} spatial geometries.")
print(f"Coordinate Reference System: {gdf.crs}")
print(gdf.head())
```

---

### 2. R (`DBI`, `RPostgres`, and `sf`)

Researchers working in R or [RStudio](r-studio.md) can interact with PostgreSQL using standard CRAN drivers:

#### Querying with `DBI` and `RPostgres`


    ```r
    library(DBI)
    library(RPostgres)

    # Establish connection without a password
    con <- dbConnect(
    RPostgres::Postgres(),
    host = "127.0.0.1",
    port = 5432,
    user = "postgres",
    password = "",
    dbname = "postgres"
    )

    # Fetch data into an R data frame
    df <- dbGetQuery(con, "SELECT catchment_name, ST_Area(geom) as area FROM study_catchments;")
    print(head(df))

    # Always disconnect when done
    dbDisconnect(con)
    ```
---

## Backing Up & Exporting Databases



Remember, data that is saved into the VM are not automatically backed up. To protect your research data against accidental loss or workstation decommissioning, always maintain regular backups on your project drive (`V:\`):

### Create a Database Backup (`pg_dump`)

Open PowerShell and execute `pg_dump` targeting your project network folder:

```powershell
# Create a compressed custom-format backup on drive V:
pg_dump -h 127.0.0.1 -p 5432 -U postgres -F c -b -v -f "V:\my-project\backups\postgres_backup_20261109.dump" postgres
```

### Restore a Database (`pg_restore`)

To restore a database dump into an existing or newly created database:

```powershell
# 1. Create target database (if restoring into a new database)
createdb -h 127.0.0.1 -p 5432 -U postgres cohort_restored

# 2. Restore using pg_restore
pg_restore -h 127.0.0.1 -p 5432 -U postgres -d cohort_restored -v "V:\my-project\backups\postgres_backup_20261109.dump"
```

!!! Tip "Read Postgres Documentation"

    Users who want to use PostgreSQL and PostGIS to their full potential are encouraged to read the official documentation at [https://www.postgresql.org/docs/](https://www.postgresql.org/docs/) and [https://postgis.net/documentation/](https://postgis.net/documentation/).

---

## Configuration & Performance Tuning Details

PostgreSQL 18 is tuned specifically for analytics workloads on Glasgow TRE workstations. You can inspect the configuration settings in `custom.conf` (located at `C:\ProgramData\PostgreSQL\18\data\custom.conf`).:

- **Asynchronous I/O (PostgreSQL 18 AIO Subsystem)**: `effective_io_concurrency = 200` and `maintenance_io_concurrency = 200` to maximize SSD throughput during large table scans and index builds.
- **Memory Allocations**:
  - `shared_buffers = 2GB`
  - `effective_cache_size = 6GB`
  - `work_mem = 9MB`
  - `maintenance_work_mem = 512MB`
- **WAL & Storage**: `wal_compression = lz4` (natively supported by the bundled `liblz4.dll`), with `min_wal_size = 1GB` and `max_wal_size = 4GB`.
- **Parallel Query Execution**: `max_worker_processes = 8`, `max_parallel_workers = 6`, and `max_parallel_workers_per_gather = 3`.
- **Huge Pages**: Configured as `huge_pages = try` to leverage Windows Large Pages when supported by system memory allocation privileges.

!!! Note "PostgreSQL Configuration Changes"

    Many of these settings can be modified during runtime using `ALTER SYSTEM SET <parameter> = <value>`. You can e.g. configure a pre-session query to adjust as you think is appropriate.

!!! warning "PostgreSQL Configuration Changes"
     Please note that by doing so you might crash your system or make it unusable, especially if you change the memory settings. 
---

## Related Documentation

- [Python Core](python-core.md) — Installing packages (`psycopg`, `SQLAlchemy`, `geopandas`) via the internal PyPI mirror.
- [JupyterLab](jupyter.md) — Interactive notebook workflows, SQL magics, and data visualization.
- [R](r.md) — Statistical programming with `DBI`, `RPostgres`, and `sf`.
- [Data Transfer Guidelines](../faq/data-transfer.md) — Procedures for exporting approved database extracts from the TRE.
