# Surfs_up
## Overview
Analysis of weather for starting up a local surfing supply store. In order to determine if the surf and ice cream shop business is sustainable year-round, perform an analysis for the weather in Oahu.

## Results
### Comparision of the temperature in different seasons.
- **Statistic**
<table>
<tr><th>June Temperature </th><th>December Temperature</th></tr>
<tr><td>

| count | 1700.000000 |
| -----| ----------- |
| mean | 74.944118 | 
| std | 3.257417 | 
| min | 64.000000 | 
| 25% | 73.000000 | 
| 50% | 75.000000 | 
| 75% | 77.000000 | 
| max | 85.000000 | 

</td><td>
  
count | 1517.000000 |
-----| ----------- |
mean | 71.041529 | 
std | 3.745920 | 
min | 56.000000 | 
25% | 69.000000 | 
50% | 71.000000 | 
75% | 74.000000 | 
max | 83.000000 | 

</td></tr> </table>

- **Temperaturs Frequency**

![temp_fig](https://user-images.githubusercontent.com/66225050/130332733-5913e906-092c-491d-99b6-8ff300a5fcad.png)

- The average tempurature during June and December are similar in Oahu, only appx. 3°F difference.
- During June and December, the temperatures are mostly in between **70°F** and **80°F**.
- The lowest temperature was recored in December at **56°F**. And the highest temperatrue recorded in June at **85°F**, but it is only 2°F higher than the highest temperature in December, 83°F. 

### Summary
- Oahu has a pretty stady temperature. There is only few Fahrenheit different between June and December. 
- Add additional query to the database:
  ```python
  jun_prcp = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date) == 6).all()
  dec_prcp = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date) == 12).all()
  jun_prcp_df = pd.DataFrame(jun_prcp, columns=['date','precipitation'])
  jun_prcp_df.describe()
  dec_prcp_df = pd.DataFrame(dec_prcp, columns=['date','precipitation'])
  dec_prcp_df.describe()
  
  # Plot rain frequency
  ax = jun_prcp_df.plot.hist(bins=15,alpha = 0.8)
  dec_prcp_df.plot.hist(bins=15, alpha=0.8, ax=ax)
  ax.set_title('Precipitation Comparison for June and December', fontsize=15)
  ax.set_xlabel('Precipitation')
  ax.set_xlim(0,2)
  ax.legend(['June','December'])
  ax.grid()
  plt.savefig("./Resources/prcp_fig.png")
  ```
- We get table and plot figure for rain in Oahu as below:
<table>
<tr><th>June Precipitation </th><th>December Precipitation</th></tr>
<tr><td>

| count | 1574.000000 |
| -----| ----------- |
| mean | 0.136360 | 
| std | 0.335731 | 
| min | 0.000000 | 
| 25% | 0.000000 | 
| 50% | 0.020000 | 
| 75% | 0.120000 | 
| max | 4.430000 | 

</td><td>
  
count | 1405.000000 |
-----| ----------- |
mean | 0.216819 | 
std | 0.541399 | 
min | 0.000000 | 
25% | 0.000000 | 
50% | 0.030000 | 
75% | 0.150000 | 
max | 6.420000 | 

</td></tr> </table>

![prcp_fig](https://user-images.githubusercontent.com/66225050/130338706-fb49bb7d-77fc-44d2-bf98-bd2383973c46.png)

- From the tables and figure above. Comparing the rainfall intensity, there should be a little chance in Oahu raining heavily. If there is, it could be the due to the tropical storm. But these high rainfall is outline of the whole dataset. The majority of precipitation in Oahu is lower than 0.15. Thus, the rainfall should cause low impact to the ice cream and surf store as well.
