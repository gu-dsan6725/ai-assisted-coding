# Train Model Workflow

Train an XGBoost regression model on the California Housing dataset.

## Prerequisites

Run the EDA and feature engineering steps first to generate the train/test splits.

## Steps

1. Load the prepared train/test splits from `output/` (parquet files)
2. Train an XGBoost regressor with these parameters:
   - n_estimators: 200
   - max_depth: 6
   - learning_rate: 0.1
   - random_state: 42
3. Generate predictions on the test set
4. Compute evaluation metrics: RMSE, MAE, R-squared, MAPE
5. Create a residual plot (predicted vs actual, residuals vs predicted)
6. Create a feature importance bar chart
7. Save the trained model as `output/xgboost_model.joblib`
8. Write an evaluation report to `output/evaluation_report.md`

## Requirements

- Use polars for data loading
- Follow the coding standards in `.agent/rules/code-style-guide.md`
- Save the training script as `03_xgboost_model.py`
- After writing the file, run `uv run ruff check --fix` and `uv run python -m py_compile`
