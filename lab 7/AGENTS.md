# AGENTS.md

Repository guidance for coding agents working in this project.

## 1) Repository Snapshot

- Project type: educational machine learning notebooks (not a packaged Python app).
- Primary assets:
  - `01-Logistic Regression.ipynb`
  - `02-Logistic Regression Assignment.ipynb`
  - `titanic_train.csv`, `titanic_test.csv`, `advertising.csv`
- Local environment folder exists: `env/` (virtual environment).
- No `pyproject.toml`, `setup.py`, `requirements*.txt`, `Makefile`, or CI config detected.
- No standalone `tests/` directory detected.

## 2) Build / Run / Lint / Test Commands

Because this repo is notebook-first, there is no formal build pipeline.

### Environment setup

- Activate local venv (macOS/zsh):
  - `source env/bin/activate`
- Confirm Python:
  - `python --version`
- Install missing packages only if needed by new work:
  - `python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter`

### Run notebooks

- Start Jupyter Notebook UI:
  - `jupyter notebook`
- Start JupyterLab:
  - `jupyter lab`

### Execute a notebook end-to-end (CLI)

- Execute Titanic notebook in place:
  - `jupyter nbconvert --to notebook --execute --inplace "01-Logistic Regression.ipynb"`
- Execute assignment notebook in place:
  - `jupyter nbconvert --to notebook --execute --inplace "02-Logistic Regression Assignment.ipynb"`

### Linting / formatting (not configured, recommended defaults)

- There is no enforced linter/formatter config in-repo.
- If you add `.py` modules or scripts, use:
  - `python -m ruff check .`
  - `python -m black .`

### Testing status

- No test framework is currently configured in this repository.
- There are no existing automated unit/integration tests to run.

### Single-test command (important)

- If tests are added with `pytest`, run one test with:
  - `python -m pytest path/to/test_file.py::test_name`
- Run one test class method with:
  - `python -m pytest path/to/test_file.py::TestClass::test_name`
- Run tests matching a keyword:
  - `python -m pytest -k "keyword"`

## 3) Code Style Guidelines for This Repo

These rules reflect existing notebook conventions plus safe defaults for new code.

### Language and structure

- Use Python for all new logic.
- Keep exploratory work in notebooks unless asked to extract scripts/modules.
- Prefer small, focused helper functions over long monolithic cells.

### Imports

- Place imports at the top of notebook/script sections.
- Group imports in this order: standard library, third-party, local.
- Use common aliases already used in the repo:
  - `import pandas as pd`
  - `import numpy as np`
  - `import matplotlib.pyplot as plt`
  - `import seaborn as sns`
- Avoid wildcard imports.
- Remove unused imports before finishing.

### Formatting

- Follow PEP 8 when writing Python code.
- Prefer 88-char lines when practical (Black-compatible).
- Use spaces around operators and after commas.
- Keep chained dataframe operations readable (use intermediate variables if needed).

### Types and annotations

- Existing notebooks are mostly untyped; type hints are encouraged for new helper functions.
- Add annotations when a function is reused or non-trivial.
- Example style:
  - `def impute_age(row: pd.Series) -> float:`

### Naming conventions

- `snake_case` for variables/functions.
- `PascalCase` for classes.
- Constants in `UPPER_SNAKE_CASE`.
- Dataframe naming:
  - Use descriptive names (`train_df`, `test_df`, `ad_data`) over single-letter names.
- Model variables should be explicit (`log_model`, `predictions`, `X_train`, `y_test`).

### Data handling and ML conventions

- Keep train/test split logic explicit and reproducible.
- Always set `random_state` where supported.
- Avoid data leakage (fit transforms only on training data).
- Record assumptions for cleaning/imputation near the code.
- Prefer vectorized pandas operations to row-by-row loops.

### Error handling

- Validate expected columns before model training.
- Fail early with clear messages for missing files/columns.
- Catch exceptions only when you can add context or recovery.
- Do not suppress warnings/errors broadly without justification.

### Notebook-specific practices

- Keep cell execution order logical and reproducible from top to bottom.
- Avoid hidden state dependencies between distant cells.
- If you modify data in place, make that explicit in the same cell.
- Keep plots deterministic where possible (set seeds for sampled visuals).
- Clear noisy outputs before final handoff unless outputs are instructional.

### Documentation and comments

- Prefer short markdown cells explaining intent over heavy inline comments.
- Add comments only for non-obvious logic.
- Document why a transformation is needed, not just what it does.

## 4) File and Path Conventions

- Use repository-relative paths in code:
  - `pd.read_csv("titanic_train.csv")`
- Do not hardcode absolute local machine paths.
- Preserve original dataset filenames unless explicitly requested.

## 5) Dependency and Version Notes

- Notebook metadata indicates Python 3 with ipykernel.
- Observed notebook metadata versions differ (`3.11.x` and `3.13.x` in files).
- Agents should avoid relying on version-fragile APIs unless necessary.

## 6) Cursor / Copilot Rules

- Checked `.cursor/rules/`: not present.
- Checked `.cursorrules`: not present.
- Checked `.github/copilot-instructions.md`: not present.
- Therefore, no additional Cursor/Copilot instruction files apply right now.

## 7) Agent Working Agreement

- Prefer minimal, targeted edits.
- Do not rewrite large notebook outputs unless required.
- Preserve educational narrative and markdown prompts in assignment notebook.
- If adding tests or tooling, document commands in this file.
- If the repo gains formal tooling (pytest/ruff/black/CI), update this file immediately.
