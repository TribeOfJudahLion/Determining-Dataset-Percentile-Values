<br/>
<p align="center">
  <a href="https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values">
    <img src="" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Unveil Data's Hidden Stories: Dive into Percentile Insights</h3>

  <p align="center">
    "Slice through statistics, spot trends, and unlock insights"
    <br/>
    <br/>
    <a href="https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values"><strong>Explore the docs »</strong></a>
    <br/>
    <br/>
    <a href="https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values">View Demo</a>
    .
    <a href="https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/issues">Report Bug</a>
    .
    <a href="https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/issues">Request Feature</a>
  </p>
</p>

![Downloads](https://img.shields.io/github/downloads/TribeOfJudahLion/Determining-Dataset-Percentile-Values/total) ![Contributors](https://img.shields.io/github/contributors/TribeOfJudahLion/Determining-Dataset-Percentile-Values?color=dark-green) ![Stargazers](https://img.shields.io/github/stars/TribeOfJudahLion/Determining-Dataset-Percentile-Values?style=social) ![Issues](https://img.shields.io/github/issues/TribeOfJudahLion/Determining-Dataset-Percentile-Values) ![License](https://img.shields.io/github/license/TribeOfJudahLion/Determining-Dataset-Percentile-Values) 

## Table Of Contents

* [About the Project](#about-the-project)
* [Built With](#built-with)
* [Getting Started](#getting-started)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Authors](#authors)
* [Acknowledgements](#acknowledgements)

## About The Project

### Problem Description:

The World Health Organization (WHO) has released a new comprehensive dataset of daily reported COVID-19 cases across various countries and continents. The dataset, `covid-data.csv`, includes multiple columns, but the WHO is specifically interested in analyzing the trend of new cases and total cases at a country level. However, the dataset is large and contains some inconsistencies and formatting issues.

The WHO has tasked a data analyst with the following objectives:

1. Load the dataset while ensuring that it is read correctly and efficiently into a Python environment for analysis.
2. Select a subset of columns that are relevant for the analysis: `iso_code`, `continent`, `location`, `date`, `total_cases`, and `new_cases`.
3. Ensure that the date column is in the correct datetime format to facilitate time-series analysis.
4. Convert the columns `total_cases` and `new_cases` to numeric types, and handle any conversion errors.
5. Perform an initial analysis to understand the distribution of new daily cases by calculating specific percentiles.
6. The solution must include error handling for potential issues like missing files or data inconsistencies.

The WHO requires the above steps to be completed in a reproducible and automated manner so that the analysis can be repeated as new data is released.

### Proposed Solution:

The solution involves writing a Python script that uses the `pandas` and `numpy` libraries to load, preprocess, and analyze the dataset. The script will be divided into functions that can be called to perform the analysis as needed.

#### Step-by-step Code Explanation:

1. **Import Libraries**:
   ```python
   import numpy as np
   import pandas as pd
   ```

2. **Define Data Loading and Preprocessing Function**:
   ```python
   def load_and_preprocess_data(filepath):
       try:
           data = pd.read_csv(filepath)
           columns_of_interest = ['iso_code', 'continent', 'location', 'date', 'total_cases', 'new_cases']
           data = data[columns_of_interest]
           data['date'] = pd.to_datetime(data['date'])
           numeric_columns = ['total_cases', 'new_cases']
           data[numeric_columns] = data[numeric_columns].apply(pd.to_numeric, errors='coerce')
           return data
       except FileNotFoundError:
           print(f"The file {filepath} does not exist.")
           return None
       except Exception as e:
           print(f"An error occurred: {e}")
           return None
   ```

3. **Load the Data**:
   ```python
   covid_data_filepath = "covid-data.csv"
   covid_data = load_and_preprocess_data(covid_data_filepath)
   ```

4. **Inspect the Data**:
   If the data is successfully loaded, the script will print the first few rows, the data types of the columns, and the shape of the dataframe.

5. **Analyze the Data**:
   If the dataframe is not empty, calculate and print the percentiles for the 'new_cases' column:
   ```python
   if covid_data is not None:
       percentiles_to_calculate = [25, 50, 60, 75, 90]
       percentiles = np.percentile(covid_data['new_cases'].dropna(), percentiles_to_calculate)
       for p, value in zip(percentiles_to_calculate, percentiles):
           print(f"{p}th percentile for new_cases is: {value}")
   ```

#### Error Handling:

- `try-except` blocks catch and handle exceptions during the data loading and preprocessing steps.
- A check for `None` ensures that the code does not attempt to operate on a dataframe if the data loading step failed.

#### Results and Reporting:

The script will output the results directly to the console. The percentiles calculated provide insights into the distribution of new cases and are useful for identifying trends or patterns. If an error occurs, it will be printed with a descriptive message.

### Extension to the Problem for Future Work:

To further refine the analysis and add more functionality, the following extensions could be considered:

1. **Automated Data Updates**: Schedule the script to run automatically when new data is released.
2. **Data Quality Checks**: Implement checks for missing values, duplicates, or outliers and handle them appropriately.
3. **Data Visualization**: Generate plots to visually represent the trends and distribution of new cases.
4. **Report Generation**: Develop a system to generate a report with the analysis findings, including tables and figures.
5. **Interactive Dashboard**: Create a dashboard using a library like Dash or Streamlit for interactive data exploration.
6. **Predictive Modeling**: Apply statistical or machine learning models to forecast future case numbers.



### Code Breakdown

#### Importing Libraries
The script starts with importing necessary Python libraries:

```python
import numpy as np
import pandas as pd
```

`numpy` is used for numerical operations, and `pandas` is a powerful library for data manipulation and analysis.

#### Data Loading and Preprocessing Function

The next segment defines a function `load_and_preprocess_data(filepath)` that is responsible for loading and preprocessing the COVID-19 dataset.

- The `filepath` parameter is the location of the .csv file containing the data.
- The function uses `pandas` to load the csv file into a `DataFrame`.
- After loading, it selects specific columns that are of interest (`iso_code`, `continent`, `location`, `date`, `total_cases`, `new_cases`).
- It converts the `date` column to a `datetime` object, which is necessary for any time-series analysis.
- It also ensures that `total_cases` and `new_cases` are treated as numeric values, using `pd.to_numeric`, and errors during conversion are coerced to NaN (not a number).

The function includes error handling using `try-except` blocks to handle scenarios where the file might not be found or other exceptions could occur during data loading and preprocessing.

#### Data Loading

```python
covid_data_filepath = "covid-data.csv"
covid_data = load_and_preprocess_data(covid_data_filepath)
```

Here, the script specifies the filepath of the dataset and calls the `load_and_preprocess_data()` function, storing the processed data in `covid_data`.

#### Inspecting the Data

The next code blocks are conditional, and will only execute if `covid_data` is not `None` (which implies that the data was loaded successfully):

- `covid_data.head(5)` displays the first five rows of the dataframe.
- `covid_data.dtypes` prints the data types of the columns.
- `covid_data.shape` provides the dimensions of the dataframe (number of rows and columns).

#### Analyzing the Data

The final provided code snippet (before the message was cut off) was aimed at understanding the distribution of `new_cases` by calculating various percentiles:

```python
percentiles_to_calculate = [25, 50, 60, 75, 90]
percentiles = np.percentile(covid_data['new_cases'].dropna(), percentiles_to_calculate)
for p, value in zip(percentiles_to_calculate, percentiles):
    print(f"{p}th percentile for new_cases is: {value}")
```

- It calculates the 25th, 50th, 60th, 75th, and 90th percentiles of the `new_cases` column to understand its distribution. The `np.percentile` function is used for this calculation.
- It uses `.dropna()` to ignore `NaN` values which could otherwise skew the results.
- The loop at the end prints out each calculated percentile value.


### Considerations and Recommendations

- It is good practice to ensure that the script includes adequate error checking when dealing with file operations and data transformations, as shown in the provided code.
- Depending on the size of the dataset, some operations could be memory-intensive. It might be beneficial to optimize by using appropriate data types (e.g., `category` for string columns with few unique values) and considering chunk processing for very large files.
- When dealing with time-series data, it is essential to check for the presence of time gaps or duplicates, which might require additional preprocessing.
- Additional exploratory data analysis (EDA) such as checking for null values, outliers, or visualizing the data trends could provide more insights into the dataset.
- It’s also crucial to ensure that the calculated percentiles make sense in the context of the data. For example, if there are many zero values or outliers, this might significantly affect percentile calculations.

This code provides a robust foundation for loading, preprocessing, and initial analysis of COVID-19 case data, which can be built upon for further analysis or modeling.

## Built With

This project leverages the power of high-performance libraries and cutting-edge technologies to process and analyze COVID-19 dataset percentiles:

- **Python**: Our core programming language, chosen for its readability, rich ecosystem of libraries, and its widespread use in data science.
  - [Python 3.x](https://www.python.org/downloads/) - The version of Python used, optimized for its modern features and security enhancements.
  
- **Pandas**: The backbone for our data manipulation and analysis, enabling us to work with large data sets efficiently and intuitively.
  - [Pandas Library](https://pandas.pydata.org/) - Used for data structures and data analysis tools.

- **NumPy**: Integrated with Pandas, NumPy provides the numerical foundation, particularly for percentile calculations on large arrays of data.
  - [NumPy Library](https://numpy.org/) - For high-level mathematical functions and multi-dimensional arrays.
  
- **Matplotlib** / **Seaborn**: These plotting libraries offer the means to visualize data and percentiles, providing insights at a glance.
  - [Matplotlib Library](https://matplotlib.org/) - For creating static, interactive, and animated visualizations in Python.
  - [Seaborn Library](https://seaborn.pydata.org/) - For making attractive and informative statistical graphics.

- **Jupyter Notebooks**: Our interactive computational environment, where we weave code, visuals, and narrative into a complete analysis story.
  - [Jupyter Notebook](https://jupyter.org/) - For combining code execution, rich text, visualizations, and other media.

- **Git**: Essential for version control, helping us manage and track the evolution of our project codebase.
  - [Git SCM](https://git-scm.com/) - For distributed version control and source code management.

- **GitHub**: The platform we chose for hosting our code, managing our project, and collaborating across the development team.
  - [GitHub](https://github.com/) - For hosting and collaborating on our project repository.

- **Virtual Environments**:
  - [venv](https://docs.python.org/3/library/venv.html) / [conda](https://docs.conda.io/en/latest/) - To manage our project’s dependencies separately, avoiding any package conflicts.

- **CSV Files**: The standard format in which the COVID-19 dataset is maintained and shared for our analysis.
  - [COVID-19 Data Repository by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University](https://github.com/CSSEGISandData/COVID-19) - The source of our COVID-19 data.


## Getting Started

Welcome to the COVID-19 Data Analysis project. This guide will walk you through the setup process to get the project running on your local system for development and testing purposes. Here's everything you need to do, step by step.

### Prerequisites

Before you begin, ensure you have the following installed on your system:
- Python 3.x - [Download & Installation Guide](https://www.python.org/downloads/)
- Git - [Download & Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Installation

#### 1. Clone the Repository

Firstly, you'll need to clone the repository using Git. Open your terminal and run the following command:

```sh
git clone https://github.com/your-username/your-project-name.git
```

Navigate to the cloned project directory:

```sh
cd your-project-name
```

#### 2. Virtual Environment Setup

It's recommended to create a virtual environment to manage the project's dependencies:

**Using venv:**

```sh
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
```

**Using conda:**

```sh
conda create --name myenv python=3.x
conda activate myenv
```

#### 3. Install Required Packages

Install all the required packages using the `requirements.txt` file with pip:

```sh
pip install -r requirements.txt
```

Or, if you prefer using conda, you might specify each package individually:

```sh
conda install pandas numpy matplotlib seaborn jupyter
```

#### 4. Launch Jupyter Notebook

To view and interact with the project Jupyter Notebooks:

```sh
jupyter notebook
```

This command will open a new browser window/tab displaying the Jupyter Dashboard.

### Usage

After installation, you can run each script directly from the terminal:

```sh
python script_name.py
```

Or you can open the Jupyter Notebooks in the project directory to view the detailed analysis:

```sh
jupyter notebook notebook_name.ipynb
```

### Running the Tests

Explain how to run the automated tests for this system (if applicable). You might provide a command like:

```sh
python -m unittest discover
```

## Roadmap

See the [open issues](https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/issues) for a list of proposed features (and known issues).

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.
* If you have suggestions for adding or removing projects, feel free to [open an issue](https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/issues/new) to discuss it, or directly create a pull request after you edit the *README.md* file with necessary changes.
* Please make sure you check your spelling and grammar.
* Create individual PR for each suggestion.
* Please also read through the [Code Of Conduct](https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/blob/main/CODE_OF_CONDUCT.md) before posting your first idea as well.

### Creating A Pull Request

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See [LICENSE](https://github.com/TribeOfJudahLion/Determining-Dataset-Percentile-Values/blob/main/LICENSE.md) for more information.

## Authors

* **Robbie** - *PhD Computer Science Student* - [Robbie](https://github.com/TribeOfJudahLion/) - **

## Acknowledgements

* []()
* []()
* []()
