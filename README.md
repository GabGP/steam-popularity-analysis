# What makes a Steam game popular?

Linear regression project for the Operations Research 2 course (Investigación de Operaciones 2). Using 100k+ Steam games, it predicts a game's popularity (number of reviews, on a log scale) and interprets the factors associated with it.

The whole analysis is in [`Steam_Popularity_Analysis.ipynb`](Steam_Popularity_Analysis.ipynb). It covers data cleaning, correlation analysis, variable selection (backward and forward), train/test validation, the final model's equation and coefficient interpretation, and a comparison with extra models. The notebook is written in Spanish.

| Model | R² (test) |
|---|---|
| Linear regression (OLS, 41 variables) | 0.488 |
| Gradient Boosting | 0.624 |
| Kumo Tabular (NVIDIA) | 0.681 |

## Data

[Steam Games Dataset](https://www.kaggle.com/datasets/fronkongames/steam-games-dataset) by Martin Bustos Roman (Kaggle, version 55). It isn't included in the repository: the notebook downloads it automatically with `kagglehub`.

## Installation

Requires [uv](https://docs.astral.sh/uv/getting-started/installation/), which also installs Python 3.12.

```bash
git clone <repository-url>
cd <repository-folder>
uv sync
uv run jupyter lab
```

Then open `Steam_Popularity_Analysis.ipynb` and run all cells. You can also use VS Code by selecting `.venv` as the kernel.

### Section 8.3 (optional): Kumo Tabular

Needs an NVIDIA GPU with a driver that supports CUDA 13. This installs PyTorch with CUDA and the Kumo package:

```bash
uv sync --group kumo
```

Always include `--group kumo` when syncing: a plain `uv sync` uninstalls PyTorch. Without a GPU, the rest of the notebook works the same and only that section is left out. The first run downloads the model weights from Hugging Face.

## Notes

- Notebook outputs are stripped before each commit with `nbstripout` (in the `dev` group), so you need to run it to see tables and plots. To enable it in a fresh clone: `uv run nbstripout --install`.
- `pyproject.toml` sets `system-certs = true` because on some networks uv can't verify PyPI's certificates with its bundled ones.
