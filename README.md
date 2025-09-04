# Forecasting Sticker Sales

This repository contains a Jupyter notebook (`forecasting-sticker-sales.ipynb`) for analyzing and forecasting daily sticker sales across multiple countries, stores, and product types. The notebook is designed for a Kaggle-like competition (based on the Playground Series S5E1 dataset structure, though themed around fictional sticker products). It includes exploratory data analysis (EDA), missing value imputation, feature engineering, model training using Random Forest, and generating predictions for a test set.

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Requirements](#requirements)
- [Usage](#usage)
- [Notebook Structure](#notebook-structure)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Overview
The goal is to predict the number of stickers sold (`num_sold`) based on features like date, country, store, and product. The dataset has missing values in `num_sold` (about 3.85%), primarily for the "Holographic Goose" product in certain countries and stores. The notebook imputes these missing values using a Random Forest Regressor, engineers features (e.g., one-hot encoding for categories, date components like month/quarter/day-of-week), and trains a final model to generate submission predictions.

Key highlights:
- Handles time-series data from 2010-01-01 to 2016-12-31 (train) and 2017-01-01 onward (test).
- Focuses on products like "Holographic Goose", "Kaggle", "Kaggle Tiers", "Kerneler", and "Kerneler Dark Mode".
- Countries: Canada, Finland, Italy, Kenya, Norway, Singapore.
- Stores: Discount Stickers, Stickers for Less, Premium Sticker Mart.

## Dataset
The data is loaded from CSV files (assumed to be in a Kaggle environment):
- `train.csv`: 230,130 rows, 6 columns (`id`, `date`, `country`, `store`, `product`, `num_sold`).
- `test.csv`: Similar structure without `num_sold`.

Key insights from EDA:
- No duplicates.
- 8,871 missing values in `num_sold`, scattered (not consecutive).
- Most missing for "Holographic Goose" in Canada/Kenya's Discount Stickers.
- Sales vary by country (e.g., Norway has highest totals), store, and product.

If running locally, download the dataset from [Kaggle Playground Series S5E1](https://www.kaggle.com/competitions/playground-series-s5e1/data) or replace paths accordingly.

## Requirements
- Python 3.10+
- Libraries (install via `pip install -r requirements.txt`):
  ```
  numpy
  pandas
  matplotlib
  scikit-learn
  ```

Example `requirements.txt`:
```
numpy==1.26.4
pandas==2.2.2
matplotlib==3.9.2
scikit-learn==1.5.1
```

## Usage
1. Clone the repository:
   ```
   git clone https://github.com/your-username/forecasting-sticker-sales.git
   cd forecasting-sticker-sales
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Run the notebook:
   - Open `forecasting-sticker-sales.ipynb` in Jupyter Notebook or JupyterLab.
   - Execute cells sequentially.
   - The notebook generates `submission.csv` for predictions on the test set.

If adapting for Kaggle:
- Upload the notebook to Kaggle and run it in their environment (data paths are set for `/kaggle/input/`).

## Notebook Structure
1. **Data Loading & Initial Inspection**: Load train/test CSVs, check shape, head, info, describe, duplicates, and nulls.
2. **Missing Value Analysis**: Identify patterns (e.g., gaps by date, country/store/product). No consecutive gaps found.
3. **EDA & Visualizations**: Grouped sales summaries, feature importance plots (via Random Forest).
4. **Missing Value Imputation**: Train a Random Forest on non-missing data to predict and fill missing `num_sold`.
5. **Feature Engineering**: 
   - Parse dates (month, quarter, day-of-week).
   - One-hot encode categorical variables (country, store, product).
   - Add a 'Type' feature (binary, possibly for holidays/special days).
6. **Model Training**: Random Forest Regressor on filled train data.
7. **Prediction & Submission**: Predict on test set and save `submission.csv`.
8. **Feature Importance**: Visualize key predictors (e.g., country/store differences).

## Results
- Missing values filled with RF predictions.
- Model: Random Forest Regressor (default params).
- Output: `submission.csv` with `id` and predicted `num_sold`.
- Feature Importance: Highlights like country (e.g., Norway), store premiums, and product types as top influencers.

For competition scoring, submit `submission.csv` to Kaggle.

## Contributing
Feel free to fork, open issues, or submit pull requests for improvements (e.g., better models like Prophet/XGBoost for time-series, hyperparameter tuning).

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
