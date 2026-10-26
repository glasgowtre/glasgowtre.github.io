---
title: Python Core
---

# Python Core & Python Packages


## Overview

#### Approach

Glasgow TRE allow Python development is based on a Python Management approach, which allows user to tailor their their Python  environments according to their specific needs.

#### Management

This is based on Astral's [`uv`](https://docs.astral.sh/uv/getting-started/) Python manager. Users can install, manage, and switch between multiple Python versions and their associated packages.

#### Python Builds

Selected Python builds are sourced from [`astral-sh/python-build-standalone`](https://github.com/astral-sh/python-build-standalone) and hosted in an internal mirror. uv then is then downloading the selected version according to your request.


!!! info "Supported Python Versions" 

    please refer to the [Available Python Releases](#available-python-releases) section for a list of available versions.

#### Available Packages

Python package managers are preconfigured configured to use our internal PyPA mirror. This includes `pip` and `uv`. 


#### IDE Support

Environments made with uv are fully compatible with modern IDEs such as VS Code. This creates an ideal enviroment for developers who want to write and test their Python code.

!!! info "Note"

    [Jupyter notebooks](jupyter.md) use the same underlying infrastructure but are pre-configured and ready to be used.

---

## Additional Python Packages

If you need additional packages, please submit a package request ticket through your Glasgow TRE representative or send an email to the helpdesk at [tre@glasgow.com](mailto:tre@glasgow.com?subject=Python%20Package%20Request).

After we review your request, the packages will be made available to all users and projects. 

!!! info "Information Needed"

    Make sure to include the library name, requested version, and analytical rationale.

---

## Available Python Releases

!!! info "Supported Python Versions"

    It is possible to install, use, and switch between multiple Python versions.

=== "Python 3.12"

    | Release | Release Date | Release Type |
    | :--- | :--- | :--- |
    | ***3.12.14** | 2026-08-12 | Security Fix |
    | `3.12.13` | 2026-03-03 | Security Fix |
    | `3.12.12` | 2025-10-09 | Security Fix |
    | `3.12.11` | 2025-06-03 | Security Fix |
    | `3.12.10` | 2025-04-08 | Bugfix |
    | `3.12.9` | 2025-02-04 | Bugfix |
    | `3.12.8` | 2024-12-03 | Bugfix |
    | `3.12.7` | 2024-10-01 | Bugfix |
    | `3.12.6` | 2024-09-06 | Bugfix |
    | `3.12.5` | 2024-08-06 | Bugfix |
    | `3.12.4` | 2024-06-06 | Bugfix |
    | `3.12.3` | 2024-04-09 | Bugfix |
    | `3.12.2` | 2024-02-06 | Bugfix |
    | `3.12.1` | 2023-12-07 | Bugfix |
    | `3.12.0` | 2023-10-02 | Major Feature Release |

=== "Python 3.13"

    | Release | Release Date | Release Type |
    | :--- | :--- | :--- |
    | **3.13.15** | 2026-08-05 | Bugfix |
    | `3.13.14` | 2026-06-10 | Bugfix |
    | `3.13.13` | 2026-04-07 | Bugfix |
    | `3.13.12` | 2026-02-03 | Bugfix |
    | `3.13.11` | 2025-12-05 | Bugfix |
    | `3.13.10` | 2025-12-02 | Bugfix |
    | `3.13.9` | 2025-10-14 | Bugfix |
    | `3.13.8` | 2025-10-07 | Bugfix |
    | `3.13.7` | 2025-08-14 | Bugfix |
    | `3.13.6` | 2025-08-06 | Bugfix |
    | `3.13.5` | 2025-06-11 | Hotfix |
    | `3.13.4` | 2025-06-03 | Bugfix |
    | `3.13.3` | 2025-04-07 | Bugfix |
    | `3.13.2` | 2025-02-04 | Bugfix |
    | `3.13.1` | 2024-12-03 | Bugfix |
    | `3.13.0` | 2024-10-07 | Major Feature Release |

=== "Python 3.14"

    | Release | Release Date | Release Type |
    | :--- | :--- | :--- |
    | ***3.14.7** | 2026-08-05 | Bugfix |
    | `3.14.6` | 2026-06-10 | Bugfix |
    | `3.14.5` | 2026-05-10 | Bugfix |
    | `3.14.4` | 2026-04-07 | Bugfix |
    | `3.14.3` | 2026-02-03 | Bugfix |
    | `3.14.2` | 2025-12-05 | Bugfix |
    | `3.14.1` | 2025-12-02 | Bugfix |
    | `3.14.0` | 2025-10-07 | Major Feature Release |

=== "Python 3.15"

    | Release | Release Date | Release Type |
    | :--- | :--- | :--- |
    | `3.15.0rc1` | 2026-08-04 | Release Candidate 1 |
    | `3.15.0rc2` | 2026-09-01 | Release Candidate 2 |

---

## Available Packages

Inventory of **713 approved packages** available on the Glasgow TRE production mirror (Snapshot 20).

### Jump to Letter

[A](#a) | [B](#b) | [C](#c) | [D](#d) | [E](#e) | [F](#f) | [G](#g) | [H](#h) | [I](#i) | [J](#j) | [K](#k) | [L](#l) | [M](#m) | [N](#n) | [O](#o) | [P](#p) | [Q](#q) | [R](#r) | [S](#s) | [T](#t) | [U](#u) | [V](#v) | [W](#w) | [X](#x) | [Y](#y) | [Z](#z)

---

<h3 id="a">A</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `absl-py` | `2.5.1` |
| `accelerate` | `0.0.1`, `1.15.0` |
| `acvl-utils` | `0.2.6` |
| `agent-detector` | `2.0.0` |
| `aiobotocore` | `3.9.2` |
| `aiodns` | `2.0.0` |
| `aiofiles` | `25.1.0` |
| `aiohappyeyeballs` | `2.7.1` |
| `aiohttp` | `3.14.5` |
| `aioitertools` | `0.13.0` |
| `aiosignal` | `1.4.0` |
| `aiosqlite` | `0.22.1` |
| `alembic` | `1.20.0`, `1.20.1` |
| `altair` | `6.3.0` |
| `amplitude-analytics` | `1.3.0` |
| `anndata` | `0.13.4` |
| `annotated-doc` | `0.0.5` |
| `annotated-types` | `0.8.0` |
| `annsel` | `0.1.3` |
| `anthropic` | `2.1.0` |
| `anycorn` | `0.20.1` |
| `anyio` | `4.15.1` |
| `apache-tvm-ffi` | `0.1.15.post0` |
| `app-model` | `0.5.1` |
| `appdirs` | `1.4.4` |
| `appnope` | `1.0.0` |
| `apprise` | `1.13.1` |
| `argon2-cffi` | `25.1.0` |
| `argon2-cffi-bindings` | `26.1.0` |
| `argparse` | `1.4.0` |
| `argparse-dataclass` | `2.0.0` |
| `array-api-compat` | `1.15.0` |
| `arrow` | `1.4.0` |
| `asgi-lifespan` | `2.1.0` |
| `asgiref` | `3.12.1` |
| `astor` | `0.8.1` |
| `asttokens` | `3.0.2` |
| `astunparse` | `1.6.3` |
| `async-lru` | `2.3.0` |
| `asyncpg` | `0.32.0` |
| `attrs` | `26.1.0` |
| `audioop-lts` | `0.2.2` |
| `autobahn` | `26.7.1` |
| `autograd` | `1.9.1` |
| `autograd-gamma` | `0.5.0` |
| `automat` | `25.4.16` |
| `avro` | `1.11.5` |
| `awscli` | `1.46.1` |
| `azure-common` | `1.1.28` |
| `azure-core` | `1.41.0` |
| `azure-identity` | `1.26.0` |
| `azure-mgmt-core` | `1.6.0` |
| `azure-mgmt-storage` | `20.1.0` |
| `azure-storage-blob` | `12.31.0` |

<h3 id="b">B</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `babel` | `2.18.0` |
| `batchgenerators` | `0.25.5` |
| `batchgeneratorsv2` | `0.3.6` |
| `beartype` | `0.23.1` |
| `beautifulsoup4` | `4.15.0` |
| `bidict` | `0.24.1` |
| `biopython` | `1.88` |
| `biosppy` | `2.2.4` |
| `blake3` | `1.0.11` |
| `bleach` | `6.4.0` |
| `blinker` | `1.9.0` |
| `blis` | `1.3.3` |
| `blosc` | `1.11.4` |
| `blosc2` | `4.14.1` |
| `bokeh` | `3.10.0`, `3.10.1` |
| `boto3` | `1.43.117` |
| `botocore` | `1.43.106`, `1.43.117` |
| `brotli` | `1.2.0` |
| `build` | `1.6.1` |
| `burner-redis` | `0.1.7` |

<h3 id="c">C</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `cachebox` | `5.2.3` |
| `cachetools` | `7.2.0`, `7.2.4` |
| `cachey` | `0.2.1` |
| `captum` | `0.0.1`, `0.9.0` |
| `catalogue` | `2.0.10` |
| `catboost` | `1.2.10` |
| `cbor2` | `5.9.0`, `6.1.5` |
| `certifi` | `2024.2.2`, `2026.7.22`, `2026.10.19` |
| `cffi` | `2.1.1` |
| `charset-normalizer` | `3.3.2`, `3.5.1`, `3.5.2` |
| `click` | `8.5.0` |
| `cloudpathlib` | `0.25.0`, `0.26.0` |
| `cloudpickle` | `3.1.2` |
| `cmdstanpy` | `1.3.0` |
| `colorama` | `0.4.6` |
| `colorcet` | `3.2.1` |
| `coloredlogs` | `15.0.1` |
| `colorlog` | `6.12.0` |
| `comm` | `0.2.3` |
| `commonmark` | `0.9.2` |
| `compressed-tensors` | `0.13.0` |
| `conda-inject` | `1.3.2` |
| `confection` | `1.3.3` |
| `configargparse` | `1.8.0` |
| `conllu` | `6.0.0` |
| `connected-components-3d` | `4.1.0` |
| `connection-pool` | `0.0.3` |
| `constantly` | `23.10.4` |
| `contourpy` | `1.3.2`, `1.4.0` |
| `coolname` | `5.0.0` |
| `cronsim` | `2.7` |
| `cryptography` | `50.0.1`, `50.0.2` |
| `cuda-bindings` | `13.4.4` |
| `cuda-pathfinder` | `1.8.3` |
| `cuda-toolkit` | `13.0.3`, `13.0.3.0` |
| `cupy-cuda12x` | `14.2.0` |
| `cycler` | `0.12.1` |
| `cyclopts` | `5.2.0` |
| `cymem` | `2.0.13` |
| `cython` | `3.1.8` |
| `cyvcf2` | `0.34.0` |

<h3 id="d">D</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `daphne` | `4.2.3` |
| `darts` | `0.47.0` |
| `dash` | `4.4.1` |
| `dask` | `2026.8.0` |
| `dask-image` | `2026.5.0` |
| `dataclasses` | `0.8` |
| `datasets` | `5.1.0` |
| `datashader` | `0.19.1` |
| `dateparser` | `1.4.3` |
| `debugpy` | `1.8.22` |
| `decorator` | `5.3.1` |
| `deepdiff` | `9.1.0` |
| `defusedxml` | `0.7.1` |
| `deprecated` | `1.2.18`, `3.0.0` |
| `deprecation` | `2.1.0` |
| `depyf` | `0.20.0` |
| `detect-installer` | `0.2.1` |
| `dicom2nifti` | `2.6.2` |
| `diffprivlib` | `0.6.6` |
| `dill` | `0.4.1` |
| `dipy` | `1.12.1` |
| `diskcache` | `5.6.3` |
| `distributed` | `2026.8.0` |
| `distro` | `1.9.0` |
| `dnspython` | `2.9.0` |
| `docker` | `7.2.0` |
| `docopt` | `0.6.2` |
| `docrep` | `0.3.2` |
| `docstring-parser` | `0.18.0` |
| `docutils` | `0.19`, `0.22.4` |
| `donfig` | `0.8.1.post1` |
| `dpath` | `2.2.0` |
| `duckdb` | `1.5.5`, `2.0.0` |
| `dynaconf` | `3.3.5` |
| `dynamic-network-architectures` | `0.4.4` |

<h3 id="e">E</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `ecos` | `2.0.14` |
| `einops` | `0.8.2` |
| `email-validator` | `2.3.0` |
| `et-xmlfile` | `2.0.0` |
| `evidently` | `0.7.23` |
| `exceptiongroup` | `1.3.1` |
| `executing` | `2.2.1`, `2.3.0` |

<h3 id="f">F</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `fairlearn` | `0.15.0` |
| `faker` | `40.43.0` |
| `fast-array-utils` | `1.5.1` |
| `fastapi` | `0.138.2`, `0.141.1`, `0.150.0` |
| `fastapi-cli` | `0.0.32` |
| `fastapi-cloud-cli` | `0.26.0` |
| `fastar` | `0.12.0` |
| `fastjsonschema` | `2.22.2` |
| `fhir-core` | `1.1.11` |
| `fhir-resources` | `8.3.0` |
| `filelock` | `4.0.4`, `4.2.4` |
| `flashinfer-python` | `0.6.3` |
| `flask` | `3.1.3` |
| `flatbuffers` | `25.12.19` |
| `flexcache` | `0.3` |
| `flexparser` | `0.4` |
| `flwr` | `1.41.0` |
| `fonttools` | `4.66.0`, `4.67.0` |
| `formulaic` | `1.2.2` |
| `fqdn` | `1.5.1` |
| `freetype-py` | `2.5.1` |
| `frozenlist` | `1.8.0` |
| `fsspec` | `2026.7.0`, `2026.9.0` |
| `fury` | `2.1.0` |
| `future` | `1.0.0` |

<h3 id="g">G</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `gast` | `0.7.0` |
| `geopandas` | `1.2.0` |
| `gguf` | `0.19.0` |
| `gitdb` | `4.0.12` |
| `gitpython` | `3.2.1` |
| `glfw` | `2.11.0` |
| `google-auth` | `2.62.0` |
| `google-auth-oauthlib` | `0.8.0` |
| `google-crc32c` | `1.9.0` |
| `google-pasta` | `0.2.0` |
| `gradio` | `6.28.0` |
| `gradio-client` | `2.7.1` |
| `granian` | `2.8.3` |
| `graphviz` | `0.21` |
| `great-expectations` | `1.23.2` |
| `greenlet` | `3.5.6` |
| `griffe` | `2.4.1` |
| `griffecli` | `2.4.1` |
| `griffelib` | `2.4.1` |
| `groovy` | `0.1.2` |
| `grpcio` | `1.84.0` |
| `grpcio-health-checking` | `1.81.1` |
| `grpcio-reflection` | `1.84.0` |

<h3 id="h">H</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `h11` | `0.16.0` |
| `h2` | `4.4.1` |
| `h5py` | `3.14.0`, `3.16.0` |
| `hail` | `0.2.139` |
| `heapdict` | `1.0.1` |
| `hf-gradio` | `0.4.1` |
| `hf-xet` | `1.6.0`, `1.7.0` |
| `holidays` | `0.105` |
| `hpack` | `4.2.0` |
| `hsluv` | `5.0.4`, `5.0.5` |
| `html5lib` | `1.1` |
| `httpcore` | `1.0.9` |
| `httpcore2` | `2.16.0` |
| `httptools` | `0.9.0` |
| `httpx` | `0.28.1` |
| `httpx2` | `2.16.0` |
| `httpx2-jsfetch` | `1.0` |
| `huggingface-hub` | `0.36.2`, `1.33.0`, `2.2.0` |
| `humanfriendly` | `10.0` |
| `humanize` | `4.16.0` |
| `hypercorn` | `0.18.0` |
| `hyperframe` | `6.1.0` |
| `hyperlink` | `21.0.0` |

<h3 id="i">I</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `icecream` | `2.2.0` |
| `idna` | `3.7`, `3.20` |
| `ijson` | `3.6.0` |
| `imagecodecs` | `2025.11.11`, `2026.10.10` |
| `imageio` | `2.38.1` |
| `imbalanced-learn` | `0.14.2` |
| `imgkit` | `1.2.3` |
| `immutables` | `0.21` |
| `importlib-metadata` | `9.0.1` |
| `in-n-out` | `0.2.1` |
| `incremental` | `24.11.0` |
| `inflect` | `7.6.0` |
| `iniconfig` | `2.3.0` |
| `interegular` | `0.3.3` |
| `interface-meta` | `2.0.1` |
| `ipykernel` | `7.3.0`, `7.4.0` |
| `ipython` | `9.17.1` |
| `ipython-pygments-lexers` | `1.1.1` |
| `ipywidgets` | `8.1.9` |
| `isodate` | `0.7.2` |
| `isoduration` | `20.11.0` |
| `iterative-telemetry` | `0.0.10` |
| `iterators` | `0.0.2` |
| `itsdangerous` | `2.2.0` |

<h3 id="j">J</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `janus` | `1.0.0`, `2.0.0` |
| `jaraco-functools` | `4.6.0` |
| `jedi` | `0.20.0`, `0.20.1` |
| `jinja2` | `3.1.6` |
| `jinja2-humanize-extension` | `0.4.0` |
| `jiter` | `0.17.0` |
| `jmespath` | `1.1.0` |
| `joblib` | `1.6.0` |
| `jproperties` | `2.1.2` |
| `json5` | `0.15.0` |
| `jsonpatch` | `1.36` |
| `jsonpointer` | `3.1.1`, `3.4` |
| `jsonschema` | `4.26.0` |
| `jsonschema-specifications` | `2025.9.1` |
| `jupyter` | `1.1.1` |
| `jupyter-builder` | `1.2.3` |
| `jupyter-client` | `8.10.0` |
| `jupyter-console` | `6.6.3` |
| `jupyter-core` | `5.9.1` |
| `jupyter-events` | `0.12.1` |
| `jupyter-lsp` | `2.3.1` |
| `jupyter-server` | `2.21.1` |
| `jupyter-server-terminals` | `0.5.4` |
| `jupyterlab` | `4.6.4` |
| `jupyterlab-pygments` | `0.3.0` |
| `jupyterlab-server` | `2.28.1` |
| `jupyterlab-widgets` | `3.0.17` |

<h3 id="k">K</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `keras` | `3.15.1` |
| `kiwisolver` | `1.5.1` |

<h3 id="l">L</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `lark` | `1.2.2`, `1.3.1` |
| `lazy-loader` | `0.6` |
| `legacy-api-wrap` | `1.5` |
| `libclang` | `18.1.1` |
| `lifelines` | `0.30.0`, `0.30.3` |
| `lightgbm` | `4.7.0` |
| `lightning` | `2.6.6` |
| `lightning-utilities` | `0.15.3` |
| `lime` | `0.2.0.1` |
| `linecache2` | `1.0.0` |
| `litestar` | `2.25.0` |
| `litestar-htmx` | `0.5.0` |
| `llguidance` | `1.3.0` |
| `llvmlite` | `0.36.0`, `0.44.0`, `0.49.0`, `0.50.0` |
| `lm-format-enforcer` | `0.11.3` |
| `local-migrator` | `0.1.10` |
| `locket` | `1.0.0` |
| `loguru` | `0.7.3` |
| `lxml` | `6.1.3` |

<h3 id="m">M</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `magicgui` | `0.10.2` |
| `mako` | `1.4.3` |
| `markdown` | `3.11.2` |
| `markdown-it-py` | `4.2.0` |
| `markupsafe` | `3.0.3`, `3.0.4` |
| `marshmallow` | `4.3.1` |
| `matplotlib` | `3.11.2` |
| `matplotlib-inline` | `0.2.2` |
| `matplotlib-scalebar` | `0.9.0` |
| `mcp` | `2.3.0` |
| `mcp-types` | `2.3.0` |
| `mdurl` | `0.1.2` |
| `medspacy` | `1.3.1` |
| `medspacy-quickumls` | `3.2` |
| `medspacy-unqlite` | `0.9.8` |
| `mistral-common` | `1.12.0` |
| `mistune` | `3.3.4` |
| `ml-dtypes` | `0.6.0` |
| `mock` | `5.2.0` |
| `model-hosting-container-standards` | `0.1.16` |
| `monai` | `1.6.1` |
| `more-itertools` | `11.2.1` |
| `mpmath` | `1.3.0`, `1.4.1` |
| `msal` | `1.39.0` |
| `msal-extensions` | `1.3.1` |
| `msgpack` | `1.2.2`, `1.2.3` |
| `msgspec` | `0.21.1`, `0.22.0` |
| `msrest` | `0.7.1` |
| `mudata` | `0.4.1` |
| `multidict` | `6.9.1`, `7.1.0` |
| `multipart` | `2.0.1` |
| `multipledispatch` | `1.0.0` |
| `multiprocess` | `0.70.19` |
| `multiscale-spatial-image` | `2.0.3` |
| `muon` | `0.2.0` |
| `murmurhash` | `1.0.15` |
| `mypy-extensions` | `1.1.0` |

<h3 id="n">N</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `namex` | `0.1.0` |
| `napari` | `0.9.2` |
| `napari-console` | `0.1.5` |
| `napari-plugin-engine` | `0.2.1` |
| `napari-resources` | `1.0.1` |
| `napari-svg` | `0.2.1` |
| `narwhals` | `2.26.0`, `2.27.1` |
| `natsort` | `8.4.0` |
| `nbclient` | `0.11.0` |
| `nbconvert` | `7.17.1` |
| `nbformat` | `5.11.1` |
| `nest-asyncio` | `1.6.0` |
| `nest-asyncio2` | `1.7.3`, `1.7.4` |
| `networkx` | `3.7` |
| `neurokit2` | `0.2.12` |
| `nfoursid` | `1.0.2` |
| `nibabel` | `5.4.2` |
| `ninja` | `1.13.2` |
| `nltk` | `3.10.3`, `3.10.4` |
| `nme` | `0.1.8` |
| `nmslib` | `2.1.2` |
| `nmslib-metabrainz` | `2.1.3` |
| `nnunetv2` | `2.8.1` |
| `notebook` | `7.6.3` |
| `notebook-shim` | `0.2.4` |
| `npe2` | `0.10.0` |
| `numba` | `0.53.1`, `0.61.2`, `0.67.0`, `0.68.0` |
| `numcodecs` | `0.17.0`, `0.17.1` |
| `numexpr` | `2.14.2` |
| `numpy` | `1.26.4`, `2.2.6`, `2.4.6`, `2.5.3`, `2.5.4` |
| `nvidia-cublas` | `13.1.1.3` |
| `nvidia-cublas-cu12` | `12.8.4.1` |
| `nvidia-cuda-cupti` | `13.0.85` |
| `nvidia-cuda-cupti-cu12` | `12.8.90` |
| `nvidia-cuda-nvrtc` | `13.0.88` |
| `nvidia-cuda-nvrtc-cu12` | `12.8.93` |
| `nvidia-cuda-runtime` | `13.0.96` |
| `nvidia-cuda-runtime-cu12` | `12.8.90` |
| `nvidia-cudnn-cu12` | `9.10.2.21` |
| `nvidia-cudnn-cu13` | `9.24.0.43` |
| `nvidia-cudnn-frontend` | `1.31.0` |
| `nvidia-cufft` | `12.0.0.61` |
| `nvidia-cufft-cu12` | `11.3.3.83` |
| `nvidia-cufile` | `1.15.1.6` |
| `nvidia-cufile-cu12` | `1.13.1.3` |
| `nvidia-curand` | `10.4.0.35` |
| `nvidia-curand-cu12` | `10.3.9.90` |
| `nvidia-cusolver` | `12.0.4.66` |
| `nvidia-cusolver-cu12` | `11.7.3.90` |
| `nvidia-cusparse` | `12.6.3.3` |
| `nvidia-cusparse-cu12` | `12.5.8.93` |
| `nvidia-cusparselt-cu12` | `0.7.1` |
| `nvidia-cusparselt-cu13` | `0.8.1` |
| `nvidia-cutlass-dsl` | `4.8.1` |
| `nvidia-cutlass-dsl-libs-base` | `4.8.1` |
| `nvidia-cutlass-dsl-libs-core` | `4.8.1` |
| `nvidia-cutlass-dsl-libs-cu12` | `4.8.1` |
| `nvidia-cutlass-dsl-libs-cu13` | `4.8.1` |
| `nvidia-ml-py` | `13.615.71` |
| `nvidia-nccl-cu12` | `2.27.5` |
| `nvidia-nccl-cu13` | `2.30.7`, `2.32.3` |
| `nvidia-nvjitlink` | `13.4.92` |
| `nvidia-nvjitlink-cu12` | `12.8.93` |
| `nvidia-nvshmem-cu12` | `3.3.20` |
| `nvidia-nvshmem-cu13` | `3.4.5` |
| `nvidia-nvtx` | `13.0.85` |
| `nvidia-nvtx-cu12` | `12.8.90` |

<h3 id="o">O</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `oauthlib` | `4.0.0` |
| `ome-zarr` | `0.21.0` |
| `ome-zarr-models` | `1.8.1` |
| `omnipath` | `1.0.12` |
| `opacus` | `1.6.0` |
| `openai` | `3.36.1` |
| `openai-harmony` | `0.0.8` |
| `opencv-python` | `5.0.0.93` |
| `opencv-python-headless` | `5.0.0.93` |
| `openpyxl` | `3.1.5` |
| `opentelemetry-api` | `1.45.1` |
| `opentelemetry-proto` | `1.45.1` |
| `opt-einsum` | `3.4.0` |
| `optree` | `0.20.0` |
| `optuna` | `5.0.0` |
| `orderly-set` | `5.5.0` |
| `orjson` | `3.12.0`, `3.13.0` |
| `osqp` | `1.1.3` |
| `outlines-core` | `0.2.11` |

<h3 id="p">P</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `packaging` | `25.0`, `26.3` |
| `pandas` | `2.2.2`, `2.3.3`, `3.0.6`, `3.1.0` |
| `pandas-flavor` | `0.8.1` |
| `pandocfilters` | `1.5.1` |
| `param` | `2.4.2` |
| `parsimonious` | `0.11.0` |
| `parso` | `0.8.7` |
| `partd` | `1.4.2` |
| `partial-json-parser` | `0.2.1.1.post7` |
| `pathlib-abc` | `0.5.2` |
| `pathspec` | `1.1.1` |
| `patsy` | `1.0.3` |
| `peft` | `0.21.2` |
| `pendulum` | `3.2.0`, `3.3.0` |
| `pexpect` | `4.9.0` |
| `phonenumbers` | `9.0.41` |
| `pillow` | `12.3.0`, `13.0.0` |
| `pims` | `0.7` |
| `pingouin` | `0.7.0` |
| `pint` | `0.26.2` |
| `pip` | `26.2.1`, `26.2.2` |
| `platformdirs` | `4.12.0`, `4.13.5` |
| `plotly` | `5.24.1`, `7.1.0` |
| `pluggy` | `1.6.0`, `1.7.0` |
| `polars` | `1.44.2` |
| `polars-runtime-32` | `1.44.2` |
| `polyfactory` | `3.5.0` |
| `polyxios` | `0.5.1` |
| `pooch` | `1.9.0` |
| `prefect` | `3.9.0` |
| `preshed` | `3.0.13` |
| `presidio-analyzer` | `2.2.364` |
| `priority` | `2.0.0` |
| `prometheus-client` | `0.26.0` |
| `prometheus-fastapi-instrumentator` | `8.1.0` |
| `prompt-toolkit` | `3.0.53` |
| `propcache` | `0.5.4` |
| `prophet` | `1.4.0` |
| `protobuf` | `6.33.6`, `7.36.2` |
| `psutil` | `7.2.2` |
| `psygnal` | `0.16.1` |
| `ptyprocess` | `0.7.0` |
| `pulp` | `3.3.2` |
| `pure-eval` | `0.2.4` |
| `py-cpuinfo` | `9.0.0` |
| `py-key-value-aio` | `0.4.6` |
| `py4j` | `0.10.9.9` |
| `pyarrow` | `25.0.1`, `26.0.0` |
| `pyasn1` | `0.6.4` |
| `pyasn1-modules` | `0.4.2` |
| `pybase64` | `1.5.1` |
| `pybind11` | `3.1.0` |
| `pycares` | `5.2.1` |
| `pyconify` | `0.2.1` |
| `pycountry` | `26.2.16` |
| `pycparser` | `3.0`, `3.11`, `3.12` |
| `pycryptodome` | `3.24.1` |
| `pyct` | `0.6.0` |
| `pydantic` | `2.12.5`, `2.13.5`, `2.14.1` |
| `pydantic-core` | `2.41.5`, `2.46.5`, `2.50.1` |
| `pydantic-extra-types` | `2.11.1` |
| `pydantic-settings` | `2.15.0`, `2.16.1` |
| `pydantic-zarr` | `0.10.0` |
| `pydicom` | `3.0.2` |
| `pydocket` | `0.27.0` |
| `pydub` | `0.25.1` |
| `pyfastner` | `1.0.10` |
| `pygfx` | `0.17.0` |
| `pygments` | `2.21.0` |
| `pyjwt` | `2.15.1` |
| `pykwalify` | `1.8.0` |
| `pylinalg` | `0.6.8` |
| `pynndescent` | `0.5.13`, `0.6.0` |
| `pyod` | `3.6.6` |
| `pyogrio` | `0.13.0` |
| `pyopengl` | `3.1.10` |
| `pyopenssl` | `26.4.0` |
| `pyparsing` | `3.3.3` |
| `pyproj` | `3.8.0` |
| `pyproject-hooks` | `1.3.3` |
| `pyradiomics` | `3.1.0` |
| `pyreadline3` | `3.5.6` |
| `pyrush` | `1.0.13` |
| `pysam` | `0.24.1` |
| `pysbd` | `0.3.4` |
| `pysimstring` | `1.3.0` |
| `pyspark` | `3.5.9` |
| `pysyft` | `0.0.1` |
| `pytest` | `9.1.1` |
| `python-dateutil` | `2.9.0.post0`, `3.0.0` |
| `python-dotenv` | `1.2.3`, `1.2.4` |
| `python-gdcm` | `3.2.6` |
| `python-json-logger` | `2.0.7`, `4.2.0` |
| `python-multipart` | `0.0.32` |
| `python-slugify` | `9.0.0` |
| `pytorch-lightning` | `2.6.6` |
| `pytz` | `2024.1`, `2026.4`, `2026.5` |
| `pywavelets` | `1.10.0` |
| `pywin32` | `312` |
| `pywinpty` | `3.0.5` |
| `pyyaml` | `6.0.3` |
| `pyzmq` | `27.2.0` |

<h3 id="q">Q</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `qtconsole` | `5.7.2` |
| `qtpy` | `2.4.3` |
| `quicksectx` | `0.4.1` |

<h3 id="r">R</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `rangehttpserver` | `1.4.0` |
| `ray` | `2.59.0` |
| `readchar` | `4.2.2` |
| `redis` | `8.1.0` |
| `referencing` | `0.37.0` |
| `regex` | `2026.9.10`, `2026.9.29` |
| `rendercanvas` | `2.7.2` |
| `requests` | `2.31.0`, `2.34.2` |
| `requests-file` | `3.0.1` |
| `requests-oauthlib` | `2.0.0` |
| `requests-toolbelt` | `1.0.0` |
| `retrying` | `1.4.2` |
| `rfc3339-validator` | `0.1.4` |
| `rfc3986-validator` | `0.1.1` |
| `rfc3987-syntax` | `1.1.0` |
| `rich` | `12.6.0`, `14.3.4`, `15.0.0` |
| `rich-click` | `1.9.9` |
| `rich-rst` | `2.2.0` |
| `rich-toolkit` | `0.20.6` |
| `rignore` | `0.8.1` |
| `rpds-py` | `2026.6.3`, `2026.9.1` |
| `rsa` | `4.7.2` |
| `rt-utils` | `1.2.7` |
| `ruamel-yaml` | `0.19.1` |
| `rubicon-objc` | `0.5.7` |

<h3 id="s">S</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `s3fs` | `2026.9.0` |
| `s3transfer` | `0.19.3` |
| `safehttpx` | `0.1.7` |
| `safetensors` | `0.8.0` |
| `scanpy` | `1.9.8`, `1.12.4` |
| `scikit-image` | `0.26.0` |
| `scikit-learn` | `1.9.1` |
| `scikit-survival` | `0.28.0` |
| `scipy` | `1.17.1`, `1.18.1` |
| `scispacy` | `0.2.4`, `0.6.2` |
| `scverse-misc` | `0.1.6`, `0.1.7` |
| `seaborn` | `0.13.2` |
| `semantic-version` | `2.10.0` |
| `semver` | `3.1.0` |
| `send2trash` | `2.1.0` |
| `sentence-transformers` | `6.2.0` |
| `sentencepiece` | `0.2.2` |
| `sentry-sdk` | `2.73.0` |
| `service-identity` | `26.1.0` |
| `session-info` | `1.0.1` |
| `session-info2` | `0.4.2` |
| `setproctitle` | `1.3.8` |
| `setuptools` | `80.10.2`, `81.0.0`, `84.0.0`, `84.2.1` |
| `shap` | `0.52.0`, `0.54.1` |
| `shapely` | `2.2.0` |
| `shellingham` | `1.5.4` |
| `shortuuid` | `1.0.13` |
| `simpleitk` | `2.5.6` |
| `six` | `1.16.0`, `1.17.0` |
| `sklearn-compat` | `0.1.6` |
| `slicer` | `0.0.8` |
| `slicerator` | `1.1.0` |
| `smart-open` | `7.7.1`, `8.0.1`, `8.0.4` |
| `smmap` | `5.0.3` |
| `snakemake` | `9.27.1` |
| `snakemake-interface-common` | `1.23.0` |
| `snakemake-interface-executor-plugins` | `9.4.0` |
| `snakemake-interface-logger-plugins` | `2.1.0` |
| `snakemake-interface-report-plugins` | `1.3.0` |
| `snakemake-interface-scheduler-plugins` | `2.0.2` |
| `snakemake-interface-storage-plugins` | `4.4.1` |
| `sniffio` | `1.3.1` |
| `sortedcontainers` | `2.4.0` |
| `soupsieve` | `2.10` |
| `spacy` | `3.8.16` |
| `spacy-legacy` | `3.0.12` |
| `spacy-loggers` | `1.0.5` |
| `spatial-image` | `1.2.3` |
| `spatialdata` | `0.8.0` |
| `spatialdata-plot` | `0.4.3` |
| `sqlalchemy` | `2.0.55`, `2.1.1`, `2.1.6` |
| `sqlmodel` | `0.0.37` |
| `squidpy` | `1.8.3` |
| `srsly` | `2.5.3`, `2.5.4` |
| `sse-starlette` | `3.5.0` |
| `stack-data` | `0.6.3` |
| `stanio` | `0.5.1` |
| `starlette` | `1.3.1`, `1.7.0`, `1.9.0` |
| `statsmodels` | `0.15.0` |
| `stdlib-list` | `0.12.0` |
| `superqt` | `0.9.0` |
| `supervisor` | `4.3.0` |
| `sympy` | `1.14.0` |

<h3 id="t">T</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `tabulate` | `0.10.0` |
| `tblib` | `3.2.2` |
| `tenacity` | `9.2.1` |
| `tensorflow` | `2.21.0` |
| `termcolor` | `3.3.0` |
| `terminado` | `0.18.1` |
| `text-unidecode` | `1.3` |
| `thinc` | `8.3.13` |
| `threadpoolctl` | `3.7.0` |
| `throttler` | `1.2.3` |
| `tifffile` | `2026.10.15` |
| `tiktoken` | `0.14.0` |
| `timm` | `1.0.22` |
| `tinycss2` | `1.5.1` |
| `tldextract` | `5.4.0` |
| `tokenizers` | `0.22.2`, `0.23.3` |
| `toml` | `0.10.2` |
| `tomli` | `2.5.0` |
| `tomli-w` | `1.2.0` |
| `tomlkit` | `0.14.0` |
| `toolz` | `1.2.0` |
| `torch` | `2.9.1`, `2.14.1`, `2.14.1+cu130` |
| `torchaudio` | `2.9.1` |
| `torchmetrics` | `1.9.0` |
| `torchvision` | `0.24.1` |
| `tornado` | `6.5.10`, `6.6` |
| `totalsegmentator` | `2.17.0` |
| `tqdm` | `4.70.1` |
| `traceback2` | `1.4.0` |
| `traitlets` | `5.16.1` |
| `transformers` | `4.57.6`, `5.20.2` |
| `transformnd` | `0.9.2` |
| `triton` | `3.5.1`, `3.8.0` |
| `truststore` | `0.10.5` |
| `trx-python` | `0.6` |
| `twisted` | `26.4.0` |
| `txaio` | `26.6.1` |
| `typeguard` | `4.6.0` |
| `typer` | `0.20.1`, `0.24.2`, `0.27.2`, `0.27.3` |
| `typing-extensions` | `4.16.0` |
| `typing-inspect` | `0.9.0` |
| `typing-inspection` | `0.4.4` |
| `tzdata` | `2024.1`, `2026.4`, `2026.5` |
| `tzlocal` | `5.4.4`, `5.4.5` |

<h3 id="u">U</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `u-msgpack-python` | `2.8.0` |
| `uharfbuzz` | `0.56.3` |
| `ujson` | `6.0.0` |
| `umap-learn` | `0.5.12` |
| `uncalled-for` | `0.4.1` |
| `unidecode` | `1.4.0` |
| `unittest2` | `1.1.0` |
| `universal-pathlib` | `0.3.10` |
| `uri-template` | `1.3.0` |
| `urllib3` | `2.2.1`, `2.8.0` |
| `uuid6` | `2025.0.1` |
| `uvicorn` | `0.49.0`, `0.54.0` |
| `uvloop` | `0.21.0`, `0.23.0` |

<h3 id="v">V</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `validators` | `0.36.0` |
| `vispy` | `0.17.0` |
| `vllm` | `0.16.0` |

<h3 id="w">W</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `wasabi` | `1.1.3` |
| `watchdog` | `6.0.0` |
| `watchfiles` | `1.3.0` |
| `wcwidth` | `0.9.1`, `0.9.3` |
| `weasel` | `1.0.0` |
| `webcolors` | `25.10.0` |
| `webencodings` | `0.6.1` |
| `websocket-client` | `1.9.2` |
| `websockets` | `16.1.1`, `17.3` |
| `werkzeug` | `3.1.9` |
| `wgpu` | `0.32.0` |
| `wheel` | `0.48.0` |
| `whenever` | `0.10.5` |
| `widgetsnbextension` | `4.0.16` |
| `win32-setctime` | `1.2.0` |
| `wrapt` | `1.17.3`, `2.5.0`, `2.5.1` |
| `wsproto` | `1.3.2` |

<h3 id="x">X</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `xarray` | `2026.7.0`, `2026.9.0` |
| `xarray-dataclass` | `3.0.0` |
| `xarray-spatial` | `0.10.17` |
| `xgboost` | `3.4.1` |
| `xgrammar` | `0.1.29` |
| `xlrd` | `2.0.2` |
| `xlsxwriter` | `3.2.9` |
| `xmltodict` | `1.0.4` |
| `xvfbwrapper` | `0.2.35` |
| `xxhash` | `4.0.2` |
| `xyzservices` | `2026.9.1` |

<h3 id="y">Y</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `yacs` | `0.1.8` |
| `yamllint` | `1.38.0` |
| `yarl` | `1.25.1` |
| `yte` | `1.9.4` |

<h3 id="z">Z</h3>

| Package Name | Available Version(s) |
| :--- | :--- |
| `zarr` | `3.4.0`, `3.4.1` |
| `zict` | `3.0.0` |
| `zipp` | `4.1.1` |
| `zope-interface` | `8.6` |
| `zstandard` | `0.25.0` |

---

## Changelog

### Snapshot 20

**Capabilities Enabled:**

- Released 408 package versions (315 new packages, 70 version updates) to the Glasgow TRE production PyPI mirror.
- Deep Learning & LLM Foundation Ecosystem: PyTorch suite (`torch`, `torchvision`, `torchaudio`, `torchmetrics`, `pytorch-lightning`, `lightning`), TensorFlow & Keras (`tensorflow`, `keras`, `flwr`), Hugging Face & LLM tooling (`transformers`, `tokenizers`, `datasets`, `peft`, `sentence-transformers`, `sentencepiece`, `tiktoken`, `vllm`, `outlines-core`, `compressed-tensors`, `gguf`, `anthropic`, `openai`, `mistral-common`).
- Distributed Computing & Workflow Orchestration: Scalable multi-node execution and pipeline management with Ray (`ray`), Dask (`dask`, `distributed`), PySpark (`pyspark`), Snakemake (`snakemake`), and Prefect (`prefect`).
- Spatial Omics & Multi-dimensional Biomedical Imaging: Multi-scale spatial omics, imaging, and single-cell analysis (`napari` and GUI ecosystem, `monai`, `spatialdata`, `spatialdata-plot`, `squidpy`, `mudata`, `muon`, `ome-zarr`, `pims`, `cyvcf2`, `pysam`, `hail`).
- Geospatial Analytics & High-Performance Visualization: Spatial geometry analysis and large-scale raster rendering (`geopandas`, `shapely`, `pyproj`, `pyogrio`, `datashader`, `vispy`, `colorcet`, `xarray-spatial`).
- Advanced Machine Learning, Model Explainability & Responsible AI: Gradient boosting frameworks (`xgboost`, `lightgbm`, `catboost`), imbalance handling (`imbalanced-learn`), interpretability (`lime`, `captum`), model monitoring (`evidently`), and differential privacy/PII governance (`diffprivlib`, `opacus`, `presidio-analyzer`, `pysyft`).
- Cloud Object Storage & Enterprise SDKs: Cloud connectors and high-throughput transfer libraries for Azure (`azure-identity`, `azure-storage-blob`, `azure-mgmt-storage`), AWS S3 (`boto3`, `botocore`, `s3fs`, `s3transfer`), and Redis (`redis`, `burner-redis`).
- GPU Runtimes, Accelerated Kernels & Modern Services: NVIDIA CUDA 12 ecosystem runtime libraries (`nvidia-*-cu12`, `cupy-cuda12x`), CUDA 13 CUTLASS, accelerated inference kernels (`flashinfer-python`, `xgrammar`), Model Context Protocol (`mcp`), gRPC (`grpcio`), high-performance web frameworks (`fastapi-cli`, `litestar`, `websockets`, `uvloop`), and modern data modeling (`sqlmodel`).

### Snapshot 6

**Capabilities Enabled:**

- Added 99 new Python packages including a newer version of some existing packages. 

- Medical image analysis, segmentation, and feature extraction tooling ([TotalSegmentator](https://github.com/wasserth/TotalSegmentator) `totalsegmentator`, [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) `nnunetv2`, `dynamic-network-architectures`, `pyradiomics`, `dicom2nifti`, `rt-utils`, `dipy`, `python-gdcm`, `trx-python`, `scikit-image`).
- NVIDIA CUDA 13 ecosystem libraries and GPU compute runtimes (`nvidia-cuda-runtime`, `nvidia-cudnn-cu13`, `nvidia-cublas`, `cuda-toolkit`, `cuda-bindings`, `triton`, `timm`, `safetensors`, `einops`).
- Scientific 3D rendering and GPU computing frameworks ([PyGFX](https://pygfx.readthedocs.io/) `pygfx`, [wgpu](https://wgpu-py.readthedocs.io/) `wgpu`, `rendercanvas`, `pylinalg`, `fury`, `glfw`, `freetype-py`).
- Asynchronous HTTP and networking stack (`aiohttp`, `yarl`, `propcache`, `aiohappyeyeballs`, `aiosignal`, `frozenlist`, `httpcore2`, `httpx2`).

**Packages Added:**

| Package Name | Available Version(s) |
| :--- | :--- |
| `acvl-utils` | `0.2.6` |
| `aiohappyeyeballs` | `2.7.1` |
| `aiohttp` | `3.14.5` |
| `aiosignal` | `1.4.0` |
| `argparse` | `1.4.0` |
| `batchgenerators` | `0.25.5` |
| `batchgeneratorsv2` | `0.3.6` |
| `blosc` | `1.11.4` |
| `blosc2` | `4.14.1` |
| `cachebox` | `5.2.3` |
| `certifi` | `2026.10.19` |
| `connected-components-3d` | `4.1.0` |
| `cuda-bindings` | `13.4.4` |
| `cuda-pathfinder` | `1.8.3` |
| `cuda-toolkit` | `13.0.3` |
| `dataclasses` | `0.8` |
| `deepdiff` | `9.1.0` |
| `dicom2nifti` | `2.6.2` |
| `dipy` | `1.12.1` |
| `docopt` | `0.6.2` |
| `dynamic-network-architectures` | `0.4.4` |
| `einops` | `0.8.2` |
| `filelock` | `4.2.4` |
| `fonttools` | `4.67.0` |
| `freetype-py` | `2.5.1` |
| `frozenlist` | `1.8.0` |
| `fury` | `2.1.0` |
| `future` | `1.0.0` |
| `glfw` | `2.11.0` |
| `graphviz` | `0.21` |
| `hf-xet` | `1.7.0` |
| `hsluv` | `5.0.4` |
| `httpcore2` | `2.16.0` |
| `httpx2` | `2.16.0` |
| `httpx2-jsfetch` | `1.0` |
| `huggingface-hub` | `2.2.0` |
| `imagecodecs` | `2026.10.10` |
| `imageio` | `2.38.1` |
| `imgkit` | `1.2.3` |
| `lazy-loader` | `0.6` |
| `linecache2` | `1.0.0` |
| `mpmath` | `1.3.0` |
| `multidict` | `7.1.0` |
| `narwhals` | `2.27.1` |
| `nnunetv2` | `2.8.1` |
| `numpy` | `2.5.4` |
| `nvidia-cublas` | `13.1.1.3` |
| `nvidia-cuda-cupti` | `13.0.85` |
| `nvidia-cuda-nvrtc` | `13.0.88` |
| `nvidia-cuda-runtime` | `13.0.96` |
| `nvidia-cudnn-cu13` | `9.24.0.43` |
| `nvidia-cufft` | `12.0.0.61` |
| `nvidia-cufile` | `1.15.1.6` |
| `nvidia-curand` | `10.4.0.35` |
| `nvidia-cusolver` | `12.0.4.66` |
| `nvidia-cusparse` | `12.6.3.3` |
| `nvidia-cusparselt-cu13` | `0.8.1` |
| `nvidia-nccl-cu13` | `2.30.7` |
| `nvidia-nvjitlink` | `13.4.92` |
| `nvidia-nvshmem-cu13` | `3.4.5` |
| `nvidia-nvtx` | `13.0.85` |
| `orderly-set` | `5.5.0` |
| `pillow` | `13.0.0` |
| `pip` | `26.2.2` |
| `polyxios` | `0.5.1` |
| `propcache` | `0.5.4` |
| `pyarrow` | `26.0.0` |
| `pycparser` | `3.11` |
| `pydantic` | `2.14.1` |
| `pydantic-core` | `2.50.1` |
| `pygfx` | `0.17.0` |
| `pykwalify` | `1.8.0` |
| `pylinalg` | `0.6.8` |
| `pyradiomics` | `3.1.0` |
| `python-gdcm` | `3.2.6` |
| `rendercanvas` | `2.7.2` |
| `requests-toolbelt` | `1.0.0` |
| `rt-utils` | `1.2.7` |
| `rubicon-objc` | `0.5.7` |
| `safetensors` | `0.8.0` |
| `scikit-image` | `0.26.0` |
| `setuptools` | `84.2.1` |
| `sympy` | `1.14.0` |
| `tifffile` | `2026.10.15` |
| `timm` | `1.0.22` |
| `totalsegmentator` | `2.17.0` |
| `traceback2` | `1.4.0` |
| `triton` | `3.8.0` |
| `truststore` | `0.10.5` |
| `trx-python` | `0.6` |
| `typer` | `0.27.3` |
| `tzdata` | `2026.5` |
| `uharfbuzz` | `0.56.3` |
| `unittest2` | `1.1.0` |
| `wgpu` | `0.32.0` |
| `xmltodict` | `1.0.4` |
| `xvfbwrapper` | `0.2.35` |
| `yacs` | `0.1.8` |
| `yarl` | `1.25.1` |

### Snapshot 5

**Capabilities Enabled:**

- Libraries  open/read/write Microsoft Excel Spreadsheet (`openpyxl`, `xlsxwriter`, `et-xmlfile`)
- Added [Dash](https://plotly.com/dash/) framework.
    - If you're not familiar with it, RealPython has an excellent tutorial on their [Develop Data Visualization Interfaces in Python With Dash](https://realpython.com/python-dash/) article.

**Packages Added:**

| Package Name | Available Version(s) |
| :--- | :--- |
| `blinker` | `1.9.0` |
| `charset-normalizer` | `3.5.2` |
| `dash` | `4.4.1` |
| `et-xmlfile` | `2.0.0` |
| `flask` | `3.1.3` |
| `importlib-metadata` | `9.0.1` |
| `itsdangerous` | `2.2.0` |
| `janus` | `2.0.0` |
| `markupsafe` | `3.0.4` |
| `nest-asyncio` | `1.6.0` |
| `openpyxl` | `3.1.5` |
| `plotly` | `7.1.0` |
| `retrying` | `1.4.2` |
| `werkzeug` | `3.1.9` |
| `xlsxwriter` | `3.2.9` |
| `zipp` | `4.1.1` |
