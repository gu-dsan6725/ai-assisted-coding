# Run EDA Workflow

Perform exploratory data analysis on the California Housing dataset.

## Steps

1. Load the California Housing dataset using `sklearn.datasets.fetch_california_housing`
2. Convert to a polars DataFrame
3. Compute summary statistics (mean, median, std, min, max) for each feature
4. Check for missing values and report findings
5. Generate distribution histograms for each feature using matplotlib
6. Create a correlation matrix heatmap using seaborn
7. Identify outliers using the IQR method
8. Save all plots to the `output/` directory
9. Log a summary of findings

## Requirements

- Use polars (not pandas) for all data manipulation
- Follow the coding standards in `.agent/rules/code-style-guide.md`
- Save the EDA script as `01_eda.py`
- After writing the file, run `uv run ruff check --fix` and `uv run python -m py_compile`
