# API-Homework

3 Observable trends from the data:

1. In the northern hemisphere above the equator, the temperature decreases significatly.  
2. The closer you are to the equator, the less likely there will be humidity.  
3. There seeems to be no observable pattern to windspeed and the equator.  The speeds are low and high at various latitudes







```python
import os
import random
import openweathermapy.core as ow
import requests
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
from citipy import citipy
api_key = "8b470b618b32d04717d95d67a3997c16"
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

```


```python
#Generate random numbers
Long = np.random.uniform(-180,180,550)
Lat =  np.random.uniform(-90,90,550)


```


```python
#Make Coordinates to dataframs
Coordinates = {"Long": Long, "Lat": Lat}
Coordinates_df = pd.DataFrame(Coordinates)
Coordinates_df.head()
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
      <th>Lat</th>
      <th>Long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-71.066785</td>
      <td>-136.044560</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-82.933394</td>
      <td>-131.253388</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-62.923891</td>
      <td>-34.202476</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-81.129259</td>
      <td>-172.496532</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6.184056</td>
      <td>22.904226</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_coordinates = Coordinates_df.as_matrix()
```


```python
#loop through coordinates
cities = []

for coordinate_pair in city_coordinates:
    lat, lon = coordinate_pair
    cities.append(citipy.nearest_city(lat, lon).city_name)
    

```


```python
#Build Query url
query_url = url + "appid=" + api_key + "&units=" + units + "&q="
query_url
```




    'http://api.openweathermap.org/data/2.5/weather?appid=8b470b618b32d04717d95d67a3997c16&units=imperial&q='




```python
weather_data = []
temp_list = []
humidity_list = []
clouds_list = []
wind_list = []
lat_list = []
long_list =[]
    
for city in cities:
    try:
        
        response = requests.get(query_url + city).json()
        #print(response)
        temp_data = response['main']['temp']
        humidity_data = response['main']["humidity"]
        clouds_data = response["clouds"]["all"]
        wind_data = response["wind"]["speed"]
        lat_data = response["coord"]["lat"]
        long_data = response["coord"]["lon"]
    except KeyError:
        print("Ooops, the city can not be found!")
    
    #weather_data.append(response)
    temp_list.append(temp_data)
    humidity_list.append(humidity_data)
    clouds_list.append(clouds_data)
    wind_list.append(wind_data)
    lat_list.append(lat_data)
    long_list.append(long_data)
    
print("Thats the end of the list")
```

    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Ooops, the city can not be found!
    Thats the end of the list
    


```python
temp_data
```




    92.24




```python
humidity_data
```




    56




```python


```


```python
weather_report = {"Temperature (F)": temp_list, "Humidity (%)": humidity_list, "Cloudiness (%)": clouds_list, "Wind Speed (MPH)": wind_list, "Latitude": lat_list,"Longitude": long_data, "Cities": cities}

weather_report_df = pd.DataFrame(weather_report)


weather_report_df.to_csv("weather_report.csv")

weather_report_df.head()
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
      <th>Cities</th>
      <th>Cloudiness (%)</th>
      <th>Humidity (%)</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Temperature (F)</th>
      <th>Wind Speed (MPH)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>rikitea</td>
      <td>76</td>
      <td>99</td>
      <td>-23.12</td>
      <td>138.6</td>
      <td>80.13</td>
      <td>17.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>rikitea</td>
      <td>76</td>
      <td>99</td>
      <td>-23.12</td>
      <td>138.6</td>
      <td>80.13</td>
      <td>17.47</td>
    </tr>
    <tr>
      <th>2</th>
      <td>mar del plata</td>
      <td>0</td>
      <td>55</td>
      <td>-46.43</td>
      <td>138.6</td>
      <td>62.63</td>
      <td>20.38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>vaini</td>
      <td>0</td>
      <td>43</td>
      <td>15.34</td>
      <td>138.6</td>
      <td>83.87</td>
      <td>4.38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>bria</td>
      <td>0</td>
      <td>58</td>
      <td>6.54</td>
      <td>138.6</td>
      <td>64.34</td>
      <td>12.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
file_name = os.path.join("weather_report.csv")
report_df = pd.read_csv(file_name)
report_df.head()
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
      <th>Unnamed: 0</th>
      <th>Cities</th>
      <th>Cloudiness (%)</th>
      <th>Humidity (%)</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Temperature (F)</th>
      <th>Wind Speed (MPH)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>rikitea</td>
      <td>76</td>
      <td>99</td>
      <td>-23.12</td>
      <td>138.6</td>
      <td>80.13</td>
      <td>17.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>rikitea</td>
      <td>76</td>
      <td>99</td>
      <td>-23.12</td>
      <td>138.6</td>
      <td>80.13</td>
      <td>17.47</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>mar del plata</td>
      <td>0</td>
      <td>55</td>
      <td>-46.43</td>
      <td>138.6</td>
      <td>62.63</td>
      <td>20.38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>vaini</td>
      <td>0</td>
      <td>43</td>
      <td>15.34</td>
      <td>138.6</td>
      <td>83.87</td>
      <td>4.38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>bria</td>
      <td>0</td>
      <td>58</td>
      <td>6.54</td>
      <td>138.6</td>
      <td>64.34</td>
      <td>12.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
report_df.plot.scatter(x='Latitude', y="Temperature (F)")
plt.xlabel("Latitude")
plt.ylabel("Max Temperature (F)")
plt.title('City Latitude vs. Max Temperature Jan 26th, 2018')
plt.style.use('seaborn-dark')
plt.grid(True)

plt.savefig("City_Lat vs Temperature")
plt.show()
```


![png](output_12_0.png)



```python
report_df.plot.scatter(x='Latitude', y="Humidity (%)")
plt.xlabel("Latitude")
plt.ylabel("Humidity (%)")
plt.title('City Latitude vs. Humidity Jan 26th, 2018')
plt.style.use('seaborn-dark')
plt.grid(True)

plt.savefig("City_Lat vs Humidity")
plt.show()
```


![png](output_13_0.png)



```python
report_df.plot.scatter(x='Latitude', y="Cloudiness (%)")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness (%)")
plt.title('City Latitude vs. Cloudiness Jan 26th, 2018')
plt.style.use('seaborn-dark')
plt.grid(True)

plt.savefig("City_Lat vs Cloudiness")
plt.show()
```


![png](output_14_0.png)



```python
report_df.plot.scatter(x='Latitude', y="Wind Speed (MPH)")
plt.xlabel("Latitude")
plt.ylabel("Wind Speed (MPH)")
plt.title('City Latitude vs. Wind Speed Jan 26th, 2018')
plt.style.use('seaborn-dark')
plt.grid(True)

plt.savefig("City_Lat vs Wind Speed")
plt.show()
```


![png](output_15_0.png)









