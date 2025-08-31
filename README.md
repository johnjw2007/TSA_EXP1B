## Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
## Date: 31.08.2025
## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Gold prediction data(XAUUAE data).

## ALGORITHM:
Import the required packages like pandas and numpy
Read the data using the pandas
Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
Display the overall results.
PROGRAM:
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

## Load the CSV file
data = pd.read_csv('XAUUSD_2010-2023.csv')

## Select only the 'time' and 'close' columns
data = data[['time', 'close']]
data.rename(columns={'close': 'ClosePrice'}, inplace=True)

## Convert 'time' column to datetime format
data['time'] = pd.to_datetime(data['time'], format='%d-%m-%Y %H:%M')

## Set 'time' as the index
data.set_index('time', inplace=True)

## Perform transformations
data['Differenced'] = data['ClosePrice'].diff()
seasonal_period = 288
data['Seasonal_Differenced'] = data['ClosePrice'].diff(seasonal_period)
data['Log_Transformed'] = np.log(data['ClosePrice'])
data.dropna(inplace=True)

## Plot and print each transformed column individually
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
    
## OUTPUT:
<img width="1119" height="639" alt="image" src="https://github.com/user-attachments/assets/bf4d3a22-2f22-4a2e-b861-6aba9332af17" />

## REGULAR DIFFERENCING: 
<img width="1093" height="638" alt="image" src="https://github.com/user-attachments/assets/fd84c288-9e10-492d-90d7-c8219a7ddc53" />

## SEASONAL ADJUSTMENT: 
<img width="1053" height="638" alt="image" src="https://github.com/user-attachments/assets/852dbf23-cc5c-4b22-b7b3-d7d1ac7f3ae6" />

## LOG TRANSFORMATION: 
<img width="1065" height="634" alt="image" src="https://github.com/user-attachments/assets/26135ba6-c71e-4263-bb88-a7a6c5a14a73" />

## RESULT:
Thus we have created the python code for the conversion of XAUUAE data.
