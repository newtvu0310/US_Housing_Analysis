
# Property Sales Analysis

This project explores a dataset containing historical property sales data. The goal is to perform Exploratory Data Analysis (EDA) and apply Time Series forecasting techniques to understand trends and potentially predict future prices.

## Overview

The dataset (`htagholdings/property-sales`) includes information on property transactions, detailing the sale date, postcode, price, property type, and the number of bedrooms. The analysis involves cleaning the data, extracting descriptive statistics, visualizing key relationships, and preparing the data for time series modeling.

## Data Dictionary

The `raw_sales.csv` dataset contains the following columns:

*   **date**: Date the property was sold (datetime).
*   **postcode**: Postal code of the property's location (integer).
*   **price**: Sale price of the property (integer).
*   **type**: Type of property (e.g., 'house', 'unit') (object).
*   **bedrooms**: Number of bedrooms in the property (float, cleaned from 0 to NaN).

## Key Findings (EDA)

*   **Average Sale Price**: The dataset shows an overall average sale price of approximately **$609,736 AUD**.
*   **Median Sale Price**: The median price sits lower at **$550,000 AUD**, indicating a right-skewed distribution where higher-priced properties pull the mean upwards.
*   **Price by Bedrooms**: There is a clear correlation between the number of bedrooms and the average sale price.

## Technologies Used

*   **Python 3**
*   **Pandas**: Data manipulation and cleaning.
*   **NumPy**: Numerical operations.
*   **Matplotlib & Seaborn**: Data visualization.
*   **Statsmodels**: Time series analysis and forecasting.
*   **Scikit-learn**: Model evaluation metrics (MSE, MAPE, MAE, RMSE).
*   **Kaggle API**: Dataset retrieval.

## Next Steps

1.  **Time Series Decomposition**: Analyze trend, seasonality, and residuals in the sales data over time.
2.  **Stationarity Testing**: Perform Augmented Dickey-Fuller (ADF) tests.
3.  **Forecasting Models**: Implement and tune time series models to forecast future property sales trends.
4.  **Model Evaluation**: Use metrics like RMSE and MAPE to assess model accuracy.
