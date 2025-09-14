This repository holds the code examples and notebooks for the book "Hands-On Data Analysis with Pandas (2nd ed.)".

Quick orientation
- Primary artifacts are Jupyter notebooks under `ch_01`..`ch_12`. Code modules used by examples live alongside those chapters (for example `ch_04/window_calc.py`, `ch_06/viz.py`).
- Exercises and solutions are under `solutions/` and many chapters include a `data/` subfolder with CSV/fixtures.
- Visual assets are in `visual-aids/` and `_img/` and sometimes referenced directly in notebooks (relative paths are used).

Environment & setup
- This project targets Python 3.8 (see `environment.yml` and `README.md`). Prefer creating a conda env from `environment.yml` on Windows:

    conda env create --file environment.yml

- CI builds use `.github/workflows/env-checks.yml` which creates a `book_env` conda environment and runs `python ch_01/check_environment.py` to validate the install. Keep edits to `environment.yml` minimal and mirror CI assumptions.
- Dependencies include some git-based packages and a local path (`./visual-aids`) in `requirements.txt` and `environment.yml`. When running `pip install -r requirements.txt` expect git installs to be fetched; network access is required.

Notebooks and code patterns
- Notebooks are the source of truth for examples and exercises. Code intended for reuse is placed in `.py` files in the chapter folders (e.g., `ch_06/viz.py`, `ch_04/window_calc.py`). When adding reusable helpers, follow this convention: put them next to the chapter that uses them and import them with relative imports in notebooks/cells.
- Data files are referenced with relative paths (e.g., `ch_02/data/`), so tests/runs should use the repository root as CWD or change directories into the chapter folder before executing notebooks.

Common tasks for an AI coding agent
- When asked to modify examples, update both the notebook cell and any accompanying `.py` helpers. Use the pattern already present: small helper modules + notebook demonstration.
- Preserve relative paths in notebooks and tests. If you add new datasets, place them under the chapter's `data/` folder and add a short note in the notebook's markdown cell documenting the source.
- If you change package versions in `environment.yml` or `requirements.txt`, also update `README.md` to keep instructions consistent and consider running the CI workflow locally (create a conda env and run `python ch_01/check_environment.py`).

Testing, validation, and CI
- There is no unit test framework preconfigured. CI focuses on environment reproducibility (`.github/workflows/env-checks.yml`). For quick validation, run:

    conda env create --file environment.yml
    conda activate book_env
    python ch_01/check_environment.py

- For notebook-level checks, open the target notebook in JupyterLab and run cells, or use `nbconvert`/`nbclient` to programmatically execute and validate outputs if needed.

Project-specific gotchas
- The project pins older package versions (pandas==1.2.0, scikit-learn==0.23.2, etc.). Avoid upgrading packages unless you verify notebooks still run: examples rely on API behavior from those versions.
- Some dependencies are installed via git (`stefmolin/*@2nd_edition`). These repositories may be required to reproduce examples; ensure network access in CI and local runs.
- Many examples expect the repository root as the working directory; do not change CWD in notebooks except in a cell that documents why it is necessary.

When editing notebooks
- Keep outputs minimal when committing changes: clear large matplotlib images unless they illustrate a fixed example. Prefer updating or adding markdown that explains changes.
- If you modify code across both a `.py` helper and a notebook, update the notebook cell that imports the helper so the order of execution remains correct.

Files to reference when making changes
- `README.md` — environment/setup and high-level guidance
- `environment.yml`, `requirements.txt` — canonical dependency sources
- `.github/workflows/env-checks.yml` — CI behavior to mirror locally
- `ch_01/check_environment.py` — the canonical environment validation script
- Example helpers: `ch_04/window_calc.py`, `ch_06/viz.py`

If uncertain, ask the maintainer for:
- preferred Python patch-level (3.8.x) and whether it's acceptable to bump a pinned version
- whether new helpers should be added to an existing chapter or put in a shared `tools/` directory

Please ask for clarification if any path, dependency, or notebook behavior is unclear.
