# FinRL-Trading Workflow Pure Replication

This repository contains a rigorous, pure replication of the `FinRL-Trading` automated quantitative workflow for the CSIE 2103 Neural Networks course at National Yunlin University of Science and Technology (NYUST).

## Project Overview
- **Objective**: 1:1 structural replication of the paper's rolling machine learning stock selection and target weight rebalancing pipeline.
- **Data & Feature Engineering**: Due to the proprietary paywall of the original FMP API, this project utilizes open-source `yfinance` daily data for the full S&P 500 universe and engineers real-time technical momentum/volatility features (`ret_1m`, `volatility_3m`) as an alternative.
- **Replication Insight**: Re-implementing the framework with real-time momentum features successfully reduced the maximum drawdown to -33.29% (compared to the paper's reported -55.15% which suffered from trailing fundamental accounting data) and pushed the Sharpe Ratio to 1.02.

## Environment & Requirements
- **Language**: Python 3.10+
- **Core Dependencies**: `lightgbm`, `scikit-learn`, `pandas`, `yfinance`, `bt`, `requests`

## How to Run
1. Clone this repository or download the Jupyter notebook.
2. Install all required dependencies via pip:
   ```bash
   pip install yfinance pandas numpy lightgbm scikit-learn bt requests
   
3.Open FinRL_Full_selection.ipynb and run all cells sequentially:

  Cell 1: Programmatically scrapes the complete S&P 500 ticker list from Wikipedia (with 403-forbidden bypass headers) and builds the historical database.
  
  Cell 2: Resolves core framework bugs (missing loggers, uncommitted functions, date alignment alignment) and applies rolling data downsampling to prevent Out-Of-Memory (OOM) errors during LightGBM cross-validation.
  
  Cell 3: Executes the high-precision backtesting calendar (2020-04-30 to 2025-07-31) using the bt vectorization engine under a strict quarterly rebalancing frequency.
