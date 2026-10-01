# Python Runtime & Package Management

## Overview & Management

- **Management Tool**: Astral [`uv`](https://github.com/astral-sh/uv) provides runtime and environment management in user space without requiring administrator rights (`C:\Program Files\uv` on Windows).
- **Binary Upstream**: Standalone Python builds sourced from [`astral-sh/python-build-standalone`](https://github.com/astral-sh/python-build-standalone) and hosted on internal Dell PowerScale S3 storage.
- **Supported Versions**: Python `3.12.0` through `3.14.13` (including beta and pre-release/RC builds) on Windows (`x86_64-pc-windows-msvc`) and Linux (`x86_64-unknown-linux-gnu`).
- **Runtime Isolation**: Enforced via `python-preference = "only-managed"` in `C:\ProgramData\uv\uv.toml` so workstations only use approved internal mirrored runtimes.
- **Package Index**: Air-gapped PyPI mirror hosted on `repo.hlz.glasgowtre.ac.uk`. Pre-configured `C:\ProgramData\pip\pip.ini` (Windows) and `/etc/pip.conf` (Linux) allow standard `pip` and Jupyter `%pip` commands to resolve dependencies automatically.

---

## How-To: Common Workflows

### Install a Python Runtime

```powershell
# List available runtimes on the internal mirror
uv python list

# Install target version (multiple versions can coexist)
uv python install 3.12.13
```

### Initialize a Project & Virtual Environment

```powershell
mkdir C:\Users\<username>\Documents\analysis_project
cd C:\Users\<username>\Documents\analysis_project

# Initialize project config (pyproject.toml)
uv init

# Create virtual environment pinned to a specific Python version
uv venv --python 3.12
```

### Install Packages

- **Using `uv`** (recorded in `uv.lock`):
  ```powershell
  uv add pandas polars jupyterlab
  uv pip install -r requirements.txt
  ```
- **Inside JupyterLab notebooks** (uses pre-configured `pip.ini`):
  ```python
  %pip install <package-name>
  ```

### Run Workloads

```powershell
# Execute a script inside the project environment
uv run script.py

# Launch JupyterLab within the project environment
uv run jupyter lab

# Run ad-hoc script with ephemeral packages without altering project dependencies
uv run --python 3.12 --with pandas script.py
```

### IDE Integration

- **VS Code & PyCharm**: Automatically detect virtual environments located in `.venv`.
- **Interpreter Path**: Select `.venv\Scripts\python.exe` (Windows) or `.venv/bin/python` (Linux).

---

## Reference: Available PyPI Packages

Inventory of **301 approved packages** available on the Glasgow TRE production mirror (Snapshot 3).

### Jump to Letter

[A](#a) | [B](#b) | [C](#c) | [D](#d) | [E](#e) | [F](#f) | [G](#g) | [H](#h) | [I](#i) | [J](#j) | [K](#k) | [L](#l) | [M](#m) | [N](#n) | [O](#o) | [P](#p) | [Q](#q) | [R](#r) | [S](#s) | [T](#t) | [U](#u) | [W](#w) | [X](#x) | [Y](#y) | [Z](#z)

---

### A

| Package Name | Available Version(s) |
| :--- | :--- |
| `aiofiles` | `25.1.0` |
| `alembic` | `1.20.0` |
| `altair` | `6.3.0` |
| `anndata` | `0.13.4` |
| `annotated-doc` | `0.0.5` |
| `annotated-types` | `0.8.0` |
| `anycorn` | `0.20.1` |
| `anyio` | `4.15.1` |
| `appnope` | `1.0.0` |
| `argon2-cffi` | `25.1.0` |
| `argon2-cffi-bindings` | `26.1.0` |
| `array-api-compat` | `1.15.0` |
| `arrow` | `1.4.0` |
| `asgiref` | `3.12.1` |
| `asttokens` | `3.0.2` |
| `async-lru` | `2.3.0` |
| `attrs` | `26.1.0` |
| `audioop-lts` | `0.2.2` |
| `autobahn` | `26.7.1` |
| `autograd` | `1.9.1` |
| `autograd-gamma` | `0.5.0` |
| `automat` | `25.4.16` |
| `awscli` | `1.46.1` |

### B

| Package Name | Available Version(s) |
| :--- | :--- |
| `babel` | `2.18.0` |
| `beautifulsoup4` | `4.15.0` |
| `bidict` | `0.24.1` |
| `biopython` | `1.88` |
| `biosppy` | `2.2.4` |
| `bleach` | `6.4.0` |
| `blis` | `1.3.3` |
| `bokeh` | `3.10.0` |
| `brotli` | `1.2.0` |

### C

| Package Name | Available Version(s) |
| :--- | :--- |
| `cachetools` | `7.2.0` |
| `catalogue` | `2.0.10` |
| `cbor2` | `5.9.0` |
| `certifi` | `2024.2.2`, `2026.7.22` |
| `cffi` | `2.1.1` |
| `charset-normalizer` | `3.3.2`, `3.5.1` |
| `click` | `8.5.0` |
| `cloudpathlib` | `0.25.0` |
| `cloudpickle` | `3.1.2` |
| `cmdstanpy` | `1.3.0` |
| `colorama` | `0.4.6` |
| `colorlog` | `6.12.0` |
| `comm` | `0.2.3` |
| `confection` | `1.3.3` |
| `conllu` | `6.0.0` |
| `constantly` | `23.10.4` |
| `contourpy` | `1.4.0` |
| `cryptography` | `50.0.1` |
| `cycler` | `0.12.1` |
| `cymem` | `2.0.13` |
| `cython` | `3.1.8` |

### D

| Package Name | Available Version(s) |
| :--- | :--- |
| `daphne` | `4.2.3` |
| `darts` | `0.47.0` |
| `debugpy` | `1.8.22` |
| `defusedxml` | `0.7.1` |
| `docutils` | `0.19` |
| `donfig` | `0.8.1.post1` |
| `duckdb` | `1.5.5` |

### E

| Package Name | Available Version(s) |
| :--- | :--- |
| `ecos` | `2.0.14` |
| `executing` | `2.2.1` |

### F

| Package Name | Available Version(s) |
| :--- | :--- |
| `fast-array-utils` | `1.5.1` |
| `fastapi` | `0.141.1` |
| `fastjsonschema` | `2.22.2` |
| `fhir-core` | `1.1.11` |
| `fhir-resources` | `8.3.0` |
| `filelock` | `4.0.4` |
| `fonttools` | `4.66.0` |
| `formulaic` | `1.2.2` |
| `fqdn` | `1.5.1` |
| `fsspec` | `2026.9.0` |

### G

| Package Name | Available Version(s) |
| :--- | :--- |
| `google-crc32c` | `1.9.0` |
| `gradio` | `6.28.0` |
| `gradio-client` | `2.7.1` |
| `granian` | `2.8.3` |
| `great-expectations` | `1.23.2` |
| `groovy` | `0.1.2` |

### H

| Package Name | Available Version(s) |
| :--- | :--- |
| `h11` | `0.16.0` |
| `h2` | `4.4.1` |
| `h5py` | `3.16.0` |
| `hf-gradio` | `0.4.1` |
| `hf-xet` | `1.6.0` |
| `holidays` | `0.105` |
| `hpack` | `4.2.0` |
| `html5lib` | `1.1` |
| `httpcore` | `1.0.9` |
| `httpx` | `0.28.1` |
| `huggingface-hub` | `1.33.0` |
| `hypercorn` | `0.18.0` |
| `hyperframe` | `6.1.0` |
| `hyperlink` | `21.0.0` |

### I

| Package Name | Available Version(s) |
| :--- | :--- |
| `icecream` | `2.2.0` |
| `idna` | `3.7`, `3.20` |
| `incremental` | `24.11.0` |
| `iniconfig` | `2.3.0` |
| `interface-meta` | `2.0.1` |
| `ipykernel` | `7.3.0` |
| `ipython` | `9.17.1` |
| `ipython-pygments-lexers` | `1.1.1` |
| `ipywidgets` | `8.1.9` |
| `isoduration` | `20.11.0` |

### J

| Package Name | Available Version(s) |
| :--- | :--- |
| `jedi` | `0.20.0` |
| `jinja2` | `3.1.6` |
| `jmespath` | `1.1.0` |
| `joblib` | `1.6.0` |
| `json5` | `0.15.0` |
| `jsonpointer` | `3.1.1` |
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

### K

| Package Name | Available Version(s) |
| :--- | :--- |
| `kiwisolver` | `1.5.1` |

### L

| Package Name | Available Version(s) |
| :--- | :--- |
| `lark` | `1.3.1` |
| `legacy-api-wrap` | `1.5` |
| `lifelines` | `0.30.0` |
| `llvmlite` | `0.36.0`, `0.49.0` |
| `local-migrator` | `0.1.10` |
| `loguru` | `0.7.3` |
| `lxml` | `6.1.3` |

### M

| Package Name | Available Version(s) |
| :--- | :--- |
| `mako` | `1.4.3` |
| `markdown-it-py` | `4.2.0` |
| `markupsafe` | `3.0.3` |
| `marshmallow` | `4.3.1` |
| `matplotlib` | `3.11.2` |
| `matplotlib-inline` | `0.2.2` |
| `mdurl` | `0.1.2` |
| `medspacy` | `1.3.1` |
| `medspacy-quickumls` | `3.2` |
| `medspacy-unqlite` | `0.9.8` |
| `mistune` | `3.3.4` |
| `mock` | `5.2.0` |
| `msgpack` | `1.2.2` |
| `msgspec` | `0.21.1` |
| `murmurhash` | `1.0.15` |

### N

| Package Name | Available Version(s) |
| :--- | :--- |
| `narwhals` | `2.26.0` |
| `natsort` | `8.4.0` |
| `nbclient` | `0.11.0` |
| `nbconvert` | `7.17.1` |
| `nbformat` | `5.11.1` |
| `nest-asyncio2` | `1.7.3` |
| `networkx` | `3.7` |
| `neurokit2` | `0.2.12` |
| `nfoursid` | `1.0.2` |
| `nibabel` | `5.4.2` |
| `nltk` | `3.10.3` |
| `nme` | `0.1.8` |
| `nmslib` | `2.1.2` |
| `notebook` | `7.6.3` |
| `notebook-shim` | `0.2.4` |
| `numba` | `0.53.1`, `0.67.0` |
| `numcodecs` | `0.17.0` |
| `numexpr` | `2.14.2` |
| `numpy` | `1.26.4`, `2.5.3` |

### O

| Package Name | Available Version(s) |
| :--- | :--- |
| `opencv-python` | `5.0.0.93` |
| `optuna` | `5.0.0` |
| `orjson` | `3.12.0` |
| `osqp` | `1.1.3` |

### P

| Package Name | Available Version(s) |
| :--- | :--- |
| `packaging` | `26.3` |
| `pandas` | `2.2.2`, `3.0.6` |
| `pandocfilters` | `1.5.1` |
| `parso` | `0.8.7` |
| `pathspec` | `1.1.1` |
| `patsy` | `1.0.3` |
| `pendulum` | `3.2.0` |
| `pexpect` | `4.9.0` |
| `pillow` | `12.3.0` |
| `pip` | `26.2.1` |
| `platformdirs` | `4.12.0` |
| `pluggy` | `1.6.0` |
| `polars` | `1.44.2` |
| `polars-runtime-32` | `1.44.2` |
| `preshed` | `3.0.13` |
| `priority` | `2.0.0` |
| `prometheus-client` | `0.26.0` |
| `prompt-toolkit` | `3.0.53` |
| `prophet` | `1.4.0` |
| `psutil` | `7.2.2` |
| `ptyprocess` | `0.7.0` |
| `pure-eval` | `0.2.4` |
| `pyarrow` | `25.0.1` |
| `pyasn1` | `0.6.4` |
| `pybind11` | `3.1.0` |
| `pycparser` | `3.0` |
| `pydantic` | `2.13.5` |
| `pydantic-core` | `2.46.5` |
| `pydantic-settings` | `2.15.0` |
| `pydicom` | `3.0.2` |
| `pydub` | `0.25.1` |
| `pyfastner` | `1.0.10` |
| `pygments` | `2.21.0` |
| `pynndescent` | `0.5.13`, `0.6.0` |
| `pyod` | `3.6.6` |
| `pyopenssl` | `26.4.0` |
| `pyparsing` | `3.3.3` |
| `pyrush` | `1.0.13` |
| `pysbd` | `0.3.4` |
| `pysimstring` | `1.3.0` |
| `pytest` | `9.1.1` |
| `python-dateutil` | `2.9.0.post0` |
| `python-dotenv` | `1.2.3` |
| `python-json-logger` | `4.2.0` |
| `python-multipart` | `0.0.32` |
| `pytz` | `2024.1`, `2026.4` |
| `pywavelets` | `1.10.0` |
| `pywinpty` | `3.0.5` |
| `pyyaml` | `6.0.3` |
| `pyzmq` | `27.2.0` |

### Q

| Package Name | Available Version(s) |
| :--- | :--- |
| `quicksectx` | `0.4.1` |

### R

| Package Name | Available Version(s) |
| :--- | :--- |
| `referencing` | `0.37.0` |
| `regex` | `2026.9.10` |
| `requests` | `2.31.0`, `2.34.2` |
| `rfc3339-validator` | `0.1.4` |
| `rfc3986-validator` | `0.1.1` |
| `rfc3987-syntax` | `1.1.0` |
| `rich` | `15.0.0` |
| `rich-click` | `1.9.9` |
| `rpds-py` | `2026.6.3` |
| `rsa` | `4.7.2` |
| `ruamel-yaml` | `0.19.1` |

### S

| Package Name | Available Version(s) |
| :--- | :--- |
| `safehttpx` | `0.1.7` |
| `scanpy` | `1.9.8`, `1.12.4` |
| `scikit-learn` | `1.9.1` |
| `scikit-survival` | `0.28.0` |
| `scipy` | `1.18.1` |
| `scispacy` | `0.2.4` |
| `scverse-misc` | `0.1.6` |
| `seaborn` | `0.13.2` |
| `semantic-version` | `2.10.0` |
| `send2trash` | `2.1.0` |
| `service-identity` | `26.1.0` |
| `session-info` | `1.0.1` |
| `session-info2` | `0.4.2` |
| `setuptools` | `84.0.0` |
| `shap` | `0.52.0` |
| `shellingham` | `1.5.4` |
| `shortuuid` | `1.0.13` |
| `simpleitk` | `2.5.6` |
| `six` | `1.16.0`, `1.17.0` |
| `slicer` | `0.0.8` |
| `smart-open` | `8.0.1` |
| `sniffio` | `1.3.1` |
| `soupsieve` | `2.10` |
| `spacy` | `3.8.16` |
| `spacy-legacy` | `3.0.12` |
| `spacy-loggers` | `1.0.5` |
| `sqlalchemy` | `2.1.1` |
| `srsly` | `2.5.3` |
| `stack-data` | `0.6.3` |
| `stanio` | `0.5.1` |
| `starlette` | `1.7.0` |
| `statsmodels` | `0.15.0` |
| `stdlib-list` | `0.12.0` |

### T

| Package Name | Available Version(s) |
| :--- | :--- |
| `terminado` | `0.18.1` |
| `thinc` | `8.3.13` |
| `threadpoolctl` | `3.7.0` |
| `tinycss2` | `1.5.1` |
| `tomlkit` | `0.14.0` |
| `tornado` | `6.5.10` |
| `tqdm` | `4.70.1` |
| `traitlets` | `5.16.1` |
| `twisted` | `26.4.0` |
| `txaio` | `26.6.1` |
| `typer` | `0.27.2` |
| `typing-extensions` | `4.16.0` |
| `typing-inspection` | `0.4.4` |
| `tzdata` | `2024.1`, `2026.4` |
| `tzlocal` | `5.4.4` |

### U

| Package Name | Available Version(s) |
| :--- | :--- |
| `u-msgpack-python` | `2.8.0` |
| `ujson` | `6.0.0` |
| `umap-learn` | `0.5.12` |
| `unidecode` | `1.4.0` |
| `uri-template` | `1.3.0` |
| `urllib3` | `2.2.1`, `2.8.0` |
| `uvicorn` | `0.54.0` |

### W

| Package Name | Available Version(s) |
| :--- | :--- |
| `wasabi` | `1.1.3` |
| `wcwidth` | `0.9.1` |
| `weasel` | `1.0.0` |
| `webcolors` | `25.10.0` |
| `webencodings` | `0.6.1` |
| `websocket-client` | `1.9.2` |
| `widgetsnbextension` | `4.0.16` |
| `win32-setctime` | `1.2.0` |
| `wrapt` | `2.5.0` |
| `wsproto` | `1.3.2` |

### X

| Package Name | Available Version(s) |
| :--- | :--- |
| `xarray` | `2026.7.0` |
| `xyzservices` | `2026.9.1` |

### Y

| Package Name | Available Version(s) |
| :--- | :--- |
| `yamllint` | `1.38.0` |

### Z

| Package Name | Available Version(s) |
| :--- | :--- |
| `zarr` | `3.4.0` |
| `zope-interface` | `8.6` |

---

### Requesting Additional Packages

- **Contact**: Submit a package request ticket to your Glasgow TRE representative.
- **Information Needed**: Library name, requested version, and analytical rationale.
- **Deployment**: Approved packages are synced to the internal mirror during scheduled maintenance updates.
