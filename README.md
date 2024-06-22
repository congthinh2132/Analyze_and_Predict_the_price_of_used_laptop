# Analyze and Predict the price of used laptop

## Used Laptop Price Prediction Project

This project explores the factors influencing used laptop prices on a commercial marketplace.

### Objective

The goal is to identify key features that affect the pricing of used laptops. By building a predictive model, we aim to estimate the price of a used laptop based on its specifications.

### Approach

The project followed a data-driven approach:

1. **Data Collection:**
    * Web scraping was used to gather data from a website. This data encompasses both structured (tabular) and unstructured formats.

2. **Data Processing and Analysis:**
    * Collected data underwent cleaning and processing to ensure its usability for modeling.
    * Exploratory data analysis (EDA) was conducted to discover patterns and relationships within the data.

3. **Model Development:**
    * Several machine learning models were developed to predict laptop prices, including:
        * Linear Regression
        * Support Vector Machine (SVM)
        * Random Forest Regression

### Technologies

* Programming Language: Python
* Data Manipulation & Analysis: Pandas, NumPy
* Machine Learning: Scikit-learn
* Data Visualization: Matplotlib

### Project Structure
project/
├── data/
│   ├── raw/ (Folder containing raw scraped data)
│   └── processed/ (Folder containing cleaned and processed data)
└── notebooks/
├── EDA_and_Model.ipynb (Jupyter notebook for exploratory data analysis and model buiding)
└── CrawedData.ipynb (Jupyter notebook for data crawling)
