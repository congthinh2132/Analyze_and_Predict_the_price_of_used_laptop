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

## IV. Process

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

* **Data Preprocessing**:
   * Price:
      * Use the IQR (Interquartile Range) method to identify and remove outliers in the "Price" column.
      * Calculate the lower and upper bounds using IQR.
      * Create a new DataFrame that only contains rows where "Price" is within the specified range, improving model performance by ensuring a more uniform distribution.
   
![image](https://github.com/user-attachments/assets/41653e92-e189-48d6-b956-91db9db338e2)

   * Backlit Keyboard, Thunderbolt, Card Reader, Touchscreen:
      Group values into two categories: "yes" and "no" to simplify the variable, as different sellers may use different terms, and missing values are often left blank.
      Replace "yes" with 1 and "no" with 0 for these columns.
   * Resolution:
      Split "Resolution" into width and height.
      Convert the data type to integer.
      Calculate PPI (Pixels Per Inch) using the formula:
      PPI = √(width² + height²) / screen size.
      Add the new "ppi" column to the dataset.
   * CPU and GPU:
      Identify the list of CPU and GPU types.
      Create new columns, "CPU_series" from "CPU type" and "GPU_brand" from "GPU."
      Categorize values into groups such as Intel Core, AMD Ryzen, NVIDIA, AMD, or Other for items not listed.


4. **Model Development:**
    * Several machine learning models were developed to predict laptop prices, including:
        * Linear Regression
        * Support Vector Machine (SVM)
        * Random Forest Regression
     
## V. Insights:

## Recommendations


