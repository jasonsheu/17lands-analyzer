# 17lands Analyzer

A Jupyter-based tool for tracking and visualizing Magic: The Gathering card performance data from [17lands.com](https://www.17lands.com) over time. Currently configured for the **Secrets of Strixhaven** limited format.

## What It Does

17lands publishes daily card rating exports with metrics like win rates, pick order, and impact stats. This tool loads multiple days of exports and lets you:

- **Track a single card** — plot any metric over time with an interactive dropdown
- **Snapshot the field** — scatter plot of all cards by GIH WR vs. ALSA for the latest day
- **Compare cards** — side-by-side metric comparison for up to 8 cards
- **Find biggest movers** — identify cards that changed the most between first and last dates
- **Browse the data** — sortable table of the latest ratings

## Setup

Requires Python 3.13.

### With uv (recommended)

[`uv`](https://github.com/astral-sh/uv) handles the virtual environment and dependency installation in one step:

```bash
git clone https://github.com/jasonsheu/17lands-analyzer.git
cd 17lands-analyzer
uv sync
```

### Without uv

Use the standard library `venv` module and `pip`:

```bash
git clone https://github.com/jasonsheu/17lands-analyzer.git
cd 17lands-analyzer
python -m venv .venv
```

Activate the environment:

- **macOS / Linux:** `source .venv/bin/activate`
- **Windows (cmd):** `.venv\Scripts\activate.bat`
- **Windows (PowerShell):** `.venv\Scripts\Activate.ps1`

Then install dependencies:

```bash
pip install ipywidgets jupyterlab nbformat numpy pandas plotly scikit-learn scipy seaborn
```

## Usage

### 1. Add data

Download card rating CSVs from [17lands.com/card_ratings](https://www.17lands.com/card_ratings) and place them in the `data/` directory. Files must follow the naming convention:

```
data/card-ratings-YYYY-MM-DD.csv
```

### 2. Open the notebook

With uv:

```bash
uv run jupyter lab strixhaven_analysis.ipynb
```

Without uv (activate your virtual environment first):

```bash
jupyter lab strixhaven_analysis.ipynb
```

Or open `strixhaven_analysis.ipynb` directly in VS Code with the Jupyter extension.

### 3. Run all cells

The notebook loads all files in `data/` automatically and renders interactive widgets for each visualization section.

## Key Metrics

| Metric | Description |
|--------|-------------|
| **GIH WR** | Games In Hand Win Rate — win rate when the card was in hand at any point |
| **OH WR** | Opening Hand Win Rate — win rate when drawn in the opening hand |
| **GD WR** | Game Decided Win Rate — win rate when the card decided the game |
| **GNS WR** | Games Not Seen Win Rate — win rate when the card was never drawn |
| **IIH** | Improvement In Hand — percentage point difference between GIH WR and GNS WR |
| **ALSA** | Average Last Seen At — how late in the draft the card is typically seen |
| **ATA** | Average Taken At — average pick number when the card is taken |

## Project Structure

```
17lands-analyzer/
├── data/                        # Card rating CSVs (not committed)
├── output/                      # Generated plots
├── strixhaven_analysis.ipynb    # Main analysis notebook
├── main.py                      # Stub entry point
└── pyproject.toml               # Project metadata and dependencies
```

## Dependencies

- [pandas](https://pandas.pydata.org/) — data loading and manipulation
- [plotly](https://plotly.com/python/) — interactive visualizations
- [ipywidgets](https://ipywidgets.readthedocs.io/) — notebook UI controls
- [scipy](https://scipy.org/) / [scikit-learn](https://scikit-learn.org/) — statistical utilities
