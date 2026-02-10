# EXP 3 - Delhi Air Quality Analysis**

**Aim**
To compare air quality parameters in Delhi across different stations and analyze the relationship between pollutants (e.g., PM2.5 and NO₂) using scatter plots and correlation analysis.


**Procedure / Algorithm**

1)Load the dataset using pandas.

2)Preprocess the data:

3)Convert the date column (period.datetimeFrom.utc) to datetime format.

4)Drop missing or invalid values.

5)Pivot the dataset so each pollutant (parameter) becomes a separate column.

6)Plot scatter plot between PM2.5 and NO₂ to study their relationship.

7)Plot correlation heatmap between all pollutants to identify relationships.

8)Interpret the results — identify which pollutants are correlated and which stations are most polluted.


**Program**
1) Load dataset & show summary
```
import pandas as pd
import matplotlib.pyplot as plt
print("NAME:KIRAN MP")
print("REG NO:212224230123")
df = pd.read_csv("delhi_pm25_aqi.csv")

display(df.head())
print("\nData Types:\n", df.dtypes)
print("\nNull Counts:\n", df.isnull().sum())
```

2) Clean the data

```
print("NAME:KIRAN MP")
print("REG NO:212224230123")
df_clean = df.copy()

df_clean['datetime'] = pd.to_datetime(
    df_clean['period.datetimeFrom.utc'], 
    errors='coerce'
)

df_clean['pm25'] = pd.to_numeric(df_clean['value'], errors='coerce')

df_clean = df_clean.dropna(subset=['datetime', 'pm25'])
```

3) Add date, month, hour columns
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")

df_clean['date'] = df_clean['datetime'].dt.date
df_clean['month'] = df_clean['datetime'].dt.month
df_clean['hour'] = df_clean['datetime'].dt.hour

display(df_clean.head())
```

4) Monthly boxplots of PM2.5
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")
plt.figure()
df_clean.boxplot(column='pm25', by='month')
plt.title("Monthly PM2.5 Distribution")
plt.suptitle("")
plt.xlabel("Month")
plt.ylabel("PM2.5 (µg/m³)")
plt.show()
```

5) Monthly average PM2.5
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")
monthly_avg = df_clean.groupby('month')['pm25'].mean()

plt.figure()
monthly_avg.plot(kind='bar')
plt.title("Monthly Average PM2.5")
plt.xlabel("Month")
plt.ylabel("Average PM2.5 (µg/m³)")
plt.show()
```

6) WHO PM2.5 limit exceedance analysis
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")
WHO_LIMIT = 25

daily_avg = df_clean.groupby('date')['pm25'].mean()
exceed_days = daily_avg[daily_avg > WHO_LIMIT]

num_exceed_days = exceed_days.count()
total_days = daily_avg.count()
percentage_exceed = (num_exceed_days / total_days) * 100

print("Days exceeding WHO limit:", num_exceed_days)
print("Percentage of days exceeding WHO limit:", percentage_exceed)
```

7) Average PM2.5 vs hour of day
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")

hourly_avg = df_clean.groupby('hour')['pm25'].mean()

plt.figure()
hourly_avg.plot()
plt.title("Average PM2.5 by Hour of Day")
plt.xlabel("Hour of Day")
plt.ylabel("Average PM2.5 (µg/m³)")
plt.show()
```

8) Top 5 worst-polluted days
```
print("NAME:KIRAN MP")
print("REG NO:212224230123")

top_5_worst_days = daily_avg.sort_values(ascending=False).head(5)

print("Top 5 Worst Polluted Days:")
display(top_5_worst_days)
```

9)Write a brief paragraph interpreting seasonal and daily trends and what those imply for public health.

Air pollution in Delhi exhibits strong seasonal and daily variations with important implications for public health. Pollution levels increase significantly during the winter months, particularly in November and December, as cooler temperatures and temperature inversions trap pollutants near the surface, while emissions from traffic, biomass burning, and other human activities intensify the problem. In contrast, air quality improves during the monsoon season, when rainfall helps remove particulate matter from the atmosphere. On a daily scale, PM2.5 concentrations tend to peak during late-night and early-morning hours and decline around midday, when higher temperatures, sunlight, and wind promote dispersion. From a public health perspective, these patterns are concerning because air pollution frequently exceeds recommended safety limits, leading to continuous exposure. Prolonged exposure to such conditions increases the risk of respiratory and cardiovascular diseases and disproportionately affects vulnerable populations such as children, the elderly, and individuals with pre-existing health conditions. These trends highlight the urgent need for targeted pollution-control measures and public health interventions, especially during winter months and high-risk hours.

**Output**
1) Load dataset & show summary
<img width="779" height="547" alt="image" src="https://github.com/user-attachments/assets/549b56e2-40d9-4bf2-a085-6a14ea1a9078" />


2) Clean the data
<img width="777" height="224" alt="image" src="https://github.com/user-attachments/assets/8ba398ff-7f96-4a60-9d61-d823f4a9b7fe" />


3) Add date, month, hour columns
<img width="778" height="317" alt="image" src="https://github.com/user-attachments/assets/bbc550e7-a817-4533-a974-5164c82aedc3" />


4) Monthly boxplots of PM2.5
<img width="779" height="575" alt="image" src="https://github.com/user-attachments/assets/7031225e-e839-424d-a80b-1f376775e3c6" />


5) Monthly average PM2.5
<img width="773" height="583" alt="image" src="https://github.com/user-attachments/assets/4b297e9e-1472-4960-a3cb-2c0fd4af05a5" />


6) WHO PM2.5 limit exceedance analysis
<img width="769" height="269" alt="image" src="https://github.com/user-attachments/assets/5aec7d2b-e646-43b8-980c-f14e080dbe50" />


7) Average PM2.5 vs hour of day
<img width="768" height="587" alt="image" src="https://github.com/user-attachments/assets/443087cb-b8d0-4151-bb0f-e4d81544f5fd" />


8) Top 5 worst-polluted days
<img width="771" height="286" alt="image" src="https://github.com/user-attachments/assets/a83f6c0b-701f-4026-a01f-abc8230ebb66" />



**Interpretation**

1)PM10 and PM2.5 show a strong positive correlation, indicating that both coarse and fine particulate matter often originate from common sources such as road dust, construction activities, and traffic emissions.

NO₂ and CO exhibit a positive correlation, suggesting that both pollutants are primarily emitted from incomplete combustion processes, especially motor vehicles and diesel generators.

2)Air pollution in Delhi shows strong seasonal and daily patterns that have serious implications for public health. Pollution levels increase sharply during the winter months, particularly in November and December, when cold temperatures trap pollutants near the ground and emissions from activities such as burning and heavy traffic intensify air quality problems. In contrast, pollution levels decrease during the monsoon season, as rainfall helps remove particulate matter from the atmosphere. On a daily basis, PM2.5 concentrations are typically highest late at night and in the early morning, and lowest around midday, when sunlight and wind aid in dispersing pollutants.

**Result**

The dataset was successfully loaded and processed to extract pollutant-wise and station-wise air quality data for Delhi.


