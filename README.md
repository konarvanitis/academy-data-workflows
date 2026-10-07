# academy-data-workflows
This repository is used for the Academy course on Data Workflows.

It contains a hands-on notebook (`workflows_notebook.ipynb`) showcasing Cognite Data Fusion Data Workflows with the Cognite Python SDK.

https://cognite-docs.readthedocs-hosted.com/projects/cognite-sdk-python/en/latest/

## Getting Started

### Prerequisites

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) (recommended) or pip

### 1. Clone the repository

```bash
git clone https://github.com/konarvanitis/academy-data-workflows
```

### 2. Install dependencies

We recommend using uv to manage your Python virtual environment:

```bash
uv sync
```

This installs the dependencies defined in `pyproject.toml` and creates a virtual environment in the project folder.

### 3. Run the notebook

Open the repo in your IDE (e.g., VS Code) and open `workflows_notebook.ipynb`.

> **Note:** You may need to select the uv virtual environment (`.venv`) as your kernel.

### 4. Set up clean notebook diffs (one-time, per clone)

Jupyter stamps your local kernel name and Python version into each notebook's metadata every time you run it, which shows up as noisy, unrelated diffs in `git status`/`git diff`. Run this once after cloning to strip that noise before it ever reaches git:

```bash
uv run nbstripout --install --attributes .gitattributes
git config filter.nbstripout.extrakeys "metadata.kernelspec metadata.language_info.version metadata.vscode"
```

This registers a git filter that strips outputs, execution counts, and the kernel/version metadata from notebooks whenever git reads or diffs them — your local `.ipynb` files on disk are untouched, so notebooks still run and show outputs normally in your editor.

## Alternative: pip installation

If you prefer not to use uv, you can install the dependencies directly with pip:

```bash
pip install "cognite-sdk[pandas]" networkx matplotlib notebook
```

## Troubleshooting

### WSL: interactive login fails with `gio: ... Operation not supported`

On WSL, Python's interactive OAuth login (the authentication cell at the top of the notebook) tries to open your default browser and can fail with an error like:

```
gio: https://login.microsoftonline.com/...: Operation not supported
```

This happens because WSL has no browser handler registered for the login URL. Copy the URL from the error message and paste it directly into your Windows browser — the login redirect to `localhost` will reach the notebook correctly thanks to WSL2's automatic localhost port forwarding.
