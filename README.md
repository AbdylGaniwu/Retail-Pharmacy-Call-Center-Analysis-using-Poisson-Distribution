# Utilizing Poisson Distribution for Retail Pharmacy Call Center Insights

## Overview

This project focuses on analyzing the performance of a **Retail Pharmacy Call Center** using a dataset covering the period from 2017 to 2023. The primary focus is on understanding how incoming calls behave in relation to other metrics such as answered calls, waiting time, and service levels. Poisson distribution is used to model incoming call events, providing insight into the randomness and potential influencing factors. 

Exploring the relationship between **Incoming Calls**, **Answered Calls**, **Waiting Time**, and **Service Level** to derive operational insights.

## Dataset Description
The dataset was extracted from a retail pharmacy call center where I work. It includes various key metrics that capture the performance and efficiency of the center over the period from 2017 to 2023. The columns in the dataset are as follows:

- **Year**: Year from 2017 to 2023.
- **Incoming Calls**: Number of calls received by the call center.
- **Answered Calls**: Number of calls answered.
- **Abandoned Calls**: Number of calls abandoned by the caller.
- **Answer Speed (AVG)**: The average time taken to answer a call.
- **Talk Duration (AVG)**: Average time spent talking to the caller.
- **Waiting Time (AVG)**: Average waiting time for callers.
- **Service Level (20 Seconds) AVG**: Percentage of calls answered within 20 seconds.

## Analysis

### 1. **Data Assessment**

- **Data Types**: Checked the data types of each column. || (df.info())
- **Missing Values**: There were no missing values in the dataset. || (df.isnull().sum())
- **Duplicate Rows**: No duplicate rows were found. || (df.duplicated().sum())

### 2. **Poisson Distribution Analysis**

The **Poisson Distribution** is used to model the number of events occurring within a fixed time interval (years). Given that the number of incoming calls varies year by year, this distribution helps in understanding whether the incoming call data fits a Poisson process or whether external factors are influencing call volume.

#### Key Questions:
1. **What is the average number of incoming calls?**
   - Calculated the average number of incoming calls, which was **198.54** calls per year.

2. **Does the incoming call data follow a Poisson distribution?**
   - By plotting the actual incoming call data against a Poisson distribution with the same mean, we found that the distribution was skewed to the right, suggesting external factors influencing the number of calls.

3. **What is the probability of receiving a certain number of calls in a year?**
   - Example: The probability of receiving exactly 1000 calls in a year was calculated to be **0.0** using the Poisson probability mass function.

### 3. **Correlation Analysis**

#### Key Questions:

1. **Are incoming calls correlated with waiting time?**
   - A correlation coefficient of **0.95** was found between incoming calls and answered calls, indicating a strong positive correlation. This suggests that as incoming call volume increases, the number of answered calls also increases proportionally.

2. **What is the relationship between service level and incoming calls?**
   - There was a negative correlation of **-0.49** between incoming calls and service level. This implies that as call volume increases, the service level (percentage of calls answered within 20 seconds) tends to decrease, likely indicating a capacity strain on the call center during high traffic periods.

### 4. **Service Level Trends**

A time series analysis of service levels from 2017 to 2023 showed that:

- There was an upward trend in service levels from 2017 to 2020.
- A significant drop occurred in 2021, possibly due to operational or external factors.
- Service levels improved significantly in 2022 and 2023, indicating successful operational adjustments.

### 5. **Key Insights**

- **Incoming Call Patterns**: Deviations from the Poisson distribution suggest that external factors like holidays or promotions might be influencing call volumes.
- **Operational Efficiency**: The negative correlation between service levels and incoming calls highlights the need for better call management during peak times, perhaps through staffing adjustments.
- **Answered Calls**: The high correlation between incoming and answered calls shows the call center's ability to keep pace with incoming traffic, but there is room for improvement in service levels.


```python
# Import necessary libraries
import pandas as pd
import numpy as np
from scipy.stats import poisson
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv('retail_pharmacy_call_center_dataset.csv')

# Explore the first 5 rows
df.head()

# Perform Poisson Distribution analysis
avg_incoming_calls = df['Incoming Calls'].mean()
poisson_dist = poisson.pmf(np.arange(0, df['Incoming Calls'].max()), avg_incoming_calls)

# Plot Actual vs Poisson Distribution
plt.hist(df['Incoming Calls'], bins=30, density=True, alpha=0.6, color='g', label='Actual Incoming Calls')
plt.plot(np.arange(0, df['Incoming Calls'].max()), poisson_dist, 'b-', label='Poisson Distribution')
plt.title('Incoming Calls vs Poisson Distribution')
plt.xlabel('Number of Incoming Calls')
plt.ylabel('Probability')
plt.legend()
plt.show()

# Correlation between Incoming Calls and Answered Calls
correlation = df['Incoming Calls'].corr(df['Answered Calls'])
print(f'Correlation between Incoming Calls and Answered Calls: {correlation:.2f}')
```

## Conclusion

This project provides a comprehensive analysis of a retail pharmacy call center using Poisson distribution, correlation analysis, and time-series trends. By using Python and pandas, we've gained operational insights that could help improve service levels and manage incoming call traffic more efficiently.

Feel free to explore the code and contribute if you have any suggestions!
