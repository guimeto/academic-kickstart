
---
title: Netcdf Part 1  
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


Network Common Data Form (Netcdf) is a way to create, access, and share scientific data in a format that is self-documenting and transparent for many types of machines.

![image0](/img/netcdf/xarray.png)

The Netcdf file itself has information describing the data it contains.

A NetCDF file has dimensions, variables, and attributes.

Here is a small example of a NetCDF file, to illustrate these concepts of dimensions, variables and attributes.

The notation used to describe this NetCDF file is called Network Common Data Language (CDL). It gives a "text" version that allows an easy understanding of the structure and contents of a binary NetCDF file:

    netcdf ./data/NARR_tasmax_201701.nc {
      dimensions:
    x = 349;
    y = 277;
    time = 31;
      variables:
    float lon(y=277, x=349);
      :units = "degrees_east";
      :long_name = "Longitude";
      :CoordinateAxisType = "Lon";

    float lat(y=277, x=349);
      :units = "degrees_north";
      :long_name = "Latitude";
      :CoordinateAxisType = "Lat";

    double time(time=31);
      :long_name = "Time";
      :delta_t = "";

    float tasmax(time=31, y=277, x=349);
      :long_name = "Daily maximum temperature";
      :units = "Celcius";
      :missing_value = -999.0; // double
      :coordinates = "lon lat";
}


Panoply is an apensource software used to quickly read aned visualize Netcdf file:
https://www.giss.nasa.gov/tools/panoply/download/

The python module that we will use in this section is netCDF4:
https://pypi.org/project/netCDF4/

To install it under anaconda: <b>conda install -c anaconda netcdf4</b>  


![image0](/img/netcdf/CanESM2_rcp85_r1i1p1_global_tos.jpg)


## 1- Create a Netcdf file:

```python
from netCDF4 import Dataset
import os 
import warnings
warnings.filterwarnings("ignore")

file_name = "./DATA/2D_Temperature.nc"
if os.path.isfile(file_name):
    os.remove(file_name)
    
#open the file for writing, you can Also specify format="NETCDF4_CLASSIC" or "NETCDF3_CLASSIC"
#The format is NETCDF4 by default
ds = Dataset(file_name, mode="w")
```

- Netcdf4-python: <b>createDimension</b>

We will create here a 2D field: (20,20)  


```python
ds.createDimension("x", 20)
ds.createDimension("y", 20)
ds.createDimension("time", None)
```




    <class 'netCDF4._netCDF4.Dimension'> (unlimited): name = 'time', size = 0



- Netcdf4-python: <b>createVariable</b>


```python
var1 = ds.createVariable("field1", "f4", ("time", "x", "y"))
var2 = ds.createVariable("field2", "f4", ("time", "x", "y"))

#add netcdf attributes
var1.units = "Celcius"
var1.long_name = "Surface air temperature"

var2.units = "Kelvin"
var2.long_name = "Surface air temperature"

```

We can now assign our field or variable.


```python
#generate random data and tell the program where it should go
import numpy as np
data = np.random.randn(10, 20, 20)
var1[:] = data
var2[:] =  data + 273.15
#actually write data to the disk
ds.close();
```

## 2- Read a Netcdf file

We will read the file Netcdf4 that we created previously.


```python
from netCDF4 import Dataset
ds = Dataset("./DATA/2D_Temperature.nc")
```

We will select our variables of interest: no data is loaded at this level.


```python
# Which variables are in our Netcdf file ?
print(ds.variables.keys())

data1_var = ds.variables["field1"]
data2_var = ds.variables["field2"]

#What's the dimension ?
print(data1_var.dimensions, data1_var.shape)
```

    odict_keys(['field1', 'field2'])
    ('time', 'x', 'y') (10, 20, 20)
    

We can now read our file: 


```python
#now we ask to really read the data into the memory
all_data = data1_var[:]
#print all_data.shape
data1 = data1_var[1,:,:]
data2 = data2_var[2,:,:]
#data1
print(data1.shape, all_data.shape, all_data.mean(axis = 0).mean(axis = 0).mean(axis = 0))
```

    (20, 20) (10, 20, 20) 0.0055584796
    

## 3- Examples of manipulations of a Netcdf file


In this example we will work with daily maximum temperature data for all January months from 1971 to 2000 from the CRCM5 regional model developed at the ESCER center.

We will import our own module for calculating temperature indices, this module is calld Indices_Temperature. 

At first we will import the necessary libraries and define the input parameters.



```python
from netCDF4 import Dataset
import Indices_Temperature
import numpy as np

Mois='01'
model='CRCM5-v1_NAM-44_ll_CCCma-CanESM2'
path_model='CRCM5-v1_CCCma-CanESM2_historical'
variable='tasmax'
indice = 'Tmax90p'
yi = 1971
yf = 2000
#########################################################
rep_data='./DATA/CRCM5/'
rep_out='./DATA/CRCM5/'
tot=(yf-yi)+1 
```

- Let's open 'CRCM5-v1_NAM-44_ll_CCCma-CanESM2_historical_tasmax_197101.nc' file:


```python
nc_Modc=Dataset('./DATA/CRCM5/'+model+'_historical_'+variable+'_197101.nc','r')
lats=nc_Modc.variables['lat'][:]
lons=nc_Modc.variables['lon'][:]
varc=nc_Modc.variables[variable][:]
```


```python
## Quick look of our file: 
print('-----------------------------------------')
print('Temperature dimension = ',varc.shape)
print('Minimum of temperature = ', np.nanmin(varc))
print('Maximum of temperature = ', np.nanmax(varc))
print('-----------------------------------------')
print('-----------------------------------------')
print('Latitude dimension= ',lats.shape)
print('Minimum of latitude = ', np.min(lats))
print('Maximum of latitude = ', np.max(lats))
print('-----------------------------------------')
print('-----------------------------------------')
print('Longitude dimesion = ',lons.shape)
print('Minimum of longitude = ', np.min(lons))
print('Maximum of longitude = ', np.max(lons))
print('-----------------------------------------')
```

    -----------------------------------------
    Temperature dimension =  (31, 130, 155)
    Minimum of temperature =  -57.66677
    Maximum of temperature =  30.657953
    -----------------------------------------
    -----------------------------------------
    Latitude dimension=  (130, 155)
    Minimum of latitude =  12.538727
    Maximum of latitude =  75.86
    -----------------------------------------
    -----------------------------------------
    Longitude dimesion =  (130, 155)
    Minimum of longitude =  -170.71053
    Maximum of longitude =  -23.28948
    -----------------------------------------
    

We can now loop over all our Netcdf files and apply a function to calculate our indice. 


```python
nt=0
IND = np.zeros((tot,130,155),dtype=float)
for year in range(yi,yf+1):
    ###### ouverture et lecture des fichiers Netcdf
    hist=model+'_historical_'+variable+'_'+str(year)+Mois+'.nc'     
    modelc=rep_data+'/'+hist
    nc_Modc=Dataset(modelc,'r')
    lats=nc_Modc.variables['lat'][:]
    lons=nc_Modc.variables['lon'][:]
    varc=nc_Modc.variables[variable][:]
    
    ###### boucle sur tous les points de grille et calcul de l'indice
    for ni in range(0, len(varc[0])):
        for nj in range(0, len(varc[0][0])):
            if indice == 'Mean_tasmax':
                IND[nt,ni,nj]=Indices_Temperature.MOY(varc[:,ni,nj])
                description='Monthly Mean of tasmax'
                unite='°Celcius'
            elif indice == 'Tmax90p':
                IND[nt,ni,nj]=Indices_Temperature.Tmax90p(varc[:,ni,nj])
                description='Monthly Mean of Tmax90p' 
                unite='°Celcius'               
    nt+=1 
    
    ###### Écriture du fichier Netcdf en sortie
C = Dataset(rep_out+model+'_historical_'+indice+'_'+str(yi)+'-'+str(yf)+'_'+Mois+'.nc', 'w')
C.description = 'Indice temperature'
C.conventions = 'CF-1.0'  
C.model_id = model
C.grid='latlon'
C.CDO = 'Climate Data Operators version 1.6.2 (http://code.zmaw.de/projects/cdo)'
C.institution = 'UQAM - ESCER Center, University of Quebec in Montreal'
C.contact = 'Guillaume Dueymes'
########################################
# Dimensions
C.createDimension('x', len(varc[0][0]))
C.createDimension('y', len(varc[0]))
C.createDimension('time', tot)

var=C.createVariable(str(indice), np.float32, ('time','y','x')) 
var.long_name = str(description)
var.unit = str(unite)
lat=C.createVariable('lat', np.float32, ('y','x'))
lon=C.createVariable('lon', np.float32, ('y','x')) 

time = C.createVariable('time', np.float64, ('time',))
time.long_name = 'time'

for var in ['lon','lat','time']:
    for att in nc_Modc.variables[var].ncattrs():
        setattr(C.variables[var],att,getattr(nc_Modc.variables[var],att))

time[:]=range(1,nt+1)
lat[:,:] = lats
lon[:,:] = lons
C.variables[str(indice)][:,:,:] = IND[::]
C.close()
    
```


```python
IND.shape
```




    (30, 130, 155)



## 4- Netcdf gridpoint extraction

In this example we will work with maximum daily temperature data from Regional Reanalysis (NARR) Regional Reanalysis. For more information about this product:

www.emc.ncep.noaa.gov/mmb/rreanl

The Netcdf files that we will open are daily values from January 1, 2017 to December 31, 2017. Files are archived by month.

The NARR grid point closest to the ECCC Montréal / McTavish weather station (45.5N, -73.8W) will be extracted here.

We first import the libraries.



```python
import netCDF4
import numpy as np
import pandas as pd
import datetime
from datetime import date, timedelta
from dateutil.relativedelta import relativedelta
```


```python
rep1='./DATA/NARR/'
model='NARR'
variable='tasmax'
variable_name='Temperature maximale'
yeari=2017
monthi=1
yearf = 2017
monthf = 12
station='Montreal' 
lati = 45.5
loni = -73.8

day_start=1
day_end = pd.date_range('{}-{}'.format(yearf, monthf), periods=1, freq='M').day.tolist()[0]
start=datetime.datetime(yeari,monthi,day_start)
end=datetime.datetime(yearf,monthf,day_end)
d0 = date(yeari, monthi, day_start)
d1 = date(yearf, monthf, day_end)
delta = d1 - d0
nb_days = delta.days+1
var_data=np.zeros(nb_days)

```

We define a function that will calculate the distance between each grid point of the Netcdf file and our reference latitude / longitude. We then deduce the minimum distance.

The other function allows us to increment our months when reading Netcdf files.


```python
def getclosest_ij(lats,lons,latpt,lonpt):
     # find squared distance of every point on grid
     dist_sq = (lats-latpt)**2 + (lons-lonpt)**2 
     # 1D index of minimum dist_sq element
     minindex_flattened = dist_sq.argmin()
     # Get 2D index for latvals and lonvals arrays from 1D index
     return np.unravel_index(minindex_flattened, lats.shape)

def add_month(now):
    try:
        then = (now + relativedelta(months=1)).replace(day=now.day)
    except ValueError:
        then = (now + relativedelta(months=2)).replace(day=1)
    return then
```

We can know apply our function over each grid point, month by month and save the value into a DataFrame. 


```python

i=0
IND=[]
# Début de notre boucle temporelle
incr=start
while incr <= end:
    filename= rep1 + model + '_' + variable + '_' + str(incr.year) + '{:02d}'.format(incr.month) + '.nc'   
    f = netCDF4.Dataset(filename)
   # print(f.variables.keys()) # get all variable names
    var = f.variables[variable] # temperature variable
    #print(temp) 
    #temp.dimensions
    #temp.shape
    lat, lon = f.variables['lat'], f.variables['lon']
    #print(lat)
    #print(lon)
    #print(lat[:])
    # extract lat/lon values (in degrees) to numpy arrays
    latvals = lat[:]; lonvals = lon[:] 
    # a function to find the index of the point closest pt
    # (in squared distance) to give lat/lon value.    
    iy_min, ix_min = getclosest_ij(latvals, lonvals, lati, loni)
    #print(iy_min)
    #print(ix_min)
    IND.append(var[:,iy_min,ix_min])
    incr=add_month(incr)
    
flattened_list = [y for x in IND for y in x]
start=datetime.datetime(yeari,monthi,day_start)
TIME=[]
for i in range(0,nb_days,1): 
 #   TIME.append((start+timedelta(days=i)).strftime("%Y-%m-%d"))
    TIME.append((start+timedelta(days=i)))
dataFrame_NARR = pd.DataFrame({'Date': TIME, variable_name: flattened_list}, columns = ['Date',variable_name]) 
dataFrame_NARR = dataFrame_NARR.set_index('Date')   
dataFrame_NARR.head()
```
| Date                |   Temperature maximale |
|:--------------------|-----------------------:|
| 2017-01-01 00:00:00 |              -0.893957 |
| 2017-01-02 00:00:00 |              -1.53144  |
| 2017-01-03 00:00:00 |              -1.73783  |
| 2017-01-04 00:00:00 |              -0.240698 |
| 2017-01-05 00:00:00 |              -0.791754 |


We save our DataFrame in csv. 


```python
dataFrame_NARR.to_csv('./DATA/NARR/NARR_'+station+'_1pt_'+str(variable)+'_'+ '{:02d}'.format(monthi) + str(yeari)+'_'+ '{:02d}'.format(monthf) + str(yearf)+'.csv')    
```

- Observation vs NARR
Now we have extracted our gridpoint near Montreal, we can compare these values with observations.   

We will extract the data from the Montreal McTavish station and put them in the NARR dataFrame. 


```python
dataframe_station = pd.read_csv('./DATA/station/MONTREAL_TAVISH_tasmax_1948_2017.csv', header=None, names=['Maximum temperature: OBS'])
start = date(1948, 1, 1)
end = date(2017, 12, 31)
delta=(end-start) 
nb_days = delta.days + 1 
rng = pd.date_range(start, periods=nb_days, freq='D')

dataframe_station['datetime'] = rng
dataframe_station.index = dataframe_station['datetime'] 
dataframe_station = dataframe_station.drop(["datetime"], axis=1)
```


```python
dataframe_station.head()
```
| datetime            |   Maximum temperature: OBS |
|:--------------------|---------------------------:|
| 1948-01-01 00:00:00 |                      -10   |
| 1948-01-02 00:00:00 |                       -3.9 |
| 1948-01-03 00:00:00 |                       -0.6 |
| 1948-01-04 00:00:00 |                       -2.8 |
| 1948-01-05 00:00:00 |                       -2.2 |


```python
dataFrame_NARR = dataFrame_NARR.rename(columns={"Temperature maximale": "Maximum temperature: NARR"})
df_NARR_Station = pd.concat([dataframe_station,dataFrame_NARR],axis=1)
df_NARR_Station.tail()
```

|                     |   Maximum temperature: OBS |   Maximum temperature: NARR |
|:--------------------|---------------------------:|----------------------------:|
| 2017-12-27 00:00:00 |                      -17.6 |                    -18.819  |
| 2017-12-28 00:00:00 |                      -20.5 |                    -19.3721 |
| 2017-12-29 00:00:00 |                      -18.4 |                    -16.4532 |
| 2017-12-30 00:00:00 |                      -17.3 |                    -16.2088 |
| 2017-12-31 00:00:00 |                      -18.3 |                    -16.7728 |


We want to plot valeurs for 2016 and 2017 years.


```python
df=df_NARR_Station.loc['2016' : '2017']
df.head()
```
|                     |   Maximum temperature: OBS |   Maximum temperature: NARR |
|:--------------------|---------------------------:|----------------------------:|
| 2016-01-01 00:00:00 |                       -0.1 |                         nan |
| 2016-01-02 00:00:00 |                        0.4 |                         nan |
| 2016-01-03 00:00:00 |                        0.2 |                         nan |
| 2016-01-04 00:00:00 |                      -13.5 |                         nan |
| 2016-01-05 00:00:00 |                       -7.5 |                         nan |


```python
import matplotlib.pyplot as plt
color = ['black', 'red']
fig = plt.figure(figsize=(16,8))
plt.plot(df.index, df['Maximum temperature: NARR'][:],  label='NARR Temperature', linewidth=2, c=color[0])
plt.plot(df.index, df['Maximum temperature: OBS'][:],  label='Observation Temperature', linewidth=2, c=color[1])

# Autre méthode pour tracer avec Pandas
#df_NARR_Station['2017'].plot(figsize=(10,5))

plt.xlabel("Time")
plt.ylabel("Temperature", {'color': 'black', 'fontsize': 10})
plt.title("Time serie: Station MTL vs NARR", y=1.05)
plt.legend(loc='upper left', ncol=1, bbox_to_anchor=(0, 1, 1, 0),fontsize =10)
plt.savefig("figures/NARR_time_Serie_temperature.png", dpi=300, bbox_inches='tight')   # bbox_inches= : option qui permet de propostionner le graphique lors de l'enregistrement
plt.show()

```


![png](/img/netcdf/output_39_0.png)


- Example of using the <b> .rolling () </ b> function to calculate a moving average on a signal.


```python
import matplotlib.pyplot as plt
df_NARR_Station['rollingmean5 Station']=  df_NARR_Station['Maximum temperature: OBS'].rolling(window=5).mean()
df_NARR_Station['rollingmean5 NARR']=  df_NARR_Station['Maximum temperature: NARR'].rolling(window=5).mean()
df_NARR_Station.tail()
```
|                     |   Maximum temperature: OBS |   Maximum temperature: NARR |   rollingmean5 Station |   rollingmean5 NARR |
|:--------------------|---------------------------:|----------------------------:|-----------------------:|--------------------:|
| 2017-12-27 00:00:00 |                      -17.6 |                    -18.819  |                  -8.04 |            -8.31893 |
| 2017-12-28 00:00:00 |                      -20.5 |                    -19.3721 |                 -11.12 |           -11.0995  |
| 2017-12-29 00:00:00 |                      -18.4 |                    -16.4532 |                 -13.88 |           -13.6478  |
| 2017-12-30 00:00:00 |                      -17.3 |                    -16.2088 |                 -16.12 |           -15.6138  |
| 2017-12-31 00:00:00 |                      -18.3 |                    -16.7728 |                 -18.42 |           -17.5252  |


```python
df_NARR_Station['2017-01':'2017-12'].plot(figsize=(16,8))
plt.xlabel("Temps")
plt.ylabel("Température")
plt.title("Maximum temperature time serie: Station MTL vs NARR", y=1.05)
plt.savefig("figures/NARR_time_Serie_temperature2.png", dpi=300, bbox_inches='tight')   # bbox_inches= : option qui permet de propostionner le graphique lors de l'enregistrement
plt.show()
```


![png](/img/netcdf/output_42_0.png)



```python

```


```python

```


```python

```
