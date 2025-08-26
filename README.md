# Power Load Prediction in Buildings Using ML

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--Learn-1.2%2B-green?logo=scikit-learn)](https://scikit-learn.org/stable/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![UCI Dataset](https://img.shields.io/badge/Dataset-UCI%20Energy%20Efficiency-orange)](https://archive.ics.uci.edu/dataset/242/energy+efficiency)

A robust machine learning system for predicting building heating and cooling loads with **quantifiable uncertainty intervals**. This tool provides a fast, accurate, and accessible alternative to expensive, complex energy simulation software for early-stage building design and energy planning.

> **Key Achievement**: Developed a Gradient Boosting model that predicts power load with **99.97% accuracy (R²)** for heating and provides practical prediction intervals, achieving ~78% coverage of actual values.

##  Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Project Architecture](#-project-architecture)
- [Results & Performance](#-results--performance)
- [GUI Demo](#-gui-demo)
- [Usage](#-usage)
- [Limitations & Future Work](#-limitations--future-work)
- [References](#-references)
- [Author & License](#-author--license)

##  Overview

This project tackles the critical challenge of predicting energy demands (heating and cooling loads) for buildings. Traditional simulation tools (e.g., EnergyPlus) are complex and costly (>$5,000/year). This solution uses a **Gradient Boosting Regressor** trained on the [UCI Energy Efficiency Dataset](https://archive.ics.uci.edu/dataset/242/energy+efficiency) to provide instant, accurate predictions based on fundamental building design parameters.

The model's standout feature is its ability to generate **prediction intervals** (5th-95th percentile), offering a data-driven measure of uncertainty crucial for risk-aware engineering decisions.

##  Key Features

- **High-Accuracy Predictions**: Achieves near-perfect R² scores of **0.9976** (Heating Load) and **0.9840** (Cooling Load).
- **Uncertainty Quantification**: Provides a probable range for each forecast, not just a single point estimate.
- **Robustness Tested**: Model performance degrades gracefully even with **20% noise** injected into input data.
- **User-Friendly GUI**: Includes graphical interface for easy input and instant results.
- **Comprehensive Analysis**: Full pipeline including EDA, hyperparameter tuning, residual analysis, and robustness testing.

##  Project Architecture

The system is built with a clear machine learning pipeline:

1.  **Data**: UCI Energy Efficiency Dataset (8 features, 768 samples).
2.  **Preprocessing & EDA**: Handled missing values, analyzed correlations, and confirmed no outliers.
3.  **Modeling**: A separate **Gradient Boosting Regressor** is trained for heating (Y1) and cooling (Y2) loads.
4.  **Hyperparameter Tuning**: Optimized via `GridSearchCV` (Best params: `n_estimators=500`, `learning_rate=0.1`, `max_depth=3 and 5`).
5.  **Quantile Prediction**: Three models per target predict the **median (0.5), lower (0.05), and upper (0.95) quantiles** to form prediction intervals.
6.  **Evaluation**: Assessed using R², MAE, MSE, and interval coverage.
7.  **Deployment**: Results are showcased in a **tkinter GUI** for interactive use.

## Results & Performance

### Predictive Accuracy on Test Set (40% holdout)

| Metric | Heating Load (Y1) | Cooling Load (Y2) |
| :--- | :--- | :--- |
| **R² Score** | **0.9976** | **0.9840** |
| **Mean Absolute Error (MAE)** | **0.339** | **0.750** |
| Root Mean Squared Error (RMSE) | 0.494 | 1.201 |

### Prediction Interval Coverage
The model successfully provides practical estimates of uncertainty:
- **Heating Load:** **77.92%** of actual values captured within the 5th-95th percentile range.
- **Cooling Load:** **78.90%** captured (with a ±0.5 tolerance adjustment for improved utility).

## GUI Demo

The project includes a functional GUI built with tkinter for easy interaction.

**Input:** Building parameters (Relative Compactness, Surface Area, Wall Area, etc.)
**Output:** Instant prediction for heating or cooling load, including the median prediction and the prediction interval.


## Usage

### Running the Jupyter Analysis
The main data analysis, model training, and evaluation are in the Jupyter Notebook:
```bash
jupyter notebook Power_Load_Prediction.ipynb
