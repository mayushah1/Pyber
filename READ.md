
## Option 1: Pyber

![Ride](Images/Ride.png)

The ride sharing bonanza continues! Seeing the success of notable players like Uber and Lyft, you've decided to join a fledgling ride sharing company of your own. In your latest capacity, you'll be acting as Chief Data Strategist for the company. In this role, you'll be expected to offer data-backed guidance on new opportunities for market differentiation.

You've since been given access to the company's complete recordset of rides. This contains information about every active driver and historic ride, including details like city, driver count, individual fares, and city type.

Your objective is to build a [Bubble Plot](https://en.wikipedia.org/wiki/Bubble_chart) that showcases the relationship between four key variables:

* Average Fare ($) Per City
* Total Number of Rides Per City
* Total Number of Drivers Per City
* City Type (Urban, Suburban, Rural)

In addition, you will be expected to produce the following three pie charts:

* % of Total Fares by City Type
* % of Total Rides by City Type
* % of Total Drivers by City Type

As final considerations:

* You must use the Pandas Library and the Jupyter Notebook.
* You must use the Matplotlib and Seaborn libraries.
* You must include a written description of three observable trends based on the data.
* You must use proper labeling of your plots, including aspects like: Plot Titles, Axes Labels, Legend Labels, Wedge Percentages, and Wedge Labels.
* Remember when making your plots to consider aesthetics!
  * You must stick to the Pyber color scheme (Gold, Light Sky Blue, and Light Coral) in producing your plot and pie charts.
  * When making your Bubble Plot, experiment with effects like `alpha`, `edgecolor`, and `linewidths`.
  * When making your Pie Chart, experiment with effects like `shadow`, `startangle`, and `explosion`.
* You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.
* See [Example Solution](Pyber/Pyber_Example.pdf) for a reference on expected format.



# Pyber Ride Sharing


## Analysis
### Observed Trend 1 
There are more number of drivers and rides in the Urban area compared with Suburban and Rural

### Observed Trend 2 
1% of total drivers in Rural area earns 6.6% of total fare revenue.

### Observed Trend 3
Suburban makes half of the Urban revenue  "$20k" comapred with $40k" with 13% of total drivers 



```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import os
```


```python
# Read combined csv file
csvpath = os.path.join( 'raw_Data', 'city_data.csv')
csvpath1 = os.path.join( 'raw_Data', 'ride_data.csv')
city_df = pd.read_csv(csvpath)
ride_df = pd.read_csv(csvpath1)
```


```python
city_df.head()
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
ride_df.head()
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
combined = pd.merge(city_df,ride_df, on="city", how="outer")
```


```python
combined.head()
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
#create variables for city type, used for scatter plot
urban=combined[combined["type"]=="Urban"]
suburban=combined[combined["type"]=="Suburban"]
rural=combined[combined["type"]=="Rural"]
```


```python
# Create counts for rides, fares and drivers
urban_ride=urban.groupby(["city"]).count()["ride_id"]
urban_fare=urban.groupby(["city"]).mean()["fare"]
urban_driver=urban.groupby(["city"]).mean()["driver_count"]

suburban_ride=suburban.groupby(["city"]).count()["ride_id"]
suburban_fare=suburban.groupby(["city"]).mean()["fare"]
suburban_driver=suburban.groupby(["city"]).mean()["driver_count"]

rural_ride=rural.groupby(["city"]).count()["ride_id"]
rural_fare=rural.groupby(["city"]).mean()["fare"]
rural_driver=rural.groupby(["city"]).mean()["driver_count"]



```


```python
#Put a scatter chart for all variables
plt.title("Pyber Ride Sharing Data (2016)")
plt.ylabel("Average Fare $")
plt.xlabel("Total Number of Rides")
plt.grid(True)

plt.xlim((0, 38))
plt.scatter(urban_ride,urban_fare,linewidth=1, marker="o", color="gold", alpha=0.7, 
            label="Urban", s=urban_driver*8, edgecolor = "black")
plt.scatter(suburban_ride,suburban_fare,linewidth=1, marker="o", color="lightskyblue", alpha=0.8, 
            label="Suburban",s=suburban_driver*8,edgecolor = "blue" )
plt.scatter(rural_ride,rural_fare,linewidth=1, marker="o", color="lightcoral", alpha=0.9, 
            label="Rural",s=rural_driver*8,edgecolor = "brown")
plt.legend(loc="best")
plt.savefig("Pyber Ride Sharing Data.png")
plt.show()
```


![png](output_11_0.png)



```python
# Total fare by city type
city_type = combined.groupby("type")["fare"].sum().reset_index()
city_type
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
      <th>type</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>4255.09</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>20335.69</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>40078.34</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.pie(city_type["fare"], labels=city_type["type"],colors=["lightcoral","lightskyblue","gold"],
        shadow=True,explode = (0.1,0.05,.1), autopct= "%1.1f%%")
plt.title('Total Fare by City Type')
plt.savefig("Total Fare by city.png")
plt.show()
```


![png](output_13_0.png)



```python
#Total ride per city type
city_ride = combined.groupby("type")["fare"].count().reset_index()
```


```python
city_ride
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
      <th>type</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>657</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.pie(city_ride["fare"], labels=city_type["type"],colors=["lightcoral","lightskyblue","gold"],
        shadow=True,explode = (0.1,0.05,.1), autopct= "%1.1f%%")
plt.title('Total Rides by City Type')
plt.savefig("Total Rides by city.png")
plt.show()
```


![png](output_16_0.png)



```python
#Total driver per city type
city_driver = combined.groupby("type")["driver_count"].sum().reset_index()
```


```python
city_driver
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
      <th>type</th>
      <th>driver_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>727</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>9730</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>64501</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.pie(city_driver["driver_count"], labels=city_type["type"],colors=["lightcoral","lightskyblue","gold"],
        shadow=True,explode = (0.1,0.1,0.1), autopct= "%1.1f%%")
plt.title('Total Drivers by City Type')
plt.savefig("Total Drivers by city.png")
plt.show()
```


![png](output_19_0.png)

