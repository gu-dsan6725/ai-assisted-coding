---
name: analyze-data
description: Perform exploratory data analysis on the California Housing dataset. Use when asked to explore, profile, or analyze the dataset.
---

When performing EDA on the California Housing dataset, follow these steps:

1. **Load the dataset** using `sklearn.datasets.fetch_california_housing` and convert to a polars DataFrame
2. **Compute summary statistics** including mean, median, std, min, max for each feature
3. **Check for missing values** and report any found
4. **Generate distribution plots** for each feature using matplotlib histograms
5. **Create a correlation matrix** heatmap using seaborn
6. **Identify outliers** using IQR method and log the count per feature
7. **Save all plots** to the `output/` directory
8. **Log a summary** of findings using the project's logging format

Use polars (not pandas) for all data manipulation. Follow the coding standards in CLAUDE.md.
