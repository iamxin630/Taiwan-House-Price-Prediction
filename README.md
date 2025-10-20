
# House Price Prediction Model - NYCU IAII ML 2025 Regression

## Project Overview

This project focuses on building a **house price prediction model** for the Taiwan real estate market using **machine learning** techniques. It leverages **XGBoost regression** combined with **advanced feature engineering** to accurately predict total house prices based on real estate transaction data.

## Project Goals

- Predict total house prices in the Taiwan real estate market  
- Identify key factors influencing property prices  
- Provide a stable and accurate price prediction model  
- Assist in real estate decision-making and investment analysis

## Dataset

### Input Data
- `train-v2.xlsx`: Training dataset  
- `valid-v2.xlsx`: Validation dataset  
- `test-reindex-test-v2.1.xlsx`: Test dataset

### Output
- `final_house_price_predictions.csv`: Final prediction results

## Core Functions

### 1. Data Cleaning
- **Outlier handling**: Detect and remove invalid or corrupted price records  
- **Date processing**: Extract year and month from transaction dates  
- **Floor standardization**: Convert Chinese floor descriptions to numeric values  
- **Data integrity check**: Ensure completeness of critical fields

### 2. Advanced Feature Engineering

#### Basic Features
- Location: County, municipality flags  
- Area: Land, building, and parking area combinations  
- Floor: Floor ratio, top/bottom floor flags, basement detection  
- Transaction: Parking availability, number of transactions

#### Derived Features
- High-correlation combo features: Total floors × building area (r = 0.6715)  
- Parking features: Parking count, parking area combinations (r > 0.58)  
- Area categories: Mini / Small / Medium / Large / Luxury  
- Floor categories: Basement / Low / Mid / High / Super-high floors  
- Luxury index: Composite score from area, floor, and parking features

#### Target Encoding
- Price level encoding: Convert categorical features to mean price values  
- Bayesian smoothing: Prevent overfitting in target encoding  
- Cross encoding: Location × area, building × parking  
- Price variability features: Capture price dispersion across categories

## Model Architecture

### XGBoost Regressor
```python
XGBRegressor(
    n_estimators=2500,
    max_depth=12,
    learning_rate=0.04,
    subsample=0.85,
    colsample_bytree=0.85,
    reg_alpha=0.1,
    reg_lambda=1.2,
    tree_method='gpu_hist'
)
````

### Feature Selection

* Intelligent feature importance ranking
* Automatically selects the top 30 most impactful features
* Uses XGBoost feature importance for ranking

## Model Performance

### Evaluation Metrics

* R² Score: Variance explained by the model
* RMSE: Root Mean Squared Error (TWD)
* MAE: Mean Absolute Error (TWD)
* MAPE: Mean Absolute Percentage Error (%)

### Expected Results

* R² on validation set > 0.85
* Explains over 85% of price variability
* Produces stable and accurate predictions

## Installation and Usage

### Environment Setup

```bash
pip install -r requirements.txt
```

### Steps to Run

1. Prepare data and place dataset files in the project root directory
2. Run the notebook in Jupyter and execute all cells in order
3. Check `final_house_price_predictions.csv` for output results

```bash
jupyter notebook new.ipynb
```

### Notebook Flow

1. Cell 1 – Library installation & imports
2. Cell 2 – Data loading
3. Cell 3 – Data cleaning
4. Cell 4 – Feature engineering
5. Cell 5 – Model training
6. Cell 6 – Model evaluation
7. Cell 7 – Result export

## Feature Description

### Original Features (Partial)

* Land transfer area (m²)
* Building transfer area (m²)
* Parking transfer area (m²)
* Floor information
* Total number of floors
* Building type
* Primary material

### Engineered Features

* Total floors × building area (most important combination)
* Parking value index = number of parking spaces × parking area
* Luxury index = composite feature from multiple dimensions
* Location-area price encoding
* Floor value coefficient

## Model Explainability

### Top Feature Importance

1. Total floors × area (correlation: 0.6715)
2. Parking features (correlation: ~0.59)
3. Building area (correlation: 0.4694)
4. Number of buildings (correlation: 0.3793)
5. Price-level encoded features

### Business Value

* Property valuation: Provide objective market price reference
* Investment decision support: Evaluate potential property value
* Market analysis: Identify key drivers of property prices
* Risk assessment: Detect pricing anomalies

## Project Structure

```
nycu-iaii-ml-2025-regression/
├── new.ipynb                           # Main notebook
├── README.md                           # Project documentation
├── requirements.txt                    # Python dependencies
├── config.yaml                         # Config file
├── report.md                           # Technical report
├── train-v2.xlsx                       # Training data
├── valid-v2.xlsx                       # Validation data
├── test-reindex-test-v2.1.xlsx         # Test data
└── final_house_price_predictions.csv   # Output predictions
```

## Experimental Results

### Feature Engineering Impact

* Basic features: R² ≈ 70–75%
* Advanced combo features: +10–15% R²
* Target encoding: +5–8% R²

### Model Comparison

| Model              | R² Score |
| ------------------ | -------- |
| Random Forest      | ~0.75    |
| XGBoost (basic)    | ~0.82    |
| XGBoost (advanced) | >0.85    |

## Custom Configuration

Edit `config.yaml` to adjust parameters:

```yaml
model:
  n_estimators: 2500
  max_depth: 12
  learning_rate: 0.04

feature_selection:
  top_k_features: 30
  selection_method: "xgboost_importance"
```

## Notes

1. All personal data has been anonymized
2. GPU acceleration is recommended for faster training
3. Minimum memory requirement: 8GB RAM
4. Estimated training time: 10–15 minutes

## Contribution Guidelines

1. Fork the repository
2. Create a new feature branch
3. Commit your changes
4. Submit a Pull Request

## License

This project is for academic and research use only. Commercial use is strictly prohibited.

## Contact

For questions or suggestions, please contact the project maintainers.

---

**Last Updated:** October 4, 2025
**Version:** 1.0.0
**Status:** Stable Release

```

