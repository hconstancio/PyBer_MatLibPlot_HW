
# PyBer Ride Sharing

# Analysis
1. There are more rides on a populated area (Urban), and the fare is lower than the other type of cities.
2. The fares are higher on rural cities with less amount of rides and drivers.
3. The higher concentration of rides are between 15 & 30 rides.
4. The majority of the amount of the fares are spent in the Urban area even though they are not the most expensive ones. 
5. As it was expected there are much more drivers (~90%) in the populated area (Urban) than any of the other type of cities.


```python
# -----------------------------------------------------------------------------------------
# Your objective is to build a [Bubble Plot](https://en.wikipedia.org/wiki/Bubble_chart) 
# that showcases the relationship between four key variables:
# * Average Fare ($) Per City
# * Total Number of Rides Per City
# * Total Number of Drivers Per City
# * City Type (Urban, Suburban, Rural
```


```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import csv
import os
```


```python
# Getting the data from file One --> (city_Data)
city_data_df = pd.read_csv('raw_data/city_data.csv')
city_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Remove any duplicated Data
city_data_df = city_data_df.drop_duplicates('city', keep = 'first')
```


```python
# Getting the data from file two --> (ride_Data)
ride_data_df = pd.read_csv('raw_data/ride_data.csv')
ride_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Combine - Merge both files based on the city
combined_pyber_df = pd.merge(city_data_df, ride_data_df,
                                 how='outer', on='city')
combined_pyber_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get the Average Fare ($) Per City: 
# Group the merged DataFrame by City
grouped_city = combined_pyber_df.groupby('city')
```


```python
# Get the mean of Fare from the grouped Data Frame
average_city = grouped_city['fare'].mean()
```


```python
# Just rpound the average fare by city to two decimals
average_city = round(average_city,2)
#average_city
```


```python
# Getting the total Number of Rides Per City by used the grouped Data Frame and using Count
rides_per_city = grouped_city['ride_id'].count()
#rides_per_city
```


```python
# Obtain the Total Number of Drivers Per City using the same grouped data frame and getting the mean
drivers_per_city = grouped_city['driver_count'].mean()
#drivers_per_city
```


```python
# Use the original Data Frame (cities.csv)  file and set the index to city type and assign to zone  
# City Type (Urban, Suburban, Rural)
zone = city_data_df.set_index('city')['type']
#zone
```


```python
# Create a DataFrame with the information that has been previously obtained and sort it by Zone Type
city_info = pd.DataFrame({
                "Number Of Rides": rides_per_city,
                "Average Fare": average_city,
                "Drivers Per City": drivers_per_city,
                "Zone Type": zone
})
city_info.sort_values('Zone Type', ascending = True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Fare</th>
      <th>Drivers Per City</th>
      <th>Number Of Rides</th>
      <th>Zone Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>East Troybury</th>
      <td>33.24</td>
      <td>3</td>
      <td>7</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>West Kevintown</th>
      <td>21.53</td>
      <td>5</td>
      <td>7</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>East Stephen</th>
      <td>39.05</td>
      <td>6</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>East Leslie</th>
      <td>33.66</td>
      <td>9</td>
      <td>11</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Hernandezshire</th>
      <td>32.00</td>
      <td>10</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>South Joseph</th>
      <td>38.98</td>
      <td>3</td>
      <td>12</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Horneland</th>
      <td>21.48</td>
      <td>8</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Jacksonfort</th>
      <td>32.01</td>
      <td>6</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Erikport</th>
      <td>30.04</td>
      <td>3</td>
      <td>8</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>North Whitney</th>
      <td>38.15</td>
      <td>10</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>South Elizabethmouth</th>
      <td>28.70</td>
      <td>3</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Stevensport</th>
      <td>31.95</td>
      <td>6</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Matthewside</th>
      <td>43.53</td>
      <td>4</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Kennethburgh</th>
      <td>36.93</td>
      <td>3</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Shelbyhaven</th>
      <td>34.83</td>
      <td>9</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Manuelchester</th>
      <td>49.62</td>
      <td>7</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>Kinghaven</th>
      <td>34.98</td>
      <td>3</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>New Johnbury</th>
      <td>35.04</td>
      <td>6</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>South Shannonborough</th>
      <td>26.52</td>
      <td>9</td>
      <td>15</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>New Cindyborough</th>
      <td>31.03</td>
      <td>20</td>
      <td>13</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>Martinmouth</th>
      <td>30.50</td>
      <td>5</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>New Jessicamouth</th>
      <td>32.81</td>
      <td>22</td>
      <td>17</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>New Brandonborough</th>
      <td>31.90</td>
      <td>9</td>
      <td>14</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>New Samanthaside</th>
      <td>34.07</td>
      <td>16</td>
      <td>23</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>Thomastown</th>
      <td>30.31</td>
      <td>1</td>
      <td>24</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>New Michelleberg</th>
      <td>24.97</td>
      <td>9</td>
      <td>11</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>South Jennifer</th>
      <td>29.80</td>
      <td>6</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>North Tara</th>
      <td>32.39</td>
      <td>14</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>North Tracyfort</th>
      <td>26.86</td>
      <td>18</td>
      <td>10</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>South Gracechester</th>
      <td>31.35</td>
      <td>19</td>
      <td>19</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Davidtown</th>
      <td>22.98</td>
      <td>73</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Carrollfort</th>
      <td>25.40</td>
      <td>55</td>
      <td>29</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Arnoldview</th>
      <td>25.11</td>
      <td>41</td>
      <td>31</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.98</td>
      <td>49</td>
      <td>19</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.62</td>
      <td>21</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.61</td>
      <td>67</td>
      <td>26</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Lake Jennaton</th>
      <td>25.35</td>
      <td>65</td>
      <td>25</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Lake Sarashire</th>
      <td>26.61</td>
      <td>8</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Lake Stevenbury</th>
      <td>24.66</td>
      <td>63</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Lisatown</th>
      <td>22.23</td>
      <td>47</td>
      <td>23</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Prattfurt</th>
      <td>23.35</td>
      <td>43</td>
      <td>24</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Port Samantha</th>
      <td>27.05</td>
      <td>55</td>
      <td>27</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Port Martinberg</th>
      <td>22.33</td>
      <td>44</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Port Josephfurt</th>
      <td>26.37</td>
      <td>28</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Port Johnstad</th>
      <td>25.88</td>
      <td>22</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Pearsonberg</th>
      <td>23.31</td>
      <td>43</td>
      <td>20</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Pamelahaven</th>
      <td>25.55</td>
      <td>30</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Nguyenbury</th>
      <td>25.90</td>
      <td>8</td>
      <td>26</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Russellport</th>
      <td>22.49</td>
      <td>9</td>
      <td>23</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Yolandafurt</th>
      <td>27.21</td>
      <td>7</td>
      <td>20</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New Jeffrey</th>
      <td>24.13</td>
      <td>58</td>
      <td>25</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New David</th>
      <td>27.08</td>
      <td>31</td>
      <td>28</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New Christine</th>
      <td>24.16</td>
      <td>22</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New Andreamouth</th>
      <td>24.97</td>
      <td>42</td>
      <td>28</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New Aaron</th>
      <td>26.86</td>
      <td>60</td>
      <td>22</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Mooreview</th>
      <td>29.52</td>
      <td>34</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Maryside</th>
      <td>26.84</td>
      <td>20</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Lisaville</th>
      <td>28.43</td>
      <td>66</td>
      <td>28</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>New Maryport</th>
      <td>28.47</td>
      <td>26</td>
      <td>20</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Zimmermanmouth</th>
      <td>28.30</td>
      <td>45</td>
      <td>24</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 4 columns</p>
</div>




```python
# Assign variables to the different Types of Zones within the cities
urban = city_info[city_info["Zone Type"] == "Urban"]
rural = city_info[city_info["Zone Type"] == "Rural"]
suburban = city_info[city_info["Zone Type"] == "Suburban"]
```

# Bubble Plot Of Ride Sharing Data


```python
# Creating base chart - Including chart tittle, axis labels, notation
plt.suptitle("Pyber Ride Sharing Data (2016)")
plt.title("Note: Circle size correlate with driver count p/city")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
# Add the Grid and use gray as the grid Color
plt.rc('grid', linestyle="-", color='gray')
plt.grid(True)
# Create the actual Bubble Chart
x_urban= urban['Number Of Rides']
y_urban= urban['Average Fare']
drivers_urban = urban['Drivers Per City']
x_rural= rural['Number Of Rides']
y_rural= rural['Average Fare']
drivers_rural = rural['Drivers Per City']
x_suburban= suburban['Number Of Rides']
y_suburban= suburban['Average Fare']
drivers_suburban = suburban['Drivers Per City']
plt.scatter(x_urban, y_urban, s = drivers_urban * 10, c="lightcoral", edgecolor= "black", linewidth=1, 
            alpha = 0.75, label = "Urban")
plt.scatter(x_rural, y_rural, s = drivers_rural * 10, c="gold", edgecolor= "black", linewidth=1, alpha = 0.75, 
           label = "Rural")
plt.scatter(x_suburban, y_suburban, s = drivers_suburban * 10, c="lightskyblue", edgecolor= "black", linewidth=1, 
            alpha = 0.75, label = "Suburban")
plt.legend()
plt.show()
```


![png](output_17_0.png)



```python
#In addition, you will be expected to produce the following three pie charts:
#* % of Total Fares by City Type
#* % of Total Rides by City Type
#* % of Total Drivers by City Type
```


```python
# Create basic data for Pie Charts
```


```python
# Create a Data Frame by grouping the Merged Data Frame by City Type uisng the required data 
# --> This will be used on the pie charts
grp_by_city_type = combined_pyber_df.groupby('type')['type', 'fare', 'ride_id', 'driver_count']
#grp_by_city_type.head()
```


```python
# Get the total fare by City Type
total_fare = grp_by_city_type.sum()['fare']
#total_fare.head()
```

# Total Fares By City Type


```python
# Create the First pie chart
labels = total_fare.index
# Formatting the pie chart according to the requirements
colors = ["gold", "lightskyblue", "lightcoral"]
explode = (0.1, 0.1, 0)
# Create the Pie Chart
plt.pie(total_fare, explode = explode, labels = labels, colors = colors,
        autopct="%1.1f%%", shadow=True, startangle=140, wedgeprops = {'linewidth': 1.5, 'edgecolor': 'darkgray'})
# Show the Pie Chart
plt.title("% Of Total Fares by City Type")
plt.show
```




    <function matplotlib.pyplot.show>




![png](output_23_1.png)


# Total Rides By City Type


```python
# Get the total Rides by City Type
total_ride = grp_by_city_type.count()['ride_id']
#total_ride.head()
```


```python
# Create the Second pie chart
labels = total_ride.index
# Formatting the pie chart according to the requirements
colors = ["gold", "lightskyblue", "lightcoral"]
explode = (0.1, 0.1, 0)
# Create the Pie Chart
plt.pie(total_ride, explode = explode, labels = labels, colors = colors,
        autopct="%1.1f%%", shadow=True, startangle=90, wedgeprops = {'linewidth': 1, 'edgecolor': 'darkgray'})
# Show the Pie Chart
plt.title("% Of Total Rides by City Type")
plt.axis("equal")
plt.show
```




    <function matplotlib.pyplot.show>




![png](output_26_1.png)


# Total Drivers By City Type


```python
# Get the total Drivers by City Type
total_drivers = grp_by_city_type.sum()['driver_count']
#total_drivers.head()
```


```python
# Create the Third pie chart
labels = total_drivers.index
# Formatting the pie chart according to the requirements
colors = ["gold", "lightskyblue", "lightcoral"]
explode = (0.2, 0.2, 0.1)
# Create the Pie Chart
plt.pie(total_drivers, explode = explode, labels = labels, colors = colors,
        autopct="%1.1f%%", shadow=True, startangle=120, wedgeprops = {'linewidth': 0.5, 'edgecolor': 'darkgray'})
# Show the Pie Chart
plt.title("% Of Total Drivers by City Type")
plt.axis("equal")
plt.show
```




    <function matplotlib.pyplot.show>




![png](output_29_1.png)

