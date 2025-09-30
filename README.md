# Electric Vehicle Range Prediction – Washington State

This project aims to develop a robust predictive model for estimating the electric driving range of newly registered Electric Vehicles (EVs) in Washington State, leveraging detailed registration data provided by the Washington State Department of Licensing.

## Dataset

The dataset contains comprehensive records of all registered EVs in Washington, including the following features:

- **County**
- **City**
- **Postal Code**
- **Model Year**
- **Make**
- **Model**
- **Electric Vehicle Type** (BEV/PHEV)
- **Clean Alternative Fuel Vehicle (CAFV) Eligibility**
- **Electric Range** (target variable)
- **Base MSRP**
- **Legislative District**
- **Electric Utility**
- **2020 Census Tract**

> **Source:** Washington State Department of Licensing, [Electric Vehicle Population Data](https://data.wa.gov/)

## Objective

**Predict the electric driving range of a newly registered EV** using key attributes:
- Make
- Model Year
- Type (BEV or PHEV)
- Base MSRP
- Geographic features (County, Utility Provider, Census Tract)

## Approach

The notebook follows a standard machine learning pipeline:

1. **Data Exploration**
    - Inspection of columns, value distributions, and data consistency.
    - Visual and statistical summaries.

2. **Data Preprocessing**
    - Dropping unnecessary identifiers (VIN, DOL Vehicle ID, Vehicle Location).
    - Handling missing values for both numeric and categorical columns.
    - Feature engineering (e.g., calculating vehicle age from model year).

3. **Feature Engineering & Encoding**
    - OneHotEncoding for categorical variables.
    - Standardization for numeric features.
    - Use of `ColumnTransformer` and `Pipeline` for streamlined preprocessing and modeling.

4. **Model Training**
    - Models used:
        - Decision Tree Regressor
        - Random Forest Regressor
        - Neural Network (MLPRegressor)
    - Models trained and evaluated using `train_test_split`.

5. **Evaluation**
    - Mean Absolute Error (MAE)
    - R² Score
    - Visual comparison of actual vs. predicted electric range.
    - Residual analysis.

6. **Visualization**
    - Scatter plots of predictions vs. actuals, colored by EV type.
    - Residual plots to detect bias or heteroskedasticity.

## Results

| Model            | MAE (↓) | R² (↑)   |
|------------------|---------|----------|
| Decision Tree    | ~0.47   | ~0.9972  |
| Random Forest    | ~0.45   | ~0.9978  |
| Neural Network   | ~0.84   | ~0.9978  |

- **Random Forest exhibits the best predictive performance** in terms of both error and explained variance.

## How to Run

1. **Requirements:**
    - Python 3.x
    - pandas, numpy
    - scikit-learn
    - matplotlib, seaborn

2. **Steps:**
    - Place the dataset CSV (`Electric_Vehicle_Population_Data.csv`) in the appropriate directory.
    - Run the notebook (`ev2.ipynb`) step by step.

## Notable Code Snippets

- Data Preprocessing:
    ```python
    dataset = dataset.drop(columns=['VIN (1-10)', 'DOL Vehicle ID', 'Vehicle Location'], errors='ignore')
    dataset['Base MSRP'] = dataset['Base MSRP'].fillna(dataset['Base MSRP'].median())
    # ... handle other missing values
    ```

- Model Pipeline:
    ```python
    preprocessor = ColumnTransformer([
        ('num', StandardScaler(), numeric_cols),
        ('cat', OneHotEncoder(handle_unknown='ignore'), categorical_cols)
    ])
    rf_model = Pipeline([
        ('preprocessor', preprocessor),
        ('model', RandomForestRegressor(n_estimators=100, random_state=42))
    ])
    ```

- Evaluation:
    ```python
    def evaluate(y_true, y_pred, model_name):
        print(f"{model_name} MAE:", mean_absolute_error(y_true, y_pred))
        print(f"{model_name} R²:", r2_score(y_true, y_pred))
    ```

## Insights

- **Geographic and manufacturer information significantly improves EV range prediction.**
- **Random Forests excel with tabular, mixed-type features and limited feature engineering.**
- **Residual plots indicate minimal bias, supporting the model's reliability.**

## Next Steps

- Explore additional features (e.g., weather, charging infrastructure, detailed vehicle specs).
- Hyperparameter tuning for the best performing models.
- Deployment of the model as a web API or demo application.
