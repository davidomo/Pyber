
## Pyber - A python-driven look at a Ride Sharing Company, Pyber

##### Noticable trends #####

1. Urban cities have the lowest ceiling on average fare. In Urban areas, trips are more likely to be shorter but happen at a higher frequency. The opposite happens to Rural cities: fewer rides that rack up, on average, a higher price per ride. Suburban cities are between the two extremes of Rural and Urban. Suburban have a lower ride count than Urban while having a higher average price per ride. 

2. Urban areas included in this data set are bunched closer than the other two city types. This means that drivers would not greatly benefit from changing which Urban city they find their riders. Driving outside an Urban city and moving to the Suburbs does not implicitly mean a higher wage for the driver however because there is a larger spread in Suburban areas for total rides needed on average.

3. Urban drivers are the only type to have an inverse relationship between the percentage of drivers to riders. Rural and Suburban drivers have the advantage of having a smaller pool of drivers to get a larger portion of the company's total rides. This means that these drivers have a higher chance to obtain more individual rides than their counterparts in Urban settings. This relationship does not correlate to pure profit for individual drivers, however, since we do not have the data for average trip length, average cost of gasoline, average miles per gallon each driver has, ect. for new drivers to plan on where they would succeed most. For this reason, I would suggest an increase in exposure to Suburban areas as they have a higher price per ride, only really missing a higher demand for rides unlike Urban areas.


```python
# Dependencies
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```


```python
file = "raw_data/city_data.csv"
file2 = "raw_data/ride_data.csv"
rawcity_df = pd.read_csv(file)
rawcity_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
rawride_df = pd.read_csv(file2)
rawride_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
rawcomb_df = pd.merge(rawcity_df, rawride_df)
rawcomb_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
grouped = rawcomb_df.groupby("city")
grouped.count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Bubble Calc
AverageFare = grouped["fare"].mean()
TotalRides = grouped["ride_id"].count()
drivercount = grouped["driver_count"].sum()
TotalDriver = (drivercount // TotalRides)

Types = rawcity_df.groupby("type")

Scatt = pd.DataFrame({"AverageFare": AverageFare,
                        "TotalRides": TotalRides,
                        "TotalDrivers": TotalDriver})

Scatt["AverageFare"] = Scatt["AverageFare"].round(2)
Scatt.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AverageFare</th>
      <th>TotalDrivers</th>
      <th>TotalRides</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.93</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.61</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.32</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.62</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.98</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Make new DF based on Type
Urban = rawcomb_df.loc[rawcomb_df["type"] == "Urban", :]
Sub = rawcomb_df.loc[rawcomb_df["type"] == "Suburban", :]
Rural = rawcomb_df.loc[rawcomb_df["type"] == "Rural"]

# Group new DF by city name
GUrban = Urban.groupby("city")
GSub = Sub.groupby("city")
GRural = Rural.groupby("city")

# Bubble Calc
AverageFare = grouped["fare"].mean()
TotalRides = grouped["ride_id"].count()
drivercount = grouped["driver_count"].sum()
TotalDriver = (drivercount // TotalRides)

# Urban Data Manipulation
UFare = GUrban["fare"].mean()
URides = GUrban["ride_id"].count()
Ucount = GUrban["driver_count"].sum()
UDriver = (Ucount // URides)

# Suburban Data Manipulation
SFare = GSub["fare"].mean()
SRides = GSub["ride_id"].count()
Scount = GSub["driver_count"].sum()
SDriver = (Scount // SRides)

# Rural Data Manipulation
RFare = GRural["fare"].mean()
RRides = GRural["ride_id"].count()
Rcount = GRural["driver_count"].sum()
RDriver = (Rcount // RRides)
```


```python
# Make new DFs for plotting
FUrban = pd.DataFrame({"AverageFare": UFare,
                       "TotalRides": URides,
                       "TotalDrivers": UDriver})
FUrban["AverageFare"] = FUrban["AverageFare"].round(2)

FSub = pd.DataFrame({"AverageFare": SFare,
                     "TotalRides": SRides,
                     "TotalDrivers": SDriver})
FSub["AverageFare"] = FSub["AverageFare"].round(2)

FRural = pd.DataFrame({"AverageFare": RFare,
                       "TotalRides": RRides,
                       "TotalDrivers": RDriver})
FRural["AverageFare"] = FRural["AverageFare"].round(2)
```


```python
# Bubble Plot
ChangeBubbleSize = 12
CBS = ChangeBubbleSize
plt.figure(figsize=(8,7))
BubUr = plt.scatter(FUrban.TotalRides, FUrban.AverageFare, c="lightskyblue", label = "Urban", 
                    s=(FUrban.TotalDrivers * CBS), alpha = 0.6, edgecolor = "black", linewidths = .6)

# Bubble Plot
BubSu = plt.scatter(FSub.TotalRides, FSub.AverageFare, c="gold", label = "Suburban", 
                    s=(FSub.TotalDrivers * CBS), alpha = 0.6, edgecolor = "black", linewidths = .9)

# Bubble Plot
BubRu = plt.scatter(FRural.TotalRides, FRural.AverageFare, c="lightcoral", label = "Rural", 
                    s=(FRural.TotalDrivers * CBS), alpha = 0.65, edgecolor = "black", linewidths = 1)

lgnd = plt.legend(handles=[BubUr, BubSu, BubRu], scatterpoints=1, fontsize=16)
lgnd.legendHandles[0]._sizes = [150]
lgnd.legendHandles[1]._sizes = [150]
lgnd.legendHandles[2]._sizes = [150]
plt.title("Pyber Ride Sharing Data")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.figtext(.95, .5, "Note: \nCircle size correlates \nwith driver count per city", fontsize=12)

# To not display "outliers", uncomment these two lines below
#plt.xlim(2,40)
#plt.ylim(15,45)

plt.savefig("Figures/Ride_Sharing_Data.png")
plt.show()
```


![png](output_9_0.png)



```python
# Pie Charts Data
TypeGrouped = rawcomb_df.groupby("type")
TypeGrouped_Raw = rawcity_df.groupby("type")

# Pice Chart #1
FareTotal = rawcomb_df["fare"].sum()
GroupedFare = TypeGrouped["fare"].sum()

GFTotal = GroupedFare / FareTotal

# Pie Chart #2
RideTotal = rawcomb_df["ride_id"].count()
GroupedRide = TypeGrouped["ride_id"].count()

GRTotal = GroupedRide / RideTotal

# Pie Chart #3
DriverTotal = rawcity_df["driver_count"].sum()
GroupedDriver = TypeGrouped_Raw["driver_count"].sum()

GDTotal = GroupedDriver / DriverTotal

print(GFTotal)
print(GRTotal)
print(GDTotal)
```

    type
    Rural       0.065798
    Suburban    0.314458
    Urban       0.619745
    Name: fare, dtype: float64
    type
    Rural       0.051932
    Suburban    0.272954
    Urban       0.675114
    Name: ride_id, dtype: float64
    type
    Rural       0.031054
    Suburban    0.190505
    Urban       0.778441
    Name: driver_count, dtype: float64
    


```python
# Pie Chart #1: Total Fare
explode = (0, 0, 0.15)
labels = GFTotal.index.tolist()
colors = ["lightcoral", "gold", "lightskyblue"]
plt.figure(figsize=(6,6))
plt.rcParams['font.size'] = 13.0
plt.pie(GFTotal, labels = labels, explode = explode, colors = colors, startangle = 265, shadow = True, autopct="%1.2f%%")
plt.axis("equal")
plt.title("Percentage of Total Fare by City Type")
plt.xlabel("City Types")
plt.ylabel("Percentage of Fares")
plt.savefig("Figures/Total_Fares.png")
plt.show()
```


![png](output_11_0.png)



```python
# Pie Chart #2: Total Rides
explode = (0, 0, 0.15)
labels = GRTotal.index.tolist()
colors = ["lightcoral", "gold", "lightskyblue"]
plt.figure(figsize=(6,6))
plt.rcParams['font.size'] = 13.0
plt.pie(GRTotal, labels = labels, explode = explode, colors = colors, startangle = 275, shadow = True, autopct="%1.2f%%")
plt.axis("equal")
plt.title("Percentage of Total Rides by City Type")
plt.xlabel("City Types")
plt.ylabel("Percentage of Rides")
plt.savefig("Figures/Total_Rides.png")
plt.show()
```


![png](output_12_0.png)



```python
# Pie Chart #3: Total Drivers
explode = (0, 0, 0.15)
labels = GDTotal.index.tolist()
colors = ["lightcoral", "gold", "lightskyblue"]
plt.figure(figsize=(6,6))
plt.rcParams['font.size'] = 13.0
plt.pie(GDTotal, labels = labels, explode = explode, colors = colors, startangle = 275, shadow = True, autopct="%1.2f%%", labeldistance=1.07)
plt.axis("equal")
plt.title("Percentage of Total Drivers by City Type")
plt.xlabel("City Types")
plt.ylabel("Percentage of Drivers")
plt.savefig("Figures/Total_Drivers.png")
plt.show()
```


![png](output_13_0.png)

