# [PYTHON] Explore Used Laptop Price Data Collected from an E-commerce Website


## I. Introduction:
### 1. Bussiness Questions:
The e-commerce website aims to maintain a competitive edge in the the used laptop market by offering prices that align with or outperform those of similar platforms in the industry. To achieve this, the focus is on identifying the key factors that influence the pricing of used laptops. By developing a predictive model, we aim to accurately estimate the price of a used laptop based on its specifications and other relevant attributes.

### 2. Dataset
This project utilizes data that I crawled from [Newegg](https://www.newegg.com/), one of the leading e-commerce platforms specializing in laptops and PC components. The analysis will be conducted using Python on Google Colab. After the data cleaning process, the dataset comprises 1,492 rows and 19 columns, with each row representing a single laptop and containing 19 features.

| **No.** | **Attribute**         | **Data Type** | **Description**                                                                                    |
|---------|-----------------------|---------------|----------------------------------------------------------------------------------------------------|
| 1       | Price                 | float64       | The price of the product, in USD                                                                   |
| 2       | Brand                 | object        | The brand of the laptop                                                                            |
| 3       | Screen Size           | float64       | The screen size of the laptop, measured in inches                                                  |
| 4       | CPU type              | object        | The type of processor (CPU) in the laptop                                                          |
| 5       | Memory                | int64         | The RAM capacity of the laptop, measured in GB                                                     |
| 6       | Storage               | int64         | The storage capacity of the laptop, measured in GB                                                 |
| 7       | GPU                   | object        | The graphics card of the laptop                                                                    |
| 8       | Resolution            | object        | The screen resolution of the laptop                                                                |
| 9       | Weight                | float64       | The weight of the laptop, measured in lbs                                                          |
| 10      | Backlit Keyboard      | object        | Whether the laptop has a backlit keyboard                                                          |
| 11      | Touchscreen           | object        | Whether the laptop supports a touchscreen                                                          |
| 12      | Graphic Type          | object        | The type of graphics in the laptop, either integrated (Integrated) or dedicated (Dedicated)        |
| 13      | Operating System      | object        | The operating system of the laptop                                                                 |
| 14      | Webcam                | object        | Whether the laptop has an integrated webcam                                                        |
| 15      | Card Reader           | object        | Whether the laptop has an integrated card reader                                                   |
| 16      | Thunderbolt           | object        | Whether the laptop has a Thunderbolt port                                                          |
| 17      | CPU model             | object        | The specific model of the processor (CPU)                                                          |
| 18      | Title                 | object        | The product title                                                                                  |
| 19      | Link                  | object        | The link to the product page on Newegg                                                             |

## II. Requirement:
* Jupiter Notebook: [Google Colab](https://colab.research.google.com/)
* Programming Language: Python 3.x
* Data Manipulation & Analysis: Pandas, NumPy
* Machine Learning: Scikit-learn
* Data Visualization: Matplotlib

## III. Dataset Access:
* Web scraping was used to gather data from a website. This data encompasses both structured (tabular) and unstructured formats.
* Everyone can download the cleaned dataset [here](https://github.com/congthinh2132/Analyze_and_Predict_the_price_of_used_laptop/blob/main/cleaned_dataset.csv).

## IV. Process:

The project followed a data-driven approach:
1. **Data Collection:**
   * Use Selenium WebDriver to open the Newegg website and iterate through desired pages.
   * Parse the loaded HTML using BeautifulSoup.
   * Extract product details (e.g., title, link, price, specifications) from relevant containers on the page.
   * Save the collected data into a DataFrame and export it to a CSV file for analysis.
The source code for the data collection process can be found [here](https://github.com/congthinh2132/Analyze_and_Predict_the_price_of_used_laptop/blob/main/source/CrawlData.ipynb).

2. **Data preprocessing and cleaning:**
* **Data Cleaning**:
   * This section involved reviewing the dataset for missing values, duplicates, and incorrect data types. Actions were taken to ensure data integrity, including imputing missing values, removing duplicates, and correcting data types where necessary. Furthermore, any outliers or incorrect values were identified and handled in accordance with the dataset's context to preserve accuracy and consistency.
   * Columns "Resolution," "Weight," and "CPU model" have missing values.
   * For "Resolution," fill missing values with the mode (most frequent) of the column.
   * For "Weight" and "CPU model," remove rows with missing values.
-> Verify that no columns contain missing values after handling.

* **Data Preprocessing and Feature Engineering**:
  * "Price":
      * Use the IQR (Interquartile Range) method to identify and remove outliers in the "Price" column.
      * Calculate the lower and upper bounds using IQR.
      * Create a new DataFrame that only contains rows where "Price" is within the specified range, improving model performance by ensuring a more uniform distribution.
![image](https://github.com/user-attachments/assets/41653e92-e189-48d6-b956-91db9db338e2)
  * "Backlit Keyboard", "Thunderbolt", "Card Reader", "Touchscreen":
      Group values into two categories: "yes" and "no" to simplify the variable, as different sellers may use different terms, and missing values are often left blank.
      Replace "yes" with 1 and "no" with 0 for these columns.
  * "Resolution":
      Split "Resolution" into width and height.
      Convert the data type to integer.
      Calculate PPI (Pixels Per Inch) using the formula:
      PPI = √(width² + height²) / screen size.
      Add the new "ppi" column to the dataset.
  * "CPU" and "GPU":
      Identify the list of CPU and GPU types.
      Create new columns, "CPU_series" from "CPU type" and "GPU_brand" from "GPU."
      Categorize values into groups such as Intel Core, AMD Ryzen, NVIDIA, AMD, or Other for items not listed.


3. **Model Development:**
* Select Input and Output Variables: Choose the input variables ("features") and output variable ("target") from the dataset.
* Split the Data: Use the train_test_split function to split the data into training (X_train, y_train) and testing (X_test, y_test) sets with an 80-20% ratio.
* Build Preprocessing Pipeline: Identify numerical features ("numeric_features") and categorical features ("categorical_features").
* Use ColumnTransformer to apply preprocessing steps such as normalizing numerical features and encoding categorical features.
* Build the Model: Select the RandomForestRegressor model with predefined hyperparameters.
* Create the Model Pipeline: Combine the preprocessing steps and the regression model into a single pipeline.
* Train the Model: Train the model using the training data (X_train, y_train) through the established pipeline.
   
## V. Visualizations and Insights:
**Average Price by Laptop Brand**: The bar chart are used to compare the pricing trends among brands.
![image](https://github.com/user-attachments/assets/d854ef71-7add-4cdc-b1ed-a9a52ada8dcd)
**Observations**: The distribution of laptop prices by brand shows significant variation, with premium brands like Razer having much higher average prices compared to budget brands or small brands.

**Average Price by 'Backlit Keyboard', 'Thunderbolt', and 'Card Reader' options**: The bar charts highlight pricing trends between laptops with and without these features.
![image](https://github.com/user-attachments/assets/8ba40cdc-2005-420e-90a7-3334d460f0ed)
**Observations**: For the variables 'Backlit Keyboard', 'Thunderbolt', and 'Card Reader', the chart illustrated that products with these features tend to have a higher average price compared to those without. This is because these features are often additional options for laptops, and some of them are typically found only in premium versions.

**Average Price by 'CPU series' and 'GPU brand'**: The bar charts illustrate the price differences across various CPU series and GPU brands
![image](https://github.com/user-attachments/assets/6bf05156-75df-4fec-97a1-19170ca7fe03)
![image](https://github.com/user-attachments/assets/7719a70b-9373-4f78-b789-1d820d91320a)
**Observations**: The 'CPU series' and 'GPU brand' positively influence the 'price' of laptops, as higher-performing CPUs and GPUs typically lead to higher prices. The same trend applies to RAM and storage—laptops with larger capacities generally cost more.

**Title**: The heatmap shows the correlation between feature varibles and target varible.
![image](https://github.com/user-attachments/assets/298c47f4-ee51-41a4-bb20-64faefd70975)
**Observations**: The investigation into the relationships among laptop features reveals fascinating connections, with Price taking center stage.
* Price and Screen Size are the star duo, consistently linked in high-end laptops, where larger screens command higher prices.
* Memory and Storage work as a reliable team, boosting performance and contributing to higher prices in tandem.
* Price and PPI appear to clash, with higher PPI often found in more affordable laptops, suggesting an inverse relationship between affordability and display quality.
* Backlit Keyboard and Touchscreen form a modern alliance, commonly seen in stylish, premium devices, which naturally come with higher price tags.
* Card Reader plays the enigmatic role, lightly influencing many features but not significantly affecting the price.
* Thunderbolt, exclusive and powerful, prefers its niche, usually associated with higher-priced laptops.

## VI. Conclusions:
Comparing base on the metrics we can see that Random Forest Regression (RFR) model shows the best performance with an R² score of 0.81, outperforming the other models. This indicates that RFR better captures the relationships between independent and dependent variables in this problem.
|Model	                  |R2	 |MAE	  |RMSE   |
|-------------------------|----|------|-------|
|Linear Regression	      |0.63|290.52|398.94 |
|SVR	                    |0.62|266.47|402.59 |
|Random Forest Regressor	|0.73|231.45|338.97 |

However, the model still has limitations, as the prediction errors (MAE and RMSE) remain relatively high.
The model's accuracy could be further improved by:
* Using more complex machine learning models.
* Collecting additional data to enhance feature richness and diversity.

In this project, we explored the factors influencing laptop prices through data analysis, preprocessing, and machine learning modeling. Key insights include:
* Feature Analysis: Variables like 'Brand', 'CPU series', 'GPU brand', 'RAM', and 'Storage' have a significant impact on price. Premium features like 'Backlit Keyboard', 'Thunderbolt', and 'Card Reader' also contribute to higher prices.
* Challenges and Recommendations: The dataset's limitations more complex models could be explored, and additional data could be collected for better feature diversity.
Overall, the project highlights the value of data-driven insights for understanding the laptop market and predicting prices accurately, offering a foundation for future research and application.


