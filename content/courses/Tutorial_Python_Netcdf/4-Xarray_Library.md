---
title: Xarray  
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial Netcdf 
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

In this tutorial, we will use the features of the Python xarray library to process and analyze Netcdf files.

To install the library under anaconda:

$ conda install xarray


Here is an example of structure of a Netcdf file under xarray:
   
![image0](/img/netcdf/xarray.png)

<b> DataArray </b>

xarray.DataArray is xarray’s implementation of a labeled, multi-dimensional array. It has several key properties:
|  |  |
|--|--|
| <b>values</b> |  a numpy.ndarray holding the array’s values |
| <b>dims</b> |  dimension names for each axis (e.g., ('x', 'y', 'z','time')) |
| <b>coords</b> | a dict-like container of arrays (coordinates) that label each point (e.g., 1-dimensional arrays of numbers, datetime objects or strings) |
| <b>attrs</b> |  an OrderedDict to hold arbitrary metadata (attributes) |

<b> DataSet </b>

xarray.Dataset is xarray’s multi-dimensional equivalent of a DataFrame. It is a dict-like container of labeled arrays (DataArray objects) with aligned dimensions. It is designed as an in-memory representation of the data model from the netCDF file format.


xarray.DataSet is a collection of DataArrays. Each NetCDF file contains a DataSet.

## 1- Open a Netcdf file

We will open and store the data of a Netcdf file in a Dataset.

First we need to import librairies and create aliases.


```python
import xarray as xr
import warnings; warnings.filterwarnings(action='ignore')
from matplotlib import pyplot as plt
%matplotlib inline
plt.rcParams['figure.figsize'] = (8,5)
```

- To import and store as dataset only one Netcdf file:

We will work with temperature fields from cera20c reanalysis.


```python
unique_dataDIR = './DATA/CERA20C/cera20c_member0_TAS_197101_day.nc'
TAS = xr.open_dataset(unique_dataDIR)
TAS
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 31)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-01-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] ...
        t2m        (time, latitude, longitude) float32 ...
    Attributes:
        CDI:          Climate Data Interface version 1.6.9 (http://mpimet.mpg.de/...
        Conventions:  CF-1.6
        history:      Thu Oct 25 14:29:40 2018: cdo daymean ./TAS/cera20c_member0...
        CDO:          Climate Data Operators version 1.6.9 (http://mpimet.mpg.de/...



- If we want to import several Netcdf files:

Here, we want to store all files' names starting with 'cera20c_member0_TAS_' and located in './data/cera20c/' path. 


```python
multi_dataDIR = './DATA/CERA20C/cera20c_member0_TAS_*.nc'
TAS2 = xr.open_mfdataset(multi_dataDIR)
TAS2
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 365)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>
    Attributes:
        CDI:          Climate Data Interface version 1.6.9 (http://mpimet.mpg.de/...
        Conventions:  CF-1.6
        history:      Thu Oct 25 14:29:40 2018: cdo daymean ./TAS/cera20c_member0...
        CDO:          Climate Data Operators version 1.6.9 (http://mpimet.mpg.de/...



- Combine Netcdf:

To combine variables and coordinates between multiple DataArray and/or Dataset objects, use merge(). It can merge a list of Dataset, DataArray or dictionaries of objects convertible to DataArray objects:
 


```python
multi_dataDIR = './DATA/CERA20C/cera20c_member0_TAS_*.nc'
TAS2 = xr.open_mfdataset(multi_dataDIR)
multi_dataDIR2 = './DATA/CERA20C/cera20c_member0_SIC_*.nc'
SIC2 = xr.open_mfdataset(multi_dataDIR2)

DS_new = xr.merge([TAS2,SIC2])
DS_new
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 365)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>



## 2- Exploring the data

We can quickly explore our datasets by using some methods of the xarray library: 

 - DS.var
 - DS.dims
 - DS.coords
 - DS.attrs


```python
DS_new.var
```




    <bound method ImplementsDatasetReduce._reduce_method.<locals>.wrapped_func of <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 365)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>>




```python
DS_new.dims
```




    Frozen(SortedKeysDict({'longitude': 288, 'latitude': 145, 'time': 365, 'bnds': 2}))




```python
DS_new.coords
```




    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00




```python
DS_new.attrs
```




    OrderedDict()



## 3- Basic operations with Xarray:

- Select a date:

We can use .sel() method to select one timestamp from our Dataset.


```python
DS_date = DS_new.sel(time='1971-01-01')
DS_date
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 1)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(1, 2), chunksize=(1, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(1, 145, 288), chunksize=(1, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(1, 145, 288), chunksize=(1, 145, 288)>



- Select time range

We can select a time range with slicing 


```python
DS_date_range = DS_new.sel(time=slice('1971-06-01', '1971-08-31'))
DS_date_range
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 92)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-06-01T10:30:00 ... 1971-08-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(92, 2), chunksize=(30, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(92, 145, 288), chunksize=(30, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(92, 145, 288), chunksize=(30, 145, 288)>



- Export a dataset

We can export our dataset into dataframe and then use Pandas library to make analysis. 


```python
df = DS_date_range.to_dataframe()
```


```python
df.head()
```
|                                                  | time_bnds           |     t2m |   siconc |
|:-------------------------------------------------|:--------------------|--------:|---------:|
| (0, 90.0, 0.0, Timestamp('1971-06-01 10:30:00')) | 1971-06-01 00:00:00 | 266.296 | 0.990234 |
| (0, 90.0, 0.0, Timestamp('1971-06-02 10:30:00')) | 1971-06-02 00:00:00 | 264.76  | 0.988525 |
| (0, 90.0, 0.0, Timestamp('1971-06-03 10:30:00')) | 1971-06-03 00:00:00 | 265.866 | 0.987502 |
| (0, 90.0, 0.0, Timestamp('1971-06-04 10:30:00')) | 1971-06-04 00:00:00 | 265.947 | 0.98738  |
| (0, 90.0, 0.0, Timestamp('1971-06-05 10:30:00')) | 1971-06-05 00:00:00 | 266.126 | 0.987152 |


```python
df.describe()
```
|       |           t2m |      siconc |
|:------|--------------:|------------:|
| count |   7.68384e+06 | 7.68384e+06 |
| mean  | 267.002       | 0.141752    |
| std   |  25.852       | 0.312001    |
| min   | 192.562       | 0           |
| 25%   | 273.221       | 0           |
| 50%   | 285.734       | 0           |
| 75%   | 296.388       | 0           |
| max   | 314.804       | 1           |


- Time mean



```python
Mean_array = DS_date_range.mean(dim='time')
Mean_array.values
```




    <bound method Mapping.values of <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
    Data variables:
        t2m        (latitude, longitude) float32 dask.array<shape=(145, 288), chunksize=(145, 288)>
        siconc     (latitude, longitude) float32 dask.array<shape=(145, 288), chunksize=(145, 288)>>



- To save our results into csv:


```python
Mean_array.t2m.to_dataframe().to_csv('./DATA/CERA20C_T2m_mean.csv')
```

- Mean over all latitudes and longitudes grid points: 


```python
DS_date_range.t2m.mean(dim=('latitude', 'longitude'))
```




    <xarray.DataArray 't2m' (time: 92)>
    dask.array<shape=(92,), dtype=float32, chunksize=(30,)>
    Coordinates:
      * time     (time) datetime64[ns] 1971-06-01T10:30:00 ... 1971-08-31T10:30:00




```python
DS_date_range.t2m.mean(dim=('latitude', 'longitude')).plot()
```




    [<matplotlib.lines.Line2D at 0xabe86a0>]




![png](/img/netcdf/output_27_1.png)


- To save into csv:


```python
DS_date_range.t2m.mean(dim=('time', 'longitude')).to_dataframe().to_csv('./DATA/CERA20C_T2m_2Dmean.csv')
```

- Quick plot with Xarray


```python
import cartopy.crs as ccrs
fig=plt.figure(figsize=(10,10), frameon=True) 

ax = plt.axes(projection=ccrs.Orthographic(-80, 35))
Mean_array.t2m.plot.contourf(ax=ax, transform=ccrs.PlateCarree());
ax.set_global(); ax.coastlines();
```


![png](/img/netcdf/output_31_0.png)


- Basic operations with Xarray:

In this example, we will mean DS_date_range over time and apply a substration to change units. 



```python
centigrade = DS_date_range.t2m.mean(dim='time') - 273.16
centigrade.values
```




    array([[ -1.2229004,  -1.2229004,  -1.2229004, ...,  -1.2229004,
             -1.2229004,  -1.2229004],
           [ -1.3348389,  -1.3311157,  -1.3274231, ...,  -1.3488159,
             -1.3442383,  -1.3395386],
           [ -1.6027222,  -1.5914001,  -1.5804138, ...,  -1.6451721,
             -1.631012 ,  -1.6168518],
           ...,
           [-58.547928 , -58.5663   , -58.58455  , ..., -58.314026 ,
            -58.391983 , -58.46997  ],
           [-59.556473 , -59.577957 , -59.59955  , ..., -59.478424 ,
            -59.50441  , -59.53041  ],
           [-60.739105 , -60.739105 , -60.739105 , ..., -60.739105 ,
            -60.739105 , -60.739105 ]], dtype=float32)




```python
fig=plt.figure(figsize=(10,10), frameon=True)
ax = plt.axes(projection=ccrs.Orthographic(-80, 35))
centigrade.plot.contourf(ax=ax, transform=ccrs.PlateCarree());
ax.set_global(); ax.coastlines();
```


![png](/img/netcdf/output_34_0.png)


- Groupby() method:

groupdby() method with Xarray is very usefull to group our datasets by month, season, year... and then apply function to compute indices.


```python
DS_new
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 145, longitude: 288, time: 365)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>




```python
# monthly mean:
DS_month = DS_new.groupby('time.month').mean('time')
DS_month
#DS_month.to_dataframe()
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288, month: 12)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * month      (month) int64 1 2 3 4 5 6 7 8 9 10 11 12
    Data variables:
        t2m        (month, latitude, longitude) float32 dask.array<shape=(12, 145, 288), chunksize=(1, 145, 288)>
        siconc     (month, latitude, longitude) float32 dask.array<shape=(12, 145, 288), chunksize=(1, 145, 288)>



We can use this method to compute climatology and then anomalies.


```python
climatology = DS_new.groupby('time.month').mean('time')
anomalies = DS_new.groupby('time.month') - climatology
anomalies
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288, time: 365)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
        month      (time) int64 1 1 1 1 1 1 1 1 1 1 ... 12 12 12 12 12 12 12 12 12
    Data variables:
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 145, 288), chunksize=(31, 145, 288)>




```python
# seaon mean:
DS_season = DS_new.groupby('time.season').mean('time')
DS_season
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288, season: 4)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * season     (season) object 'DJF' 'JJA' 'MAM' 'SON'
    Data variables:
        t2m        (season, latitude, longitude) float32 dask.array<shape=(4, 145, 288), chunksize=(1, 145, 288)>
        siconc     (season, latitude, longitude) float32 dask.array<shape=(4, 145, 288), chunksize=(1, 145, 288)>




```python
# year mean:
DS_year = DS_new.groupby('time.year').mean('time')
DS_year
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288, year: 1)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * year       (year) int64 1971
    Data variables:
        t2m        (year, latitude, longitude) float32 dask.array<shape=(1, 145, 288), chunksize=(1, 145, 288)>
        siconc     (year, latitude, longitude) float32 dask.array<shape=(1, 145, 288), chunksize=(1, 145, 288)>



- to select a specific season:


```python
DS_winter = DS_season.sel(season='DJF')
DS_winter
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288)
    Coordinates:
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
        season     <U3 'DJF'
    Data variables:
        t2m        (latitude, longitude) float32 dask.array<shape=(145, 288), chunksize=(145, 288)>
        siconc     (latitude, longitude) float32 dask.array<shape=(145, 288), chunksize=(145, 288)>



In the example below, we will group the xarray.DataArray data by season, calculate the average, apply a simple arrhythmic operation and plot the resulting fields for each season. 


```python
DS_Season = DS_new.t2m.groupby('time.season').mean('time')- 273.15
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(9,5))
j = 0
for i, season in enumerate(('DJF', 'MAM', 'JJA', 'SON')):
    if season =='JJA':
        j += 1
        i = 0
    elif season =='SON':
        i = 1
        
    DS_Season.sel(season=season).plot.pcolormesh(
        ax=axes[i, j], vmin=-30, vmax=30, cmap='Spectral_r',
        add_colorbar=True, extend='both')

for ax in axes.flat:
    ax.axes.get_xaxis().set_ticklabels([])
    ax.axes.get_yaxis().set_ticklabels([])
    ax.axes.axis('tight')
   
plt.tight_layout()
fig.suptitle('Seasonal Surface Air Temperature', fontsize=16, y=1.02)
```




    Text(0.5, 1.02, 'Seasonal Surface Air Temperature')




![png](output_45_1.png)



```python

lat_bnd = [80, 50]
lon_bnd = [250, 310]
DS_Season = DS_new.sel(longitude=slice(*lon_bnd), latitude=slice(*lat_bnd),).siconc.groupby('time.season').mean('time') *100

fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(16,10))
j = 0
for i, season in enumerate(('DJF', 'MAM', 'JJA', 'SON')):
    if season =='JJA':
        j += 1
        i = 0
    elif season =='SON':
        i = 1
        
    DS_Season.sel(season=season).plot.pcolormesh(
        ax=axes[i, j], vmin=0, vmax=100, cmap='Spectral_r',
        add_colorbar=True, extend='both')
for ax in axes.flat:
    ax.axes.get_xaxis().set_ticklabels([])
    ax.axes.get_yaxis().set_ticklabels([])
    ax.axes.axis('tight')
   
plt.tight_layout()
fig.suptitle('Seasonal Sea Ice Concentration', fontsize=16, y=1.02)
```




    Text(0.5, 1.02, 'Seasonal Sea Ice Concentration')




![png](/img/netcdf/output_46_1.png)


To save our result into Netcdf: 


```python
DS_season = DS_new.groupby('time.season').mean('time')
dataDIR = './DATA/CERA20C_season.nc'
DS_Season.to_netcdf(dataDIR)

```

##  4- Select grid points from Netcdf file using Xarray

In the previous section we applied the .sel () method to work on the time dimension. This method can be used on spatial dimensions to extract points or study areas from our netcdf file.

### Gridpoint:  to extract the closest grid point of a latitude / longitude: 


```python
lati = 45.5
loni = 269.2
data  = DS_new.sel(longitude=loni  , latitude=lati  , method='nearest') 
data
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, time: 365)
    Coordinates:
        longitude  float32 268.75
        latitude   float32 45.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time) float32 dask.array<shape=(365,), chunksize=(31,)>
        siconc     (time) float32 dask.array<shape=(365,), chunksize=(31,)>




```python
data['t2m'] = data['t2m'] - 273.15
```


```python
data.t2m
```




    <xarray.DataArray 't2m' (time: 365)>
    dask.array<shape=(365,), dtype=float32, chunksize=(31,)>
    Coordinates:
        longitude  float32 268.75
        latitude   float32 45.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00



We can convert our selection into a DataFrame and then use Pandas to analyse our results.


```python
df = data.t2m.to_dataframe()
fig = plt.figure(figsize=(16,8))
df['t2m'].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x13660400>




![png](/img/netcdf/output_55_1.png)


### Gridpoints:  to extract a list of points


```python
lats =  [20.0,50.0,90.0]
lons =  [60.0,80.0,120.0]

data  = DS_new.sel(longitude=lons  , latitude=lats  , method='nearest')
data['t2m'] = data['t2m']-273.15
data
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 3, longitude: 3, time: 365)
    Coordinates:
      * longitude  (longitude) float32 60.0 80.0 120.0
      * latitude   (latitude) float32 20.0 50.0 90.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 3, 3), chunksize=(31, 3, 3)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 3, 3), chunksize=(31, 3, 3)>




```python
fig = plt.figure(figsize=(16,8))
data.t2m.sel(longitude=60.0, latitude=[20.0,50.0,90.0]).plot.line(x='time')
```




    [<matplotlib.lines.Line2D at 0xdf31ac8>,
     <matplotlib.lines.Line2D at 0xdd0bf28>,
     <matplotlib.lines.Line2D at 0xdd0b4a8>]




![png](/img/netcdf/output_58_1.png)


### To extract an area or subdomain delimited by latitude and longitude values: .slicing() 


```python
lat_bnd = [80, 50]
lon_bnd = [250, 310]
area = DS_new.sel(longitude=slice(*lon_bnd), latitude=slice(*lat_bnd),)
area
```




    <xarray.Dataset>
    Dimensions:    (bnds: 2, latitude: 25, longitude: 49, time: 365)
    Coordinates:
      * longitude  (longitude) float32 250.0 251.25 252.5 ... 307.5 308.75 310.0
      * latitude   (latitude) float32 80.0 78.75 77.5 76.25 ... 52.5 51.25 50.0
      * time       (time) datetime64[ns] 1971-01-01T10:30:00 ... 1971-12-31T10:30:00
    Dimensions without coordinates: bnds
    Data variables:
        time_bnds  (time, bnds) datetime64[ns] dask.array<shape=(365, 2), chunksize=(31, 2)>
        t2m        (time, latitude, longitude) float32 dask.array<shape=(365, 25, 49), chunksize=(31, 25, 49)>
        siconc     (time, latitude, longitude) float32 dask.array<shape=(365, 25, 49), chunksize=(31, 25, 49)>




```python
area.longitude.values
```




    array([250.  , 251.25, 252.5 , 253.75, 255.  , 256.25, 257.5 , 258.75,
           260.  , 261.25, 262.5 , 263.75, 265.  , 266.25, 267.5 , 268.75,
           270.  , 271.25, 272.5 , 273.75, 275.  , 276.25, 277.5 , 278.75,
           280.  , 281.25, 282.5 , 283.75, 285.  , 286.25, 287.5 , 288.75,
           290.  , 291.25, 292.5 , 293.75, 295.  , 296.25, 297.5 , 298.75,
           300.  , 301.25, 302.5 , 303.75, 305.  , 306.25, 307.5 , 308.75,
           310.  ], dtype=float32)



To visualize our area:: 


```python
import cartopy.crs as ccrs
import cartopy.feature as cfeat
def make_figure():
    fig = plt.figure(figsize=(22, 12))
    ax = fig.add_subplot(1, 1, 1, projection=ccrs.PlateCarree())

    # generate a basemap with country borders, oceans and coastlines
    ax.add_feature(cfeat.LAND)
    ax.add_feature(cfeat.OCEAN)
    ax.add_feature(cfeat.COASTLINE)
    ax.add_feature(cfeat.BORDERS, linestyle='dotted')
    return fig, ax

make_figure();
```


![png](/img/netcdf/output_63_0.png)



```python
_, ax = make_figure()
# plot the temperature field
area.t2m[0].plot()
```




    <matplotlib.collections.QuadMesh at 0xb2e9240>




![png](/img/netcdf/output_64_1.png)


### To mask an area delimited by a Shapefile:

To do this, we need to import two more librairies: 
- Geopandas: conda install -c conda-forge geopandas
- osgeo: conda install -c conda-forge gdal

The next function will open a shapefile, read the polygons and make a mask from each grid points of our Netcdf inside the polygons. 


```python
from osgeo import ogr
import geopandas as gpd
import numpy as np
def get_mask(lons2d, lats2d, shp_path="", polygon_name=None):
    """
    Assumes that the shape file contains polygons in lat lon coordinates
    :param lons2d:
    :param lats2d:
    :param shp_path:
    :rtype : np.ndarray
    The mask is 1 for the points inside of the polygons
    """
    ds = ogr.Open(shp_path)
    """
    :type : ogr.DataSource
    """

    xx = lons2d.copy()
    yy = lats2d

    # set longitudes to be from -180 to 180
    xx[xx > 180] -= 360

    mask = np.zeros(lons2d.shape, dtype=int)
    nx, ny = mask.shape

    pt = ogr.Geometry(ogr.wkbPoint)

    for i in range(ds.GetLayerCount()):
        layer = ds.GetLayer(i)
        """
        :type : ogr.Layer
        """

        for j in range(layer.GetFeatureCount()):
            feat = layer.GetFeature(j)
            """
            :type : ogr.Feature
            """

            # Select polygons by the name property
            if polygon_name is not None:
                if not feat.GetFieldAsString("NAME") == polygon_name:
                    continue

            g = feat.GetGeometryRef()
            """
            :type : ogr.Geometry
            """

            assert isinstance(g, ogr.Geometry)

            for pi in range(nx):
                for pj in range(ny):
                    pt.SetPoint_2D(0, float(xx[pi, pj]), float(yy[pi, pj]))

                    mask[pi, pj] += int(g.Contains(pt))

    return mask

```

We first read the Netcdf file and store informations in a Xarray.dataset. 



```python
ds = xr.open_dataset('./DATA/CERA20C/cera20c_member0_TAS_197101_day.nc')
```

We then need to extract latitudes and longitudes values and compute a 2D matrix. 


```python
Imp_Lats =  ds['latitude'].values
Imp_Lons =  ds['longitude'].values
lon2d, lat2d = np.meshgrid(Imp_Lons, Imp_Lats)
```


```python
ds_mean = ds.mean('time') - 273.15
ds_mean
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288)
    Coordinates:
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
    Data variables:
        t2m        (latitude, longitude) float32 -34.067184 ... -25.249802



We open the shape file with Geopandas library.


```python
shapes = gpd.read_file("./DATA/Shapefiles/Countries_Final-polygon.shp")
list(shapes.columns.values)
```




    ['FIPS',
     'ISO2',
     'ISO3',
     'UN',
     'NAME',
     'AREA',
     'POP2005',
     'REGION',
     'SUBREGION',
     'LON',
     'LAT',
     'layer',
     'path',
     'geometry']




```python
shapes.head()
```
```python
shapes.loc[27, 'geometry']
shapes.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0xd8b4b70>




![png](/img/netcdf/output_75_1.png)


We want in our study to extract information inside Mexico shapefile.


```python
mask=get_mask(lon2d,lat2d,shp_path="./DATA/Shapefiles/Countries_Final-polygon.shp", polygon_name='Mexico') 
np.max(mask)
```




    1



We will convert our mask into numpy 2D array. We'll be later able to apply this matrix to mask our Netcdf file. 


```python
np.save('DATA/Mexico.npy',mask) # saving our mask in numpy.array
```

We will mask our area using .where() method. 


```python
ds_mask = ds_mean.where(mask == 1) 
ds_mask.to_netcdf('DATA/Mexico.nc')  # we want to save our shapefile mask in Netcdf format
```


```python
ds_mask
```




    <xarray.Dataset>
    Dimensions:    (latitude: 145, longitude: 288)
    Coordinates:
      * latitude   (latitude) float32 90.0 88.75 87.5 86.25 ... -87.5 -88.75 -90.0
      * longitude  (longitude) float32 0.0 1.25 2.5 3.75 ... 356.25 357.5 358.75
    Data variables:
        t2m        (latitude, longitude) float32 nan nan nan nan ... nan nan nan nan




```python
np.max(ds_mask.t2m)
```




    <xarray.DataArray 't2m' ()>
    array(24.010315)




```python
_, ax = make_figure()
# plot the temperature field
lat_bnd = [35, 0]
lon_bnd = [240, 280]
ds_mask.t2m.sel(longitude=slice(*lon_bnd), latitude=slice(*lat_bnd),).plot.pcolormesh(vmin=0, vmax=30, cmap='Spectral',add_colorbar=True, extend='both')
```




    <matplotlib.collections.QuadMesh at 0xdc65400>




![png](/img/netcdf/output_84_1.png)


##  5- Last example using Xarray: 

In this section, We will calculate the seasonal accumulation of the precipitation, extract a region, plot the domain and record our result in Netcdf:


```python
# Let's open cera20c_enda_ep_PR_*.nc netcdf files 
multi_dataDIR = './DATA/CERA20C/cera20c_enda_ep_PR_*.nc'
array = xr.open_mfdataset(multi_dataDIR)
array.tp
```




    <xarray.DataArray 'tp' (time: 365, latitude: 181, longitude: 360)>
    dask.array<shape=(365, 181, 360), dtype=float32, chunksize=(31, 181, 360)>
    Coordinates:
      * longitude  (longitude) float32 0.0 1.0 2.0 3.0 ... 356.0 357.0 358.0 359.0
      * latitude   (latitude) float32 90.0 89.0 88.0 87.0 ... -88.0 -89.0 -90.0
      * time       (time) datetime64[ns] 1971-01-02T18:00:00 ... 1972-01-01T18:00:00
    Attributes:
        units:      m
        long_name:  Total precipitation



All Netcdf files are stored in DataArray container, we can now group our Datasets by season, apply a simple sum() method over time and then change units from meters to mm.


```python
array_season = array.groupby('time.season').sum('time')*1000
array_season
```




    <xarray.Dataset>
    Dimensions:    (latitude: 181, longitude: 360, season: 4)
    Coordinates:
      * latitude   (latitude) float32 90.0 89.0 88.0 87.0 ... -88.0 -89.0 -90.0
      * season     (season) object 'DJF' 'JJA' 'MAM' 'SON'
      * longitude  (longitude) float32 0.0 1.0 2.0 3.0 ... 356.0 357.0 358.0 359.0
    Data variables:
        tp         (season, latitude, longitude) float32 dask.array<shape=(4, 181, 360), chunksize=(1, 181, 360)>



We want to extract a specific domain delimited: 
    - latitude boundaries: 50N to 70N
    - longitude boudaries: 250E to 310E
    
We finally want to extract winter season. 


```python
lat_bnd = [70, 50]
lon_bnd = [250, 310]
subset_season_DJF = array_season.sel(season = 'DJF', longitude=slice(*lon_bnd), latitude=slice(*lat_bnd),)
subset_season_DJF
```




    <xarray.Dataset>
    Dimensions:    (latitude: 21, longitude: 61)
    Coordinates:
      * latitude   (latitude) float32 70.0 69.0 68.0 67.0 ... 53.0 52.0 51.0 50.0
        season     <U3 'DJF'
      * longitude  (longitude) float32 250.0 251.0 252.0 253.0 ... 308.0 309.0 310.0
    Data variables:
        tp         (latitude, longitude) float32 dask.array<shape=(21, 61), chunksize=(21, 61)>



Let's save the Dataset to Netcdf. 


```python
dataDIR = './DATA/subset_season.nc'
subset_season_DJF.to_netcdf(dataDIR)
```

We can call our make_figure() function to quick plot our Dataset. 


```python
_, ax = make_figure()
# plot the temperature field
subset_season_DJF.tp.plot.pcolormesh(vmin=0, vmax=200, cmap='Spectral',add_colorbar=True, extend='both')
```




    <matplotlib.collections.QuadMesh at 0x130aedd8>




![png](/img/netcdf/output_94_1.png)



```python
array_season
```




    <xarray.Dataset>
    Dimensions:    (latitude: 181, longitude: 360, season: 4)
    Coordinates:
      * latitude   (latitude) float32 90.0 89.0 88.0 87.0 ... -88.0 -89.0 -90.0
      * season     (season) object 'DJF' 'JJA' 'MAM' 'SON'
      * longitude  (longitude) float32 0.0 1.0 2.0 3.0 ... 356.0 357.0 358.0 359.0
    Data variables:
        tp         (season, latitude, longitude) float32 dask.array<shape=(4, 181, 360), chunksize=(1, 181, 360)>




```python

```


```python

```

