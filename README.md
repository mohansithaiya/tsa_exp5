# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 16/05/2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import warnings

warnings.filterwarnings("ignore")

# Load dataset
data = pd.read_excel('/content/Hyderabad-AirQ.xlsx')

# Clean column names
data.columns = data.columns.str.strip()

# Convert Date column
data['Date'] = pd.to_datetime(data['Date'])

# Remove missing values
data = data.dropna(subset=['Date', 'PM2.5'])

# Set Date as index
data.set_index('Date', inplace=True)

# Aggregate data
data = data.resample('M')['PM2.5'].mean()

# Convert into dataframe
data = pd.DataFrame(data)

# Remove missing values
data = data.dropna()

# Seasonal decomposition
decomposition = seasonal_decompose(
    data['PM2.5'],
    model='additive',
    period=2
)

# Plot graphs
plt.figure(figsize=(10, 12))

# Original
plt.subplot(411)
plt.plot(data['PM2.5'], label='PM2.5')
plt.legend(loc='upper left')
plt.title('Original Data')

# Trend
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend')

# Seasonal
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality')

# Residual
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual')

plt.tight_layout()
plt.show()
```




### OUTPUT:
<img width="977" height="1189" alt="image" src="https://github.com/user-attachments/assets/8b1a89a2-aed9-4faa-8aaf-449ebf5e6cf7" />


### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
