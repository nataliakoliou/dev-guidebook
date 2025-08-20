# GitHub Pages PyPI Repository

This guide explains how to use GitHub Pages to host a PyPI-compatible package index for custom Python packages, allowing you to install them directly via pip without using the official PyPI server.

### 1. Create Your Python Package

Inside your main repository, e.g., `kobe4ml`, create a Python package folder such as `torch_loader`.

The structure should follow standard Python packaging practices, e.g., using `pyproject.toml` or `setup.py`.

- `pyproject.toml` contains package metadata and build system information.

- `torch_loader/` contains the actual Python code.

```bash
kobe4ml/
│
├── pyproject.toml
├── torch_loader/
│   ├── __init__.py
│   ├── loader.py
│   └── utils.py
└── ...
```

This package can later be installed via pip from your GitHub Pages PyPI index.

### 2. Prepare GitHub Pages Structure

Inside the same repository, create a folder `docs/`. Inside `docs/`, create folders for each package you want to host. Replace underscores `_` with dashes `-` in folder names, because PyPI naming conventions (PEP 503) require normalized names with dashes.

- `docs/` is the folder that GitHub Pages will serve.
- Each package folder contains an `index.html` pointing to the package source.
- Naming normalization ensures pip can find and install your packages correctly.

```bash
docs/
├── index.html
├── torch-loader/
│   └── index.html
└── ...
```

### 3. Create the Root Index for Packages

The root index `docs/index.html` lists all available packages and provides installation instructions:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>PyTorch Loader Repository</title>
    <style>
      body {
        font-family: "Source Sans Pro", "Trebuchet MS", "Lucida Grande", "Bitstream Vera Sans", "Helvetica Neue", sans-serif;
        margin: 0px;
      }
      h1 {
        background-color: rgba(130,174,182,1);
        font-size: 24px;
        color: rgba(4,38,45,1);
        padding: 20px;
      }  
      .explanation {
        background-color: rgba(215,226,241,1);
        font-size: 14px;
        color: rgba(4,38,45,1);
        padding: 20px;
      }
      div.package {
        font-size: 16px;
        color: rgba(79,108,142,1);
        border-bottom: 5px solid rgba(215,227,241,1);
        padding: 20px;
        width: 100%;
      }    
    </style>
  </head>
  <body>
    <h1>PyTorch Loader: PyPI-Compatible Repository</h1>
    <section class="explanation">
      <p>This is a custom PyPI-compatible package index for a PyTorch data loader package.</p>
      <p>You can install the package using:</p>
      <pre><code>pip install torch_loader --extra-index-url https://yourusername.github.io/yourrepo/</code></pre>
    </section>

    <div class="package">
      <a href="torch-loader/">torch_loader</a>
    </div>
  </body>
</html>
```

### 4. Create the Package Index

Inside each package folder, create an `index.html` pointing to the package source.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Links for torch_loader</title>
  </head>
  <body>
    <h1>Links for torch_loader</h1>
    <a href="git+https://github.com/kobe-benchmarking/kobe4ml.git#egg=torch_loader-0.34" data-requires-python=">=3.9">
      torch_loader-0.34
    </a><br/>
  </body>
</html>
```

#### With a specific branch:

Add `@branchname` after the repository URL. Example for `torch_loader` on branch `phase1`:

```html
<a href="git+https://github.com/kobe-benchmarking/kobe4ml.git@phase1#egg=torch_loader-0.34" data-requires-python=">=3.9">
  torch_loader-0.34
</a>
```

#### With a subdirectory:

If your package is inside a subfolder in the repo, add `&subdirectory=subfolder/path`. Example for `torch_loader` in `loaders/torch_loader` on branch `phase1`:

```html
<a href="git+https://github.com/kobe-benchmarking/kobe4ml.git@phase1#egg=torch_loader-0.34&subdirectory=loaders/torch_loader" data-requires-python=">=3.9">
  torch_loader-0.34
</a>
```

The simple case above assumes the package is at the root of the repo and on the default branch.

### 5. Push to GitHub Pages

Go to `Settings → Pages` in your repository. Select the branch e.g., `main` and folder `/docs` as the source. Save changes; GitHub will provide your Pages URL.

Commit and push your changes:

```bash
git add docs
git commit -m "Add PyPI-compatible GitHub Pages index"
git push origin main
```

Your packages are now accessible via the GitHub Pages URL: https://kobe-benchmarking.github.io/kobe4ml/.

### 6. Install the Package via Pip

From any Python environment (virtualenv or Conda):

```bash
pip install torch_loader --extra-index-url https://kobe-benchmarking.github.io/kobe4ml/
```

## References

(1) [How to use GitHub as a PyPI server](https://medium.com/@cuddlyburger/how-to-use-github-as-a-pypi-server-1c3b0d07db2): Step-by-step guide for hosting Python packages on GitHub Pages. 

(2) [PEP 503 – Simple Repository API](https://peps.python.org/pep-0503/): Python standard for PyPI-compatible indexes.

(3) [pip install documentation](https://pip.pypa.io/en/stable/cli/pip_install/): Official pip guide.