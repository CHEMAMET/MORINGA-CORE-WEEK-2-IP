# Financial Inclusion in East Africa

A Machine learning project examining financial inclusion across Kenya, Rwanda, Tanzania, and Uganda to predict bank account ownership and identify key demographic factors influencing financial outcomes.

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Methodology](#methodology)
- [Results](#results)
- [Model Performance](#model-performance)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Project Overview

This project addresses the challenge of financial inclusion in East Africa. Financial inclusion remains one of the main obstacles to economic and human development in the region, with only 13.9% of the adult population having access to or using a commercial bank account across Kenya, Rwanda, Tanzania, and Uganda.

### Research Question
Predict which individuals are most likely to have or use a bank account, while providing insights into the state of financial inclusion in Kenya, Rwanda, Tanzania, and Uganda.

### Success Metric
The model is considered successful if it can accurately identify demographic factors that drive financial outcomes and provide meaningful insights into financial inclusion patterns.

## 📊 Dataset

- **Source**: Various Finscope surveys (2016-2018)
- **Creators**: Financial Sector Deepening organizations across East Africa
- **Generated**: 2016-2018
- **Size**: 23,524 individuals with 13 features
- **Features**: 
  - Demographic information (age, gender, education level)
  - Household characteristics (size, relationship with head)
  - Geographic indicators (country, location type)
  - Economic factors (job type, marital status)
  - Technology access (cell phone access)
  - Target variable: bank account ownership (Yes/No)

### Dataset Characteristics
- **Missing values**: Initially contained missing values across multiple columns (handled during preprocessing)
- **Class distribution**: 14.1% with bank accounts, 85.9% without bank accounts
- **Data cleaning**: Null values removed, column names standardized, anomalies in year column addressed

## 🛠 Installation

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels pandas-profiling
```

### Required Libraries
```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from pandas_profiling import ProfileReport
from sklearn import model_selection
from sklearn.metrics import r2_score
from sklearn.model_selection import train_test_split
import statsmodels.api as sm
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score
from sklearn.linear_model import LogisticRegression
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
```

## 🚀 Usage

1. **Load the dataset**:
```python
df = pd.read_csv('http://bit.ly/FinancialDataset')
```

2. **Run the preprocessing**:
```python
# Drop null values
df.dropna(inplace=True)

# Drop unnecessary columns
df.drop(['uniqueid'], axis=1, inplace=True)

# Standardize column names
df.columns = df.columns.str.lower().str.replace(" ", "_")
df.rename(columns={'the_relathip_with_head':'the_relationship_with_head'}, inplace=True)
df.rename(columns={'level_of_educuation':'level_of_education'}, inplace=True)

# Remove anomalies
indexnames = df[df['year'] > 2018].index
df.drop(indexnames, inplace=True)
```

3. **Perform exploratory analysis**:
```python
# Basic visualizations
plt.figure(figsize=(6,6), dpi=90)
plt.pie(df['has_a_bank_account'].value_counts().values, 
        labels=df['has_a_bank_account'].value_counts().index, 
        autopct='%1.1f%%', shadow=True, explode=(0,0.1), startangle=140)
plt.axis('equal')
plt.title('Bank Account Ownership Distribution')
plt.show()
```

## 🔬 Methodology

### 1. Data Preparation
- **Missing value handling**: Null values identified and removed
- **Feature engineering**: Column names standardized and corrected
- **Anomaly detection**: Outliers in year column identified and removed

### 2. Exploratory Data Analysis
- **Univariate analysis**: Distribution of individual variables examined
- **Bivariate analysis**: Relationships between variables explored
- **Multivariate analysis**: Complex interactions between multiple variables analyzed

### 3. Visualization
- **Pie charts**: Used to visualize categorical distributions (bank account ownership, job types)
- **Bar charts**: Displayed country distribution and education levels
- **Box plots**: Identified outliers in age and household size

### 4. Dimensionality Reduction
- Applied to identify key factors affecting financial inclusion

### 5. Multiple Regression Modeling
- Built predictive models to identify factors influencing bank account ownership

## 📈 Results

### Key Findings

1. **Low Financial Inclusion**: Only 14.1% of respondents had a bank account, while 85.9% did not
2. **Employment Patterns**: Top employment categories were self-employed, informally employed, and farming/fishing
3. **Education Impact**: Most respondents' highest level of education was primary school
4. **Demographic Insights**: Dataset includes respondents from ages 16 to 100, with a mean age of approximately 39 years
5. **Household Characteristics**: Average household size is about 3.7 people, with some households having up to 21 members

### Country-Specific Observations
- **Rwanda**: Highest number of survey respondents
- **Uganda**: Lowest number of survey respondents
- **Distribution**: Unequal representation across countries may impact generalizability

## 🏆 Model Performance

### Strengths
- ✅ Comprehensive dataset covering four East African countries
- ✅ Multiple demographic and socioeconomic variables for analysis
- ✅ Recent data (2016-2018) providing relevant insights
- ✅ Balanced approach combining visualization and statistical modeling

### Limitations
- ⚠️ Class imbalance in target variable (85.9% without bank accounts)
- ⚠️ Potential sampling biases in original surveys
- ⚠️ Limited technological variables beyond cell phone access
- ⚠️ Lack of longitudinal data to track changes over time

### Recommendations
1. Address class imbalance through sampling techniques
2. Incorporate additional financial technology variables
3. Consider country-specific models to account for regional differences
4. Explore interaction effects between demographic variables

## 🔧 Technical Details

### Data Sources
- **FinAccess Kenya 2018**: [https://fsdkenya.org/publication/finaccess2019/](https://fsdkenya.org/publication/finaccess2019/)
- **Finscope Rwanda 2016**: [http://www.statistics.gov.rw/publication/finscope-rwanda-2016](http://www.statistics.gov.rw/publication/finscope-rwanda-2016)
- **Finscope Tanzania 2017**: [http://www.fsdt.or.tz/finscope/](http://www.fsdt.or.tz/finscope/)
- **Finscope Uganda 2018**: [http://fsduganda.or.ug/finscope-2018-survey-report/](http://fsduganda.or.ug/finscope-2018-survey-report/)

### Variable Definitions
- Variable Definitions: [http://bit.ly/VariableDefinitions](http://bit.ly/VariableDefinitions)
- Dataset: [http://bit.ly/FinancialDataset](http://bit.ly/FinancialDataset)

## 📝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Setup
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

## 📄 License

Please refer to the original data sources for licensing information regarding the datasets used in this analysis.

## 🙏 Acknowledgments

- Financial Sector Deepening organizations across East Africa for the survey data
- The organizations responsible for collecting and providing access to the Finscope surveys
- Contributors to the open-source Python libraries used in this analysis

---

**Note**: This analysis is based on data from 2016-2018. For current insights, consider updating with more recent financial inclusion survey data from the region.
