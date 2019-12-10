
---
title: 8 Matplotlib library
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 1
---
![image0](/img/matplotlib.png)

The Matplotlib library is one of the most used libraries for plotting data in Python.

Many types of graphics can be developed with this library:
https://matplotlib.org/gallery/index.html

To illustrate some features of the Python matplotlib.pyplot module (which provides a plotting system similar to that of MATLAB), we will use a database from the UQAM station. 


```python
import pandas as pd 
import numpy as np
import warnings; warnings.filterwarnings(action='ignore')

dataframe_UQAM = pd.read_csv('./DATA/UQAM_DATA_STATION_2018.csv')
dataframe_UQAM['Date']=pd.to_datetime(dataframe_UQAM['Date'])
dataframe_UQAM = dataframe_UQAM.set_index("Date", drop=True)
dataframe_UQAM.head()
```
| Date                |   Temperature minimale |   Temperature maximale |   Temperature moyenne |   Precipitation totale |   Dir_wind |   Mod_wind |
|:--------------------|-----------------------:|-----------------------:|----------------------:|-----------------------:|-----------:|-----------:|
| 2014-02-01 00:00:00 |                   -4.6 |                    0.9 |                  -1.5 |                      0 |        244 |          4 |
| 2014-02-02 00:00:00 |                   -6.2 |                    0.2 |                  -3.5 |                      0 |        163 |          2 |
| 2014-02-03 00:00:00 |                   -4.8 |                    0.5 |                  -1.2 |                      0 |        255 |          3 |
| 2014-02-04 00:00:00 |                   -9.9 |                   -4.8 |                  -8   |                      0 |        148 |          2 |
| 2014-02-05 00:00:00 |                   -9.9 |                   -6.3 |                  -7.6 |                      0 |        261 |          2 |



## Introduction to Matplotlib 
### conda install matplotlib

By running this special iPython command, we will be displaying plots inline:


```python
%matplotlib inline
```


```python
import matplotlib.pyplot as plt
```


```python
plt.plot() # you create an empty graph or instance and then add layers.
plt.show()
```


![png](/img/output_6_0.png)


## Add data to our charts


```python
dataframe_UQAM['2015'].head()
```

| Date                |   Temperature minimale |   Temperature maximale |   Temperature moyenne |   Precipitation totale |   Dir_wind |   Mod_wind |
|:--------------------|-----------------------:|-----------------------:|----------------------:|-----------------------:|-----------:|-----------:|
| 2015-01-01 00:00:00 |                  -13.3 |                   -6.4 |                  -9.5 |                      0 |        254 |          3 |
| 2015-01-02 00:00:00 |                   -7.3 |                   -3   |                  -4.9 |                      0 |        231 |          3 |
| 2015-01-03 00:00:00 |                  -12   |                   -3.2 |                  -7.8 |                      0 |        282 |          4 |
| 2015-01-04 00:00:00 |                  -15.3 |                   -8.7 |                 -12.5 |                      0 |        113 |          2 |
| 2015-01-05 00:00:00 |                   -8.8 |                    3.9 |                  -2.6 |                      0 |        178 |          3 |




```python
year_to_plot = dataframe_UQAM['2015']
plt.plot(year_to_plot.index,year_to_plot['Temperature moyenne'])
plt.show()
```


![png](/img/output_9_0.png)



```python
year_to_plot = dataframe_UQAM['2015']
plt.plot(year_to_plot.index,year_to_plot['Temperature moyenne'], marker='x')
plt.show()
```


![png](/img/output_10_0.png)


- <b>marker</b> option : 

https://matplotlib.org/api/markers_api.html

-  <b>linestyle</b> option: to delete or not the lines



```python
year_to_plot = dataframe_UQAM['2015']
plt.plot(year_to_plot.index,year_to_plot['Temperature moyenne'], marker='x', linestyle="--")
plt.show()
```


![png](/img/output_12_0.png)


- <b>scatter </b> fonction: function allows you to create scatter plot
- <b>.rcParams</b> method is used to enlarge the graphic window


```python
plt.rcParams["figure.figsize"]=[16,9]  
plt.scatter(year_to_plot.index,year_to_plot['Temperature moyenne'])
plt.show()
```


![png](/img/output_14_0.png)


- to use the scatter color option, python wants an input list and not a dictionary 
- color option : c=list()


```python
plt.rcParams["figure.figsize"]=[16,9]
plt.scatter(year_to_plot.index,year_to_plot['Temperature moyenne'], c=list(year_to_plot['Temperature moyenne']))
plt.xlabel("Temps")
plt.ylabel("Température")
plt.title("Temperature", y=1.05)
plt.show()
```


![png](/img/output_16_0.png)



- We used default scatter color ()
- with the <b> cmap </b> option, we can choose our color panel: https://matplotlib.org/examples/color/colormaps_reference.html
- we will for example choose the color palette "seismic" via the option <b> cmap </b>
- to change the shape and size of the points: use the <b> marker </b> and <b> s </b> options
- to save a graph: pyplot function: <b> savefig () </b>
- To add a color bar: <b> colorbar () </b> function
- To rotate the labels in x: function <b> xticks () </b>


```python
plt.rcParams["figure.figsize"]=[16,9]
plt.scatter(year_to_plot.index,year_to_plot['Temperature moyenne'], c=list(year_to_plot['Temperature moyenne']),
            cmap="seismic",
            marker="D", 
            s=100)
plt.xlabel("Time")
plt.ylabel("Temperature")
plt.title("Temperature", y=1.05)
plt.colorbar()
plt.xticks(rotation=45)
plt.show()
plt.savefig("figures/my_graph.png", bbox_inches="tight") 
```


![png](/img/output_18_0.png)



    <Figure size 1152x648 with 0 Axes>


##  Matplotlib classes

When creating a graph, matplotlib:

- stores a container for all the graphics
- stores a container so that the graphic is positioned on a grid
- stores visual symbols on the graph

You can plot different things in the same figure using the subplot function. Here is an example:


```python
fig = plt.figure()
ax1 = fig.add_subplot(2,2,1) # up and left 
ax2 = fig.add_subplot(2,2,2) # up and right 
ax3 = fig.add_subplot(2,2,3) # down and left 
ax4 = fig.add_subplot(2,2,4) # down and right
plt.show()
```


![png](/img/output_21_0.png)


Here is a documentation on subplot: 
https://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot

##  Add data


```python
fig = plt.figure()
ax1 = fig.add_subplot(2,1,1) 
ax2 = fig.add_subplot(2,1,2)

ax1.plot(dataframe_UQAM['2017'].index,dataframe_UQAM['2017']['Temperature moyenne'])
ax2.plot(dataframe_UQAM['2016'].index,dataframe_UQAM['2016']['Temperature moyenne'])

```




    [<matplotlib.lines.Line2D at 0xa516dd8>]




![png](/img/output_24_1.png)


## Improvement of the graph


```python
fig = plt.figure(figsize=(15, 8))
colors = ['green', 'blue', 'red']
for i in range(3):
    ax = fig.add_subplot(3,1,i+1)
    year = str(2014+i)
    label=year
    plt.plot(dataframe_UQAM[year].index,dataframe_UQAM[year]['Temperature moyenne'], c=colors[i], label = label)
    plt.legend(loc='upper left')
plt.show()

```


![png](/img/output_26_0.png)


## Example
### Objectives: to draw a meteogram of the UQAM station for the day of 14/12/2018


```python
import pandas as pd 
dataframe_UQAM = pd.read_csv('./DATA/UQAM_DATA_STATION.csv')
print(dataframe_UQAM.head())
```

              Time  Precipitation  pressure  humidex  Rosee  Temperature  Chill  \
    0  18-12-09_09           0.14    1038.0     -8.0   -7.8         -5.1   -8.0   
    1  18-12-09_10           0.00    1039.0     -7.0   -6.7         -3.9   -7.0   
    2  18-12-09_11           0.00    1033.0     -5.0   -6.0         -2.7   -5.0   
    3  18-12-09_12           0.00    1018.0     -2.0   -5.8         -0.2   -3.0   
    4  18-12-09_13           0.00    1106.0     -2.0   -6.0          0.0   -5.0   
    
       Humidite  Dir_wind  Mod_wind  
    0      81.0     208.0       6.0  
    1      81.0     201.0       6.0  
    2      78.0     184.0       5.0  
    3      66.0     208.0       8.0  
    4      64.0     268.0      18.0  
    


```python
dataframe_UQAM2 = pd.read_csv('./DATA/UQAM_DATA_STATION.csv', parse_dates=["Time"],date_parser=lambda x: pd.to_datetime(x, format="%y-%m-%d_%H"))
dataframe_UQAM2.head()

```
|    | Time                |   Precipitation |   pressure |   humidex |   Rosee |   Temperature |   Chill |   Humidite |   Dir_wind |   Mod_wind |
|---:|:--------------------|----------------:|-----------:|----------:|--------:|--------------:|--------:|-----------:|-----------:|-----------:|
|  0 | 2018-12-09 09:00:00 |            0.14 |       1038 |        -8 |    -7.8 |          -5.1 |      -8 |         81 |        208 |          6 |
|  1 | 2018-12-09 10:00:00 |            0    |       1039 |        -7 |    -6.7 |          -3.9 |      -7 |         81 |        201 |          6 |
|  2 | 2018-12-09 11:00:00 |            0    |       1033 |        -5 |    -6   |          -2.7 |      -5 |         78 |        184 |          5 |
|  3 | 2018-12-09 12:00:00 |            0    |       1018 |        -2 |    -5.8 |          -0.2 |      -3 |         66 |        208 |          8 |
|  4 | 2018-12-09 13:00:00 |            0    |       1106 |        -2 |    -6   |           0   |      -5 |         64 |        268 |         18 |





```python
# We just want data for 14/12/2018
start_date = '2018-12-14'
end_date = '2018-12-15'
df= dataframe_UQAM2
mask = (df['Time'] > start_date) & (df['Time'] <= end_date)


dataframe_jour = dataframe_UQAM2.loc[mask]
print(dataframe_jour.head())
print(len(dataframe_jour))
```

                       Time  Precipitation  pressure  humidex  Rosee  Temperature  \
    112 2018-12-14 01:00:00            0.0    1039.0    -10.0  -10.0         -6.3   
    113 2018-12-14 02:00:00            0.0    1039.0     -9.0   -9.0         -5.8   
    114 2018-12-14 03:00:00            0.0    1036.0     -9.0   -8.5         -5.4   
    115 2018-12-14 04:00:00            0.0    1036.0     -9.0   -8.4         -5.3   
    116 2018-12-14 05:00:00            0.0    1037.0     -8.0   -7.5         -4.8   
    
         Chill  Humidite  Dir_wind  Mod_wind  
    112   -8.0      75.0     208.0       4.0  
    113   -8.0      78.0     117.0       4.0  
    114   -7.0      79.0      89.0       4.0  
    115   -7.0      79.0      79.0       3.0  
    116   -7.0      81.0      92.0       4.0  
    24
    


```python
from matplotlib.font_manager import FontProperties
import matplotlib.dates as mdates
from datetime import datetime
from datetime import timedelta as td


daylabels = []
i = 0 
for index, row in dataframe_jour.iterrows():
    daylabels.append(dataframe_jour.iloc[i][0].replace(minute=0, second=0, microsecond=0).strftime('%Hh'))
    i += 1
print(daylabels)

start_date = '2018-12-14'
end_date = '2018-12-15'
fig = plt.figure(figsize=(20, 8))
fontP = FontProperties()
fontP.set_size('xx-small')
t = np.arange(0, 24, 1)
##### on trace les températures
ax1 = plt.subplot(411)
ax1.grid(True)
plt.plot(t, dataframe_jour['Temperature'], 'r-', label='Temperature de l\'air', linewidth=2)
plt.plot(t, dataframe_jour['Rosee'], 'r--',label='Temperature du point de rosee', linewidth=2)
plt.plot(t, dataframe_jour['Chill'], 'g--',label='Wind Chill', linewidth=2)
plt.legend(loc='upper left', ncol=1, bbox_to_anchor=(0, 1, 1, 0),fontsize =15)
plt.ylabel('Température ($^\circ$C)', {'color': 'black', 'fontsize': 15})

plt.setp(ax1.get_xticklabels(), fontsize=15)
plt.title('Meteogram station UQAM:'+ start_date + ' / ' + end_date, weight='bold').set_fontsize('20')
plt.setp(ax1.get_xticklabels(), visible=False)

##########  TRACE DES ACCUMULATIONS PRECIPITATION  ##########  
# share x only
ax2 = plt.subplot(412, sharex=ax1)
ax2.grid(True)
t = np.arange(0, 24, 1)
width=1
ax2.bar(t,dataframe_jour['Precipitation'].values,width,color='b', label='Pluie', linewidth=2)
plt.setp(ax2.get_xticklabels(), visible=False)
plt.ylim(0,  np.round(dataframe_jour['Precipitation'].max() ) +1)
plt.ylabel('Accumulation (mm)', {'color': 'black', 'fontsize': 15})
plt.legend(loc='upper left', ncol=1, bbox_to_anchor=(0, 0, 1, 1), fontsize =15)

# share x only
##### on trace l humidite
ax2 = plt.subplot(413, sharex=ax1)
ax2.grid(True)
plt.plot(t, dataframe_jour['Humidite'], 'b-', linewidth=2)
plt.setp(ax2.get_xticklabels(), visible=False)
plt.ylabel('Humidite relative (%)', {'color': 'black', 'fontsize': 15})
plt.legend(loc='upper left', ncol=1, bbox_to_anchor=(0, 0, 1, 1), fontsize =15)

##### on trace la pression
ax3 = plt.subplot(414, sharex=ax1)
plt.plot(t, dataframe_jour['pressure'], 'g-', linewidth=2)
plt.xlim(0.01, 24)
plt.ylim(np.round(min(dataframe_jour['pressure'])) - 2, np.round(max(dataframe_jour['pressure'])) + 2)
plt.ylabel('Pression (hPa)', {'color': 'black', 'fontsize': 15})
plt.legend(loc='upper left', ncol=1, bbox_to_anchor=(0, 0, 1, 1), fontsize =15)
ax3.grid(True)

for label in ax3.get_yticklabels():
    label.set_color("black")

ax3.set(xticks=np.arange(0,len(daylabels),1), xticklabels=daylabels) #Same as plt.xticks
spacing = 1
visible = ax3.xaxis.get_ticklabels()[::spacing]
for label in ax3.xaxis.get_ticklabels():
    if label not in visible:
        label.set_visible(False)


fig.autofmt_xdate()
fig.set_size_inches(18.5, 10.5)
fileout='figures/Meteogram_UQAM.png'
plt.savefig(fileout)
fig.autofmt_xdate()
plt.show()
```

    ['01h', '02h', '03h', '04h', '05h', '06h', '07h', '08h', '09h', '10h', '11h', '12h', '13h', '14h', '15h', '16h', '17h', '18h', '19h', '20h', '21h', '22h', '23h', '00h']
    


![png](/img/output_31_1.png)



```python

```
