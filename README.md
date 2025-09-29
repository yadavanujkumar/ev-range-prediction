# EV Range Prediction Notebook

This project is a Jupyter notebook that predicts the electric driving range (in miles) of electric vehicles (EVs) using machine learning. The dataset is based on Washington State registered EVs and includes features like make, model year, type (BEV/PHEV), MSRP, location, and more.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Usage](#usage)
- [Results & Visualizations](#results--visualizations)
- [Requirements](#requirements)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The goal is to accurately predict the electric driving range of an EV based on its attributes and location. The notebook walks through data cleaning, preprocessing, model training, and evaluation with visualizations to assess model performance.

---

## Features

- **Data Cleaning:** Handles missing values, irrelevant columns, and feature engineering (e.g., vehicle age).
- **Encoding:** Standardizes numeric features and one-hot encodes categorical variables.
- **Modeling:** Compares multiple machine learning models:
  - Decision Tree Regressor
  - Random Forest Regressor
  - Neural Network (MLPRegressor)
- **Evaluation:** Uses MAE and R² metrics, provides scatter plots and error analysis.
- **Visualizations:** Actual vs. predicted range, error histograms, and boxplots by EV type.

---

## Dataset

- **Source:** Washington State EV registration data.
- **Sample Features:**
  - Model Year
  - Make & Model
  - Electric Range (target)
  - Base MSRP
  - Electric Vehicle Type (BEV or PHEV)
  - Geographic features (County, Utility, Census Tract)
  - link : https://share.google/fq0rlLU9ddiFiY2l9
---

## Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yadavanujkumar/ev-range-prediction.git
   cd ev-range-prediction
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook:**
   - Open `ev.ipynb` in Jupyter Notebook or JupyterLab.
   - Run all cells to reproduce the analysis.

4. **(Optional) Use your own data:**
   - Replace the dataset CSV with your own, ensuring the column names match.

---

## Results & Visualizations

- **High Model Accuracy:** Random Forest achieves very low mean absolute error (MAE < 1 mile) and high R² (>0.99).
- **Visual Analysis:** Most predictions fall close to actual values, and errors are well-distributed and unbiased.

Sample visualizations produced:
- Scatter plot: Actual vs. Predicted Range
- Histogram: Distribution of prediction errors
- Boxplot: Error grouped by EV type (BEV/PHEV)

---

## Requirements

- Python 3.8+
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- jupyter

Install dependencies with:
```bash
pip install -r requirements.txt
```


## Contributing

Contributions welcome! Please open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License.
