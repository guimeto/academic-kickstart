
---
title: 2 Netcdf Part 2  
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python Netcdf 
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

Instead of extracting a grid point, we may want to extract a domain / box delimited by latitudes and longitudes.

In this example we will work with the annual mean of daily maximum temperature data from several regional models of CORDEX-NAM44.

We will extract all the grid points from the region between <b> 47degN and 51degN of latitude and between -72degW and -64degW of longitude </b>.

We will then plot the inter-annual variability of the mean annual temperature anomalies. 



![image0](/img/netcdf/CORDEX_domaine.png)

```python
# we first inmport librairies
import netCDF4
import numpy as np
import pandas as pd
from datetime import datetime
import matplotlib.pylab as plt
import warnings; warnings.filterwarnings(action='ignore')
import seaborn as sns
from matplotlib import gridspec

# path and variable name
rep='./DATA/Inter_annual_anomaly/'
variable_in = 'Mean_tasmax'

# list of periods we want to use
list_period = ['2011-2040','2041-2070','2071-2100']

# list of models
list_rcp45 = ['CRCM5-v1_NAM-44_ll_CCCma-CanESM2_rcp45', 'CRCM5-v1_NAM-44_ll_MPI-M-MPI-ESM-LR_rcp45' ]

# Area to extract
latbounds = [ 47 , 51 ]
lonbounds = [ -72 , -64 ] 
```

We will make a loop over each model and period to make the extraction:


```python
# 
df_rcp45 = []
matrix_45 = []
for period in list_period: 
    globals()['flattened_list_'+period] = []  # we define a global variable 
    for i in range(0,len(list_rcp45)):
        filename= rep +'anomalie_' +  list_rcp45[i] +  '_' + variable_in + '_' + period  + '_1971-2000.nc'   
        nc = netCDF4.Dataset(filename)
        # we here read netcdf values
        var = nc.variables[variable_in][:]  
        lats = nc.variables['lat'][:]; lons = nc.variables['lon'][:]
        # in this part, we extract our domain 
        subset = ((lats > latbounds[0]) & (lats < latbounds[1]) & 
             (lons > lonbounds[0]) & (lons < lonbounds[1]))
        data=pd.DataFrame(var[:,subset], dtype='float') 
        globals()['flattened_list_'+period].append(data.mean(axis=1))
        
    df_rcp45.append(pd.DataFrame(globals()['flattened_list_'+period]).T) 
    
df_rcp45 = pd.concat(df_rcp45)
df_rcp45.head()
```
|    |        0 |          1 |
|---:|---------:|-----------:|
|  0 | 1.72084  | -0.288691  |
|  1 | 1.4762   |  0.885357  |
|  2 | 0.581686 |  0.541863  |
|  3 | 0.390671 | -0.0141989 |
|  4 | 1.14842  |  1.29417   |


We can add datetime index in our DataFrame.


```python
TIME=[]
for y in range(int(list_period[0].split('-')[0]),int(list_period[-1].split('-')[-1])+1,1):
    TIME.append(datetime.strptime(str(y), '%Y'))
    
df_rcp45['Date'] = TIME   
df_rcp45.index = df_rcp45['Date']
df_rcp45 = df_rcp45.drop(["Date"], axis=1) 
df_rcp45.head()
```
| Date                |        0 |          1 |
|:--------------------|---------:|-----------:|
| 2011-01-01 00:00:00 | 1.72084  | -0.288691  |
| 2012-01-01 00:00:00 | 1.4762   |  0.885357  |
| 2013-01-01 00:00:00 | 0.581686 |  0.541863  |
| 2014-01-01 00:00:00 | 0.390671 | -0.0141989 |
| 2015-01-01 00:00:00 | 1.14842  |  1.29417   |





We then want, for each year, the intra-model variability. For this, we will calculate the minimum and maximum values by applying the <b> .apply </b> method.


```python
df_rcp45['min'] = df_rcp45.apply(np.min, axis=1)
df_rcp45['max'] = df_rcp45.apply(np.max, axis=1)
df_rcp45['mean'] = df_rcp45.apply(np.mean, axis=1)
df_rcp45.head()
```
| Date                |        0 |          1 |        min |      max |     mean |
|:--------------------|---------:|-----------:|-----------:|---------:|---------:|
| 2011-01-01 00:00:00 | 1.72084  | -0.288691  | -0.288691  | 1.72084  | 0.716076 |
| 2012-01-01 00:00:00 | 1.4762   |  0.885357  |  0.885357  | 1.4762   | 1.18078  |
| 2013-01-01 00:00:00 | 0.581686 |  0.541863  |  0.541863  | 0.581686 | 0.561774 |
| 2014-01-01 00:00:00 | 0.390671 | -0.0141989 | -0.0141989 | 0.390671 | 0.188236 |
| 2015-01-01 00:00:00 | 1.14842  |  1.29417   |  1.14842   | 1.29417  | 1.2213   |



We will make the same work with RCMs in future condition with rcp8.5 scenario and RCMs in historical conditions.


```python
list_rcp85 = ['CRCM5-v1_NAM-44_ll_CCCma-CanESM2_rcp85','CRCM5-v1_NAM-44_ll_MPI-M-MPI-ESM-MR_rcp85']
df_rcp85 = []
matrix_85 = []
for period in list_period: 
    globals()['flattened_list_'+period] = []
    for i in range(0,len(list_rcp85)):
        filename= rep + 'anomalie_' +  list_rcp85[i] +  '_' + variable_in + '_' + period  + '_1971-2000.nc'   
        nc = netCDF4.Dataset(filename)
        var = nc.variables[variable_in][:]  
        lats = nc.variables['lat'][:]; lons = nc.variables['lon'][:]            
        subset = ((lats > latbounds[0]) & (lats < latbounds[1]) & 
             (lons > lonbounds[0]) & (lons < lonbounds[1]))
        #mask = np.where(subset)
        data=pd.DataFrame(var[:,subset], dtype='float') 
        globals()['flattened_list_'+period].append(data.mean(axis=1))        
    df_rcp85.append(pd.DataFrame(globals()['flattened_list_'+period]).T) 
    
df_rcp85 = pd.concat(df_rcp85)
df_rcp85['Date'] = TIME   
df_rcp85.index = df_rcp85['Date']
df_rcp85 = df_rcp85.drop(["Date"], axis=1)  

df_rcp85['min'] = df_rcp85.apply(np.min, axis=1)
df_rcp85['max'] = df_rcp85.apply(np.max, axis=1)
df_rcp85['mean'] = df_rcp85.apply(np.mean, axis=1)

### historical RCMs
list_histo = ['CRCM5-v1_NAM-44_ll_CCCma-CanESM2_historical', 'CRCM5-v1_NAM-44_ll_MPI-M-MPI-ESM-LR_historical']
df_histo = []
globals()['flattened_list_'+period] = []
for i in range(0,len(list_histo)):
    filename= rep + 'anomalie_' +  list_histo[i] +  '_' + variable_in + '_1971-2000_1971-2000.nc'   
    nc = netCDF4.Dataset(filename)
    var = nc.variables[variable_in][:]  
    lats = nc.variables['lat'][:]; lons = nc.variables['lon'][:]
    
    subset = ((lats > latbounds[0]) & (lats < latbounds[1]) & 
         (lons > lonbounds[0]) & (lons < lonbounds[1]))
    #mask = np.where(subset)
    data=pd.DataFrame(var[:,subset], dtype='float') 
    globals()['flattened_list_'+period].append(data.mean(axis=1))        
df_histo.append(pd.DataFrame(globals()['flattened_list_'+period]).T) 
TIME=[]
for y in range(1971,2001,1):
    TIME.append(datetime.strptime(str(y), '%Y'))  
    
df_histo = pd.concat(df_histo)
df_histo['Date'] = TIME   
df_histo.index = df_histo['Date']
df_histo = df_histo.drop(["Date"], axis=1)  

df_histo['min'] = df_histo.apply(np.min, axis=1)
df_histo['max'] = df_histo.apply(np.max, axis=1)
df_histo['mean'] = df_histo.apply(np.mean, axis=1)
```

We put all results in the same DataFrame: 


```python
result = []
result = pd.DataFrame({'min_rcp45': df_rcp45['min'], 'max_rcp45': df_rcp45['max'],'mean_rcp45': df_rcp45['mean'],
                       'min_rcp85': df_rcp85['min'], 'max_rcp85': df_rcp85['max'],'mean_rcp85': df_rcp85['mean'],
                       'min_histo': df_histo['min'], 'max_histo': df_histo['max'],'mean_histo': df_histo['mean']},
        columns = ['min_rcp45','max_rcp45','mean_rcp45','min_rcp85','max_rcp85','mean_rcp85','min_histo','max_histo','mean_histo']) 

result.tail()
```
| Date                |   min_rcp45 |   max_rcp45 |   mean_rcp45 |   min_rcp85 |   max_rcp85 |   mean_rcp85 |   min_histo |   max_histo |   mean_histo |
|:--------------------|------------:|------------:|-------------:|------------:|------------:|-------------:|------------:|------------:|-------------:|
| 2096-01-01 00:00:00 |     1.89008 |     4.49628 |      3.19318 |     5.44184 |     8.03633 |      6.73908 |         nan |         nan |          nan |
| 2097-01-01 00:00:00 |     3.86389 |     5.06262 |      4.46325 |     6.10506 |     7.35563 |      6.73034 |         nan |         nan |          nan |
| 2098-01-01 00:00:00 |     2.28996 |     4.60365 |      3.4468  |     6.58306 |     7.14778 |      6.86542 |         nan |         nan |          nan |
| 2099-01-01 00:00:00 |     2.94984 |     4.26892 |      3.60938 |     6.40518 |     7.04316 |      6.72417 |         nan |         nan |          nan |
| 2100-01-01 00:00:00 |     2.99867 |     3.27685 |      3.13776 |     6.16794 |     6.96608 |      6.56701 |         nan |         nan |          nan |


We can now plot our inter-annual variability:


```python
color = ['black','blue', 'red']
fig = plt.figure(figsize=(10, 6)) 
gs = gridspec.GridSpec(1, 2, width_ratios=[6, 1]) 
gs.update( wspace=0.04)
ax1 = plt.subplot(gs[0])

plt.rcParams["figure.figsize"]=[16,9]       #  
plt.plot(result.index.year, result['mean_histo'][:],  label='RCMs historical', linewidth=2, c=color[0])
plt.plot(result.index.year, result['mean_rcp45'][:],  label='RCMs scenario rcp 4.5', linewidth=2, c=color[1])
plt.plot(result.index.year, result['mean_rcp85'][:],  label='RCMs scenario rcp 8.5', linewidth=2, c=color[2])

plt.fill_between(result.index.year,result['min_histo'],result['max_histo'], color = color[0], alpha=.2)
plt.fill_between(result.index.year,result['min_rcp45'],result['max_rcp45'], color =  color[1], alpha=.2)
plt.fill_between(result.index.year,result['min_rcp85'],result['max_rcp85'], color =  color[2], alpha=.2)
plt.legend(loc="upper left", markerscale=1., scatterpoints=1, fontsize=20)

plt.xticks(range(result.index.year[0]-1, result.index.year[-1]+1, 10), fontsize=14)
plt.yticks( fontsize=14)

ax1.grid(axis = "x", linestyle = "--", color='black', linewidth=0.25, alpha=0.5)
ax1.grid(axis = "y", linestyle = "--", color='black', linewidth=0.25, alpha=0.5)

plt.setp(plt.gca().get_xticklabels(), rotation=45, ha="right")

plt.xlabel('Date', fontsize=20, color='black', weight='semibold')
plt.ylabel('°C', fontsize=20, color='black', weight='semibold')
plt.title('Annual change in daily maximum temperature: (1971-2100) compared with normal (1971-2000)', fontsize=20, color='black', weight='semibold')
 
ax1.set_facecolor('white')
plt.yticks( fontsize=14)
plt.show()  

```


![png](/img/netcdf/output_13_1.png)


We would add next to our chart a boxplot on all models for the period 1971-2000 and 2071-2100 only.
We will extract these periods from our matrix result = []


```python
list_to_remove = ['min','max','mean']
df_histo = df_histo.drop(list_to_remove, axis=1)  
df_rcp45 = df_rcp45.drop(list_to_remove, axis=1)  
df_rcp85 = df_rcp85.drop(list_to_remove, axis=1) 
df_histo = df_histo.loc['1971' : '2010'].stack()
df_rcp45 = df_rcp45.loc['2071' : '2100'].stack()
df_rcp85 = df_rcp85.loc['2071' : '2100'].stack()

matrix_box = pd.DataFrame({'RCMs_histo': df_histo, 'RCMs_rcp45': df_rcp45,'RCMs_rcp85': df_rcp85},
        columns = ['RCMs_histo','RCMs_rcp45','RCMs_rcp85'])
matrix_box.head()
```
|                                       |   RCMs_histo |   RCMs_rcp45 |   RCMs_rcp85 |
|:--------------------------------------|-------------:|-------------:|-------------:|
| (Timestamp('1971-01-01 00:00:00'), 0) |   -1.34157   |          nan |          nan |
| (Timestamp('1971-01-01 00:00:00'), 1) |   -0.12412   |          nan |          nan |
| (Timestamp('1972-01-01 00:00:00'), 0) |   -0.641267  |          nan |          nan |
| (Timestamp('1972-01-01 00:00:00'), 1) |   -0.0350673 |          nan |          nan |
| (Timestamp('1973-01-01 00:00:00'), 0) |    0.0541643 |          nan |          nan |

```python
color = ['black','blue', 'red']
fig = plt.figure(figsize=(22, 12)) 
gs = gridspec.GridSpec(1, 2, width_ratios=[6, 1]) 
gs.update( wspace=0.04)
ax1 = plt.subplot(gs[0])

plt.rcParams["figure.figsize"]=[16,9]       #  
plt.plot(result.index.year, result['mean_histo'][:],  label='RCMs historical', linewidth=2, c=color[0])
plt.plot(result.index.year, result['mean_rcp45'][:],  label='RCMs scenario rcp 4.5', linewidth=2, c=color[1])
plt.plot(result.index.year, result['mean_rcp85'][:],  label='RCMs scenario rcp 8.5', linewidth=2, c=color[2])

plt.fill_between(result.index.year,result['min_histo'],result['max_histo'], color = color[0], alpha=.2)
plt.fill_between(result.index.year,result['min_rcp45'],result['max_rcp45'], color =  color[1], alpha=.2)
plt.fill_between(result.index.year,result['min_rcp85'],result['max_rcp85'], color =  color[2], alpha=.2)
plt.legend(loc="upper left", markerscale=1., scatterpoints=1, fontsize=20)

#ax.set_xlim(result.index.year[0], result.index.year[-1])
plt.xticks(range(result.index.year[0]-1, result.index.year[-1]+1, 10), fontsize=14)
plt.yticks( fontsize=14)

ax1.grid(axis = "x", linestyle = "--", color='black', linewidth=0.25, alpha=0.5)
ax1.grid(axis = "y", linestyle = "--", color='black', linewidth=0.25, alpha=0.5)

plt.setp(plt.gca().get_xticklabels(), rotation=45, ha="right")

plt.xlabel('Date', fontsize=20, color='black', weight='semibold')
plt.ylabel('°C', fontsize=20, color='black', weight='semibold')
plt.title('Annual change in daily maximum temperature: (1971-2100) compared with normal (1971-2000)', fontsize=20, color='black', weight='semibold')


my_pal = {"RCMs_histo": "grey", "RCMs_rcp45": "blue", "RCMs_rcp85":"red"}
ax2 = plt.subplot(gs[1])
#ax2 = matrix_box.boxplot(column=['RCMs_histo', 'RCMs_rcp45', 'RCMs_rcp85'])
ax2 = sns.boxplot(data=matrix_box, palette=my_pal)  
# Add transparency to colors
for patch in ax2.artists:
 r, g, b, a = patch.get_facecolor()
 patch.set_facecolor((r, g, b, .2))
plt.setp(plt.gca().get_xticklabels(), rotation=45, ha="right")
 
ax1.set_facecolor('white')
ax2.set_facecolor('white')
ax2.spines['top'].set_visible(False)
ax2.spines['bottom'].set_visible(False)
ax2.spines['right'].set_visible(False)
ax2.spines['left'].set_visible(False)

medians = matrix_box.median().values
median_labels = [str(np.round(s, 2))+' °C' for s in medians]
pos = range(len(medians))
i=0
for tick,label in zip(pos,ax2.get_xticklabels()):
    ax2.text(pos[tick], medians[tick] + 0.1, median_labels[tick], 
            horizontalalignment='center', size='medium', color = color[i], weight='semibold')
    i+=1
x1, x2, x3 = 0, 1, 2
ax2.text(x1, matrix_box.min().min().round()-0.15 , "1971-2000", ha='center', va='bottom', size='medium', color='black', weight='semibold')   
ax2.text((x2+x3)*.5, matrix_box.min().median()-0.4 , "2071-2100", ha='center', va='bottom', size='medium', color='black', weight='semibold')
plt.yticks( fontsize=14)
    
plt.savefig('./figures/VI_YEAR_Mean_tasmax.png', bbox_inches='tight', format='png', dpi=1000)
plt.show()  
```


![png](/img/netdf/output_16_0.png)



```python

```


```python

```
