
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date:

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Gold prediction data(XAUUAE data).


### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.


### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load the CSV file
data = pd.read_csv('XAUUSD_2010-2023.csv')

# Select only the 'time' and 'close' columns
data = data[['time', 'close']]
data.rename(columns={'close': 'ClosePrice'}, inplace=True)

# Convert 'time' column to datetime format
data['time'] = pd.to_datetime(data['time'], format='%d-%m-%Y %H:%M')

# Set 'time' as the index
data.set_index('time', inplace=True)

# Perform transformations
data['Differenced'] = data['ClosePrice'].diff()
seasonal_period = 288
data['Seasonal_Differenced'] = data['ClosePrice'].diff(seasonal_period)
data['Log_Transformed'] = np.log(data['ClosePrice'])
data.dropna(inplace=True)

# Plot and print each transformed column individually
columns_to_plot = {
    'Original Data': 'ClosePrice',
    'Regular Differencing': 'Differenced',
    'Seasonal Adjustment': 'Seasonal_Differenced',
    'Log Transformation': 'Log_Transformed'
}

for title, column in columns_to_plot.items():
    plt.figure(figsize=(10, 4))
    plt.plot(data[column], label=title)
    plt.title(title)
    plt.legend()
    plt.show()
    print(f"{title}:\n", data[column].head())
```


### OUTPUT:
![image](https://github.com/user-attachments/assets/fb93a37e-e76a-4574-a4c8-caa56abf392b)

REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/f538312e-e014-4bd0-9e04-9de54eea02b8)

SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/fee64860-a711-4361-832d-52e5eb5f5187)

LOG TRANSFORMATION:
![image](https://github.com/user-attachments/assets/9bbb6c2a-f77f-42ce-884a-925b1365ee96)


### RESULT:
Thus we have created the python code for the conversion of XAUUAE data.
