---
name: evaluate-model
description: Evaluate a trained regression model and generate a performance report. Use when asked to evaluate, assess, or report on model performance.
---

When evaluating a regression model, follow these steps:

1. **Load the trained model** from the `output/` directory (joblib format)
2. **Load test data** and generate predictions
3. **Compute regression metrics**:
   - RMSE (Root Mean Squared Error)
   - MAE (Mean Absolute Error)
   - R-squared (R2 score)
   - MAPE (Mean Absolute Percentage Error)
4. **Generate a residual plot** (predicted vs actual, residuals vs predicted)
5. **Create a feature importance chart** (bar chart of XGBoost feature importances)
6. **Save all plots** to the `output/` directory
7. **Write an evaluation report** to `output/evaluation_report.md` with:
   - A metrics summary table
   - Key findings and observations
   - Recommendations for improvement

Use polars for data handling. Log all metrics using the project's logging format.
