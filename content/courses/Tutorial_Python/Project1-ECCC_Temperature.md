
---
title: Project 1 ECCC temperature data
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 9
---

![image0](/img/pylogo.png)

1: ECCC temperature data

In previous sections, we presented how to use the Pandas library which allowed us to process and manipulate data sets. Combining this with Python's Datetime and Matplotlib libraries, we were able to quickly visualize our data.

We will continue to discover the functionality of these libraries in a practical case by analyzing the daily temperature data recorded by one of the Environment and Climate Change Canada stations located in Montreal / McTavish between the period 1948 and 2017 (file named 'MONTREAL_tasmoy_1948_2017.txt' in ./DATA directory)

To complete and enrich our analysis, a new Python library will be presented: <b> Seaborn </b>.

- the Seaborn library is based on matplotlib.
- it allows to draw more complex graphs

For more information:

https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html

This link presents a gallery of chart types to be realized with Seaborn:
https://seaborn.pydata.org/examples/index.html

### 1- Opening and reading our time series


```python
import numpy as np
import pandas as pd
import datetime
from datetime import date
import numpy as np 
import warnings
warnings.filterwarnings("ignore")

df = pd.DataFrame()

# We open ascii file and store information in a new DataFrame
with open('./DATA/MONTREAL_tasmoy_1948_2017.txt', 'r') as file:
     rows = file.read()
data_EC_Montreal = [float(row) for row in rows.split()]
```

We have created a 1D field but we have no temporal information in our file.
Knowing that our registration covers the period 1948 - 2017, we will format our dates with the <b> datetime </b> module of Python. 


```python
# We know that the time series starts on January 1, 1948 and ends on December 31, 2017 inclusively
# We create a Datetime object instance to complete our DataFrame
start = date(1948, 1, 1)
end = date(2017, 12, 31)
delta=(end-start) 
nb_days = delta.days + 1 
rng = pd.date_range(start, periods=nb_days, freq='D')

# We will use DateTime object as DataFrame index
df['datetime'] = rng
df.index = df['datetime'] 

df['Temperature Montreal'] = data_EC_Montreal
df.head()
```
| datetime            | datetime            |   Temperature Montreal |
|:--------------------|:--------------------|-----------------------:|
| 1948-01-01 00:00:00 | 1948-01-01 00:00:00 |                  -12   |
| 1948-01-02 00:00:00 | 1948-01-02 00:00:00 |                   -8.9 |
| 1948-01-03 00:00:00 | 1948-01-03 00:00:00 |                   -3.4 |
| 1948-01-04 00:00:00 | 1948-01-04 00:00:00 |                   -3.4 |
| 1948-01-05 00:00:00 | 1948-01-05 00:00:00 |                   -3.1 |


```python
dir(df) # the dir () function allows to list the functions that are applicable to our DataFrame object
```
We assigned our time series in a Pandas DataFrame and then formatted the date as a Datetime object.

It is now easy to manipulate the dataset and apply some simple functions.

### 2- Calculation of indices on the temperature data

- We will develop and apply a function to calculate the quantiles of our distribution

- By resampling our series with the <b> .resample () </b> method of Pandas, we will see how to apply native functions of numpy and apply our own function.


```python
# Creating our index that calculates the quantile of the distribution
# We use the numpy .percentile () function
def percentile(n):
    def percentile_(x):
        return np.nanpercentile(x, n)
    percentile_.__name__ = 'percentile_%s' % n
    return percentile_         
```

- <b> .resample () </b> and <b> .agg () </b> methods of Pandas

The <b> .resample () </b> method is very useful for frequency conversion and time series resampling. The object (here DataFrame) must have a data / time index (DatetimeIndex) in order to be used.
Several resampling frequencies are available (time, week, month, season, year ...)

https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.resample.html


The <b> .agg () </b> method is used for aggregation of data according to a list of functions to be applied to each column, resulting in an aggregated result with a hierarchical index.

https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.agg.html

In our example, we will resample our data set by month and calculate for each month the average, the minimum, the maximum and the 90th and 95th quantiles.


```python
resamp_Montreal = df.resample('M').agg([np.mean, np.min, np.max, percentile(90), percentile(95)])
resamp_Montreal.head()
```
| datetime            |      mean |   amin |   amax |   percentile_90 |   percentile_95 |   year |   MonthNo | month   |
|:--------------------|----------:|-------:|-------:|----------------:|----------------:|-------:|----------:|:--------|
| 1948-01-31 00:00:00 | -10.9903  |  -23.4 |   -3.1 |           -3.6  |           -3.4  |   1948 |         1 | Jan     |
| 1948-02-29 00:00:00 |  -9.58621 |  -20.8 |    3.6 |           -2.64 |           -0.32 |   1948 |         2 | Feb     |
| 1948-03-31 00:00:00 |  -2.46129 |  -17.8 |    7.5 |            5.6  |            6.4  |   1948 |         3 | Mar     |
| 1948-04-30 00:00:00 |   6.64    |   -1.7 |   14.5 |           12.08 |           13.13 |   1948 |         4 | Apr     |
| 1948-05-31 00:00:00 |  12.6645  |    6.7 |   21.7 |           16.7  |           18.35 |   1948 |         5 | May     |



```python
# simple step to remove the row 'Temperature Montreal' 
resamp_Montreal = resamp_Montreal.loc[:,'Temperature Montreal'] 
resamp_Montreal.head() 
```

| datetime            |      mean |   amin |   amax |   percentile_90 |   percentile_95 |
|:--------------------|----------:|-------:|-------:|----------------:|----------------:|
| 1948-01-31 00:00:00 | -10.9903  |  -23.4 |   -3.1 |           -3.6  |           -3.4  |
| 1948-02-29 00:00:00 |  -9.58621 |  -20.8 |    3.6 |           -2.64 |           -0.32 |
| 1948-03-31 00:00:00 |  -2.46129 |  -17.8 |    7.5 |            5.6  |            6.4  |
| 1948-04-30 00:00:00 |   6.64    |   -1.7 |   14.5 |           12.08 |           13.13 |
| 1948-05-31 00:00:00 |  12.6645  |    6.7 |   21.7 |           16.7  |           18.35 |



### 3- Some examples of graphics with the Seaborn library

Now that we have some statistics on our DataFrame, we will use Python's Seaborn library to visualize them. 

![image0](/img/seaborn.png)

- Example: Heatmap

https://seaborn.pydata.org/generated/seaborn.heatmap.html


For example, we would like to observe the variation of the average temperature for all the months of the year and all the years. We are going to define two new columns in our DataFrame in which will be assigned only the years and the months respectively. 


```python
resamp_Montreal['year']  = resamp_Montreal.index.year
resamp_Montreal['MonthNo'] = resamp_Montreal.index.month
```


```python
resamp_Montreal.head()
```

| datetime            |      mean |   amin |   amax |   percentile_90 |   percentile_95 |   year |   MonthNo |
|:--------------------|----------:|-------:|-------:|----------------:|----------------:|-------:|----------:|
| 1948-01-31 00:00:00 | -10.9903  |  -23.4 |   -3.1 |           -3.6  |           -3.4  |   1948 |         1 |
| 1948-02-29 00:00:00 |  -9.58621 |  -20.8 |    3.6 |           -2.64 |           -0.32 |   1948 |         2 |
| 1948-03-31 00:00:00 |  -2.46129 |  -17.8 |    7.5 |            5.6  |            6.4  |   1948 |         3 |
| 1948-04-30 00:00:00 |   6.64    |   -1.7 |   14.5 |           12.08 |           13.13 |   1948 |         4 |
| 1948-05-31 00:00:00 |  12.6645  |    6.7 |   21.7 |           16.7  |           18.35 |   1948 |         5 |


Before we plot our heatmap, we need to reorganize our dataframe.
- The <b> .pivot_table () </b> method: this method allows you to cross tables dynamically.

https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html

We would like to visualize only the average monthly temperatures, so work with the 'mean' column, put the year in Index and have one month per column. The <b> .pivot_table () </b> method allows us to do this. 


```python
Montreal_pivot = resamp_Montreal.pivot_table(values='mean',index='year',columns=['MonthNo'])
Montreal_pivot.head()
```
|   year |         1 |        2 |         3 |       4 |       5 |       6 |       7 |       8 |       9 |       10 |        11 |       12 |
|-------:|----------:|---------:|----------:|--------:|--------:|--------:|--------:|--------:|--------:|---------:|----------:|---------:|
|   1948 | -10.9903  | -9.58621 | -2.46129  | 6.64    | 12.6645 | 17.7467 | 21.4903 | 21.1065 | 17.15   |  9.1     |  5.98333  | -2.52258 |
|   1949 |  -5.77419 | -5.69286 | -2.19677  | 7.51667 | 13.5129 | 20.56   | 22.871  | 21.5452 | 14.62   | 12.0258  | -0.193333 | -3.21935 |
|   1950 |  -5.34839 | -9.79643 | -4.89355  | 4.71    | 14.1161 | 18.9567 | 21.3258 | 19.1129 | 13.6167 | 10.1     |  3.95667  | -4.83548 |
|   1951 |  -7.35484 | -6.48571 | -0.490323 | 7.29667 | 14.4097 | 18.27   | 21.3129 | 18.6677 | 15.1333 | 10.371   |  0.18     | -5.3129  |
|   1952 |  -7.80323 | -5.27241 | -0.987097 | 7.99667 | 12.4065 | 19.6    | 23.0806 | 20.7323 | 16.03   |  7.67419 |  3.65667  | -3.18387 |

We then apply <b>.heatmap()</b> function on our DataFrame.


```python
import seaborn as sns 
import matplotlib.pyplot as plt 
ax = plt.axes()
sns.heatmap(Montreal_pivot)
figure = ax.get_figure()    
figure.set_size_inches(15, 10) 
plt.show()
```


    <Figure size 1500x1000 with 2 Axes>


We can improve our display.


```python
ax = plt.axes()
sns.heatmap(Montreal_pivot, cmap='RdYlGn_r', linewidths=0.5, annot=True , ax = ax,vmin=-30, vmax=30,center=0, fmt='.1f',yticklabels=True, cbar_kws={'label': 'Celcius'})
ax.set_title('Mean temperature', weight='bold', fontsize="x-large")
figure = ax.get_figure()    
figure.set_size_inches(22, 15) 
plt.show()
```


![png](/img/output_20_0.png)


- Other examples: Boxplot,  violin plot, line plot 

https://seaborn.pydata.org/generated/seaborn.boxplot.html

https://seaborn.pydata.org/generated/seaborn.violinplot.html

https://seaborn.pydata.org/generated/seaborn.lineplot.html

At first, we create a new variable containing the months but in string of characters. For this we apply the <b> .strftime () </b> method of datetime.


```python
resamp_Montreal['month'] = resamp_Montreal.index.strftime("%b")
```


```python
resamp_Montreal.head()
```

| datetime            |      mean |   amin |   amax |   percentile_90 |   percentile_95 |   year |   MonthNo | month   |
|:--------------------|----------:|-------:|-------:|----------------:|----------------:|-------:|----------:|:--------|
| 1948-01-31 00:00:00 | -10.9903  |  -23.4 |   -3.1 |           -3.6  |           -3.4  |   1948 |         1 | Jan     |
| 1948-02-29 00:00:00 |  -9.58621 |  -20.8 |    3.6 |           -2.64 |           -0.32 |   1948 |         2 | Feb     |
| 1948-03-31 00:00:00 |  -2.46129 |  -17.8 |    7.5 |            5.6  |            6.4  |   1948 |         3 | Mar     |
| 1948-04-30 00:00:00 |   6.64    |   -1.7 |   14.5 |           12.08 |           13.13 |   1948 |         4 | Apr     |
| 1948-05-31 00:00:00 |  12.6645  |    6.7 |   21.7 |           16.7  |           18.35 |   1948 |         5 | May     |


- Boxplot: 


```python
ax = plt.axes()
sns.boxplot(x="month", y="mean", data=resamp_Montreal, palette="Set1")  
figure = ax.get_figure()    
figure.set_size_inches(12, 8) 
plt.show()
```


![png](/img/output_26_0.png)


- Violin plot: 


```python
ax = plt.axes()
sns.violinplot(x="month", y="mean", data=resamp_Montreal, palette="Set1")  
figure = ax.get_figure()    
figure.set_size_inches(12, 8)
plt.show()
```


![png](/img/output_28_0.png)


- Line plot: 


```python
ax = plt.axes()
sns.lineplot(x=resamp_Montreal.index.year, y="mean",
             hue="month",
             data=resamp_Montreal,
             palette="tab10")
figure = ax.get_figure()    
figure.set_size_inches(12, 8)
plt.show()
```


![png](/img/output_30_0.png)



```python
sns.catplot(x="month", y="percentile_90", data=resamp_Montreal, kind="swarm")
plt.show()
```


![png](/img/output_31_0.png)


- We can combine several Seaborn charts:


```python
ax = plt.axes()
ax1 = plt.subplot2grid((2, 2), (0, 0), colspan=2)
sns.lineplot(x=resamp_Montreal.index.year, y="mean", hue="month", data=resamp_Montreal, palette="tab10")
ax2 = plt.subplot2grid((2, 2), (1, 0), colspan=1)
sns.boxplot(x="month", y="mean", data=resamp_Montreal, palette="tab10") 
ax3 = plt.subplot2grid((2, 2), (1, 1), colspan=1)
sns.violinplot(x="month", y="mean", data=resamp_Montreal, palette="tab10") 
figure = ax.get_figure()    
figure.set_size_inches(12, 8) 
plt.show()
```


![png](/img/output_33_0.png)


### 4- Fonction groupby

We previously see  <b>.groupby()</b>  method from Pandas.

https://www.tutorialspoint.com/python_pandas/python_pandas_groupby.htm

This method is very useful using datetime objects.


```python
resamp_Montreal.head()
```
| datetime            |      mean |   amin |   amax |   percentile_90 |   percentile_95 |   year |   MonthNo | month   |
|:--------------------|----------:|-------:|-------:|----------------:|----------------:|-------:|----------:|:--------|
| 1948-01-31 00:00:00 | -10.9903  |  -23.4 |   -3.1 |           -3.6  |           -3.4  |   1948 |         1 | Jan     |
| 1948-02-29 00:00:00 |  -9.58621 |  -20.8 |    3.6 |           -2.64 |           -0.32 |   1948 |         2 | Feb     |
| 1948-03-31 00:00:00 |  -2.46129 |  -17.8 |    7.5 |            5.6  |            6.4  |   1948 |         3 | Mar     |
| 1948-04-30 00:00:00 |   6.64    |   -1.7 |   14.5 |           12.08 |           13.13 |   1948 |         4 | Apr     |
| 1948-05-31 00:00:00 |  12.6645  |    6.7 |   21.7 |           16.7  |           18.35 |   1948 |         5 | May     |

We want to group our dataframe by month  with  <b>.groupeby()</b> method.

```python
resamp_Montreal_grouped  = resamp_Montreal.groupby("month") 
resamp_Montreal_grouped.groups     # Pour voir les groupes
```


    {'Apr': DatetimeIndex(['1948-04-30', '1949-04-30', '1950-04-30', '1951-04-30',
                    '1952-04-30', '1953-04-30', '1954-04-30', '1955-04-30',
                    '1956-04-30', '1957-04-30', '1958-04-30', '1959-04-30',
                    '1960-04-30', '1961-04-30', '1962-04-30', '1963-04-30',
                    '1964-04-30', '1965-04-30', '1966-04-30', '1967-04-30',
                    '1968-04-30', '1969-04-30', '1970-04-30', '1971-04-30',
                    '1972-04-30', '1973-04-30', '1974-04-30', '1975-04-30',
                    '1976-04-30', '1977-04-30', '1978-04-30', '1979-04-30',
                    '1980-04-30', '1981-04-30', '1982-04-30', '1983-04-30',
                    '1984-04-30', '1985-04-30', '1986-04-30', '1987-04-30',
                    '1988-04-30', '1989-04-30', '1990-04-30', '1991-04-30',
                    '1992-04-30', '1993-04-30', '1994-04-30', '1995-04-30',
                    '1996-04-30', '1997-04-30', '1998-04-30', '1999-04-30',
                    '2000-04-30', '2001-04-30', '2002-04-30', '2003-04-30',
                    '2004-04-30', '2005-04-30', '2006-04-30', '2007-04-30',
                    '2008-04-30', '2009-04-30', '2010-04-30', '2011-04-30',
                    '2012-04-30', '2013-04-30', '2014-04-30', '2015-04-30',
                    '2016-04-30', '2017-04-30'],
                   dtype='datetime64[ns]', name='datetime', freq='12M'),
     'Aug': DatetimeIndex(['1948-08-31', '1949-08-31', '1950-08-31', '1951-08-31',
                    '1952-08-31', '1953-08-31', '1954-08-31', '1955-08-31',
                    '1956-08-31', '1957-08-31', '1958-08-31', '1959-08-31',
                    '1960-08-31', '1961-08-31', '1962-08-31', '1963-08-31',
                    '1964-08-31', '1965-08-31', '1966-08-31', '1967-08-31',
                    '1968-08-31', '1969-08-31', '1970-08-31', '1971-08-31',
                    '1972-08-31', '1973-08-31', '1974-08-31', '1975-08-31',
                    '1976-08-31', '1977-08-31', '1978-08-31', '1979-08-31',
                    '1980-08-31', '1981-08-31', '1982-08-31', '1983-08-31',
                    '1984-08-31', '1985-08-31', '1986-08-31', '1987-08-31',
                    '1988-08-31', '1989-08-31', '1990-08-31', '1991-08-31',
                    '1992-08-31', '1993-08-31', '1994-08-31', '1995-08-31',
                    '1996-08-31', '1997-08-31', '1998-08-31', '1999-08-31',
                    '2000-08-31', '2001-08-31', '2002-08-31', '2003-08-31',
                    '2004-08-31', '2005-08-31', '2006-08-31', '2007-08-31',
                    '2008-08-31', '2009-08-31', '2010-08-31', '2011-08-31',
                    '2012-08-31', '2013-08-31', '2014-08-31', '2015-08-31',
                    '2016-08-31', '2017-08-31'],
                 ... }



- To iterate through groups: 

```python
for MonthNo,group in resamp_Montreal_grouped :                              
    print(MonthNo)
    print(group)
    
```

    Apr
                     mean  amin  amax  percentile_90  percentile_95  year  \
    datetime                                                                
    1948-04-30   6.640000  -1.7  14.5          12.08         13.130  1948   
    1949-04-30   7.516667   2.0  15.8          12.43         14.370  1949   
    1950-04-30   4.710000  -4.2  11.7           8.56         10.770  1950   
    1951-04-30   7.296667   1.4  15.0          11.78         13.105  1951   
    1952-04-30   7.996667  -1.4  15.3          14.01         15.000  1952   
    ...
    
    [70 rows x 8 columns]
    Aug
                     mean  amin  amax  percentile_90  percentile_95  year  \
    datetime                                                                
    1948-08-31  21.106452  15.0  27.8          26.40         27.400  1948   
    1949-08-31  21.545161  15.0  27.0          25.60         26.700  1949   
    1950-08-31  19.112903  12.5  23.4          22.50         23.050  1950   
    1951-08-31  18.667742  13.1  23.4          22.00         22.950  1951   
    1952-08-31  20.732258  14.2  25.6          23.40         25.300  1952   
    1953-08-31  20.480645  15.6  27.2          25.00         27.000  1953   
    1954-08-31  19.312903  12.8  24.5          22.00         23.350  1954   
    ...
    

- To select a group: get_group() 


```python
# we grouped our dataframe using month index
resamp_Montreal_grouped.get_group('Dec').head()
```
| datetime            |     mean |   amin |   amax |   percentile_90 |   percentile_95 |   year |   MonthNo | month   |
|:--------------------|---------:|-------:|-------:|----------------:|----------------:|-------:|----------:|:--------|
| 1948-12-31 00:00:00 | -2.52258 |  -15   |    7   |             2.2 |            3.9  |   1948 |        12 | Dec     |
| 1949-12-31 00:00:00 | -3.21935 |  -13.9 |    8.9 |             5.8 |            6.7  |   1949 |        12 | Dec     |
| 1950-12-31 00:00:00 | -4.83548 |  -23.4 |    3.9 |             0   |            1.95 |   1950 |        12 | Dec     |
| 1951-12-31 00:00:00 | -5.3129  |  -19.2 |   13.1 |             7   |           11.15 |   1951 |        12 | Dec     |
| 1952-12-31 00:00:00 | -3.18387 |  -17   |    7.8 |             2   |            4.6  |   1952 |        12 | Dec     |

- Aggregation:
Python has several methods are available to perform aggregations on data. It is done using the pandas and numpy libraries. The data must be available or converted to a dataframe to apply the aggregation functions.



```python
# to calculate 'percentile_90' in each  group. 
resamp_Montreal_grouped['percentile_90'].agg(np.mean)
```


    month
    Apr    12.434848
    Aug    24.283582
    Dec     1.790000
    Feb    -0.098529
    Jan    -1.046324
    Jul    25.119242
    Jun    23.557385
    Mar     5.021493
    May    19.483846
    Nov     8.615147
    Oct    15.280294
    Sep    21.236765
    Name: percentile_90, dtype: float64




```python
resamp_Montreal_grouped['percentile_90'].agg(np.size)
```




    month
    Apr    70.0
    Aug    70.0
    Dec    70.0
    Feb    70.0
    Jan    70.0
    Jul    70.0
    Jun    70.0
    Mar    70.0
    May    70.0
    Nov    70.0
    Oct    70.0
    Sep    70.0
    Name: percentile_90, dtype: float64



## Exercice :  

## Compute day degres index for Montreal station

1- open and read file "MONTREAL_tasmoy_1948_2017.txt"

2- Define datetime index (time range: 01/01/1948 : 31/12/2017 )

3- Write a function to compute the index

4- For each year, compute temperature mean, min , max and DG0 index

5- Make a plot




```python

```

1- 


```python
import numpy as np
with open('./data/MONTREAL_tasmoy_1948_2017.txt', 'r') as file:
     rows = file.read()
data_EC_Montreal = [float(row) for row in rows.split()]  
```

2- 


```python
import pandas as pd
import datetime
from datetime import date
df = pd.DataFrame()

start = date(1948, 1, 1)
end = date(2017, 12, 31)
delta=(end-start) 
nb_days = delta.days + 1 
rng = pd.date_range(start, periods=nb_days, freq='D')

df['datetime'] = rng
df.index = df['datetime'] 
df['Temperature Montreal'] = data_EC_Montreal
```

3- 


```python
def DG0(S):  
     ind_DGO=[]
     ind_DGO = sum(x for x in S if x >= 0)
     return ind_DGO  
```

4- 


```python
resamp = df.resample('AS')
dataset = resamp.agg([np.mean, np.min, np.max, DG0])
dataset.head()
```
| datetime            |   ('Temperature Montreal', 'mean') |   ('Temperature Montreal', 'amin') |   ('Temperature Montreal', 'amax') |   ('Temperature Montreal', 'DG0') |
|:--------------------|-----------------------------------:|-----------------------------------:|-----------------------------------:|----------------------------------:|
| 1948-01-01 00:00:00 |                            7.23388 |                              -23.4 |                               27.8 |                            3506.1 |
| 1949-01-01 00:00:00 |                            8.04767 |                              -15   |                               28.4 |                            3602.9 |
| 1950-01-01 00:00:00 |                            6.84877 |                              -23.6 |                               25.9 |                            3318.9 |
| 1951-01-01 00:00:00 |                            7.24521 |                              -24.2 |                               25.3 |                            3404.9 |
| 1952-01-01 00:00:00 |                            7.85546 |                              -20   |                               27.5 |                            3474.2 |




5- 


```python
dataset.columns = dataset.columns.droplevel(0)
```


```python
dataset['DG0'].head()
```




    datetime
    1948-01-01    3506.1
    1949-01-01    3602.9
    1950-01-01    3318.9
    1951-01-01    3404.9
    1952-01-01    3474.2
    Freq: AS-JAN, Name: DG0, dtype: float64




```python
import matplotlib.pyplot as plt
dataset['DG0'].plot(figsize=(12,5))
plt.show()
```


![png](/img/output_58_0.png)



```python
# we must filter missing values
def DG0bis(S):  
     ind_DGObis=[]      
     S_no_nan = S[~np.isnan(S)]
     N = len(S)
     N2 = len(S_no_nan)
     if ((N2/N) < 0.8): 
         ind_DGObis = np.empty(1)
         ind_DGObis = np.nan
     else:       
         ind_DGObis = sum(x for x in S if x >= 0)
     return ind_DGObis 
```


```python
dataset = resamp.agg([np.mean, np.min, np.max, DG0, DG0bis])
dataset.head()
```

| datetime            |   ('Temperature Montreal', 'mean') |   ('Temperature Montreal', 'amin') |   ('Temperature Montreal', 'amax') |   ('Temperature Montreal', 'DG0') |   ('Temperature Montreal', 'DG0bis') |
|:--------------------|-----------------------------------:|-----------------------------------:|-----------------------------------:|----------------------------------:|-------------------------------------:|
| 1948-01-01 00:00:00 |                            7.23388 |                              -23.4 |                               27.8 |                            3506.1 |                               3506.1 |
| 1949-01-01 00:00:00 |                            8.04767 |                              -15   |                               28.4 |                            3602.9 |                               3602.9 |
| 1950-01-01 00:00:00 |                            6.84877 |                              -23.6 |                               25.9 |                            3318.9 |                               3318.9 |
| 1951-01-01 00:00:00 |                            7.24521 |                              -24.2 |                               25.3 |                            3404.9 |                               3404.9 |
| 1952-01-01 00:00:00 |                            7.85546 |                              -20   |                               27.5 |                            3474.2 |                               3474.2 |


```python
dataset.columns = dataset.columns.droplevel(0)
```


```python
dataset['DG0'].plot(figsize=(12,5))
dataset['DG0bis'].plot(figsize=(12,5))
plt.show()
```


![png](/img/output_62_0.png)

