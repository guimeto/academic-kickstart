---
title: 7 Pandas library
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 7
---

![image0](/img/pandas.png)
<img src="./figures/pandas.png" alt="Indentation" width="30%" height="30%">




Pandas is a library specialized in data manipulation. This library contains a set of optimized functions for handling large datasets. It allows to create and export tables of data from text files (separators, .csv, fixed format, compressed), binary (HDF5 with Pytable), HTML, XML, JSON, MongoDB, SQL ...

A new data structure is used with this library: the DataFrame. There are two types of data with pandas: <b>series</b> and <b>dataframes</b>.

- a dataframe is an array that is created with dictionaries or lists
- they are based on Numpy or ndarray tables
- they can have column and line names
- they have the particularity of being able to mix the types of data: str, float, Nan, Int ...

- they can be viewed as an excel sheet but with a larger number of data volumes and a larger number of functions and attributes.


## 7.1 Series introduction  - 

Series is a one-dimensional labeled array capable of holding data of any type (integer, string, float, python objects, etc.). The axis labels are collectively called index. 
```python
# first, we must import Pandas library
import pandas as pd      # aliasing as pd
import warnings; warnings.filterwarnings(action='ignore')
```

A pandas Series can be created using the following constructor:


```python
serie = pd.Series([11,15,12,13,14])
print(serie)
```

    0    11
    1    15
    2    12
    3    13
    4    14
    dtype: int64
    
We have in series, indexes and values. These indexes can be replaced by text with the index option. Be careful, the number of indexes must correspond to the number of values. 

```python
serie = pd.Series([11,15,12,13,14], index=["Montreal", "Ottawa", "Toronto", "Gatineau", "Quebec"])
```
```python
print(serie)
```
    Montreal    11
    Ottawa      15
    Toronto     12
    Gatineau    13
    Quebec      14
    dtype: int64
   
The describe() method computes a summary of statistic


```python
serie.describe()
```
    count     5.000000
    mean     13.000000
    std       1.581139
    min      11.000000
    25%      12.000000
    50%      13.000000
    75%      14.000000
    max      15.000000
    dtype: float64

We can use index to access to an element. 

```python
serie["Montreal"]
```




    11



We can use index number.  


```python
serie[3]
```




    13



We can use several indexes.


```python
serie[["Montreal", "Quebec", "Toronto"]]
```

    Montreal    11
    Quebec      14
    Toronto     12
    dtype: int64

There are large number of methods collectively compute descriptive statistics such as min(), max(), sum() ... 

```python
serie.min()
```




    11




```python
serie.max()
```




    15



We can apply comparison operators. 


```python
serie[serie>12]
```




    Ottawa      15
    Gatineau    13
    Québec      14
    dtype: int64




```python
serie>12 
```




    Montréal    False
    Ottawa       True
    Toronto     False
    Gatineau     True
    Québec       True
    dtype: bool



## 7.2 Pandas Dataframes 

Pandas DataFrame is two-dimensional size-mutable, potentially heterogeneous tabular data structure with labeled axes (rows and columns). A Data frame is a two-dimensional data structure, i.e., data is aligned in a tabular fashion in rows and columns. Pandas DataFrame consists of three principal components, the data, rows, and columns.

### 7.2.1  Create a  Dataframe

In the real world, a Pandas DataFrame will be created by loading the datasets from existing storage, storage can be SQL Database, CSV file, and Excel file. Pandas DataFrame can be created from the lists, dictionary, and from a list of dictionary etc. Dataframe can be created in different ways here are some ways by which we create a dataframe:

 ### - a) Using a Numpy array


```python
import numpy as np  
stations = np.genfromtxt("./DATA/DATA_Barrage_1963_2017_5.csv", delimiter=",", dtype='float')   
stations
```
    array([[  39.7       ,   39.09      ,   39.55645161,   23.23      ,
              22.5       ,   22.85903226, 2390.52612903, 3164.97      ,
            1673.8       ],
           [  41.16      ,   40.96      ,   41.08806452,   23.22      ,
              22.43      ,   22.7583871 , 2227.28290323, 3008.18      ,
            1697.87      ],
           [  41.15      ,   41.05      ,   41.11322581,   23.35      ,
              22.87      ,   23.15548387, 2851.27419355, 3231.8       ,
            2367.85      ],
           [  41.09      ,   40.61      ,   40.9683871 ,   23.78      ,
              22.7       ,   23.03258065, 2635.03774194, 3967.33      ,
            2069.65      ],
           [  41.09      ,   39.6       ,   40.26967742,   24.24      ,
              22.87      ,   23.64580645, 3924.23451613, 5407.32      ,
            2417.89      ]])


To create the dataframe, we use the Pandas <b> DataFrame () </b> function. It is at this stage that we define the names of our columns. In input we put the table Numpy. 

```python
dataframe = pd.DataFrame(stations, columns=["Amont Max", "Amont Min", "Amont Mean", "Aval Max", "Aval Max", "Aval Mean", "Debit Mean", "Debit Max","Debit Min"])
dataframe
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
      <th>Amont Max</th>
      <th>Amont Min</th>
      <th>Amont Mean</th>
      <th>Aval Max</th>
      <th>Aval Max</th>
      <th>Aval Mean</th>
      <th>Debit Mean</th>
      <th>Debit Max</th>
      <th>Debit Min</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>39.70</td>
      <td>39.09</td>
      <td>39.556452</td>
      <td>23.23</td>
      <td>22.50</td>
      <td>22.859032</td>
      <td>2390.526129</td>
      <td>3164.97</td>
      <td>1673.80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41.16</td>
      <td>40.96</td>
      <td>41.088065</td>
      <td>23.22</td>
      <td>22.43</td>
      <td>22.758387</td>
      <td>2227.282903</td>
      <td>3008.18</td>
      <td>1697.87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41.15</td>
      <td>41.05</td>
      <td>41.113226</td>
      <td>23.35</td>
      <td>22.87</td>
      <td>23.155484</td>
      <td>2851.274194</td>
      <td>3231.80</td>
      <td>2367.85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.09</td>
      <td>40.61</td>
      <td>40.968387</td>
      <td>23.78</td>
      <td>22.70</td>
      <td>23.032581</td>
      <td>2635.037742</td>
      <td>3967.33</td>
      <td>2069.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41.09</td>
      <td>39.60</td>
      <td>40.269677</td>
      <td>24.24</td>
      <td>22.87</td>
      <td>23.645806</td>
      <td>3924.234516</td>
      <td>5407.32</td>
      <td>2417.89</td>
    </tr>
  </tbody>
</table>
</div>



### - b) Create Dataframe loading csv file: <b>read_table()</b> or <b>read_csv()</b> function

- <b> read_table () </b> and <b> read_csv () </b> are the most useful functions under Pandas for reading text files and generating a DataFrame.

We will work with a dataset from a hydraulic dam.
Our csv file has 9 variables, the first line gives us the names of the variables (or labels).

A csv document can be read with the <b> read_table () </b> function, with the separator attribute ",".


```python
barrage = pd.read_table("./DATA/DATA_EXTREME_Carillon_1963_2017_5.csv", sep=",")
barrage.head()
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
      <th>Amont_max</th>
      <th>Amont_min</th>
      <th>Amont_moyen</th>
      <th>Aval_max</th>
      <th>Aval_min</th>
      <th>Aval_moyen</th>
      <th>Debit_Moyen</th>
      <th>Debit_max</th>
      <th>Debit_min</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>39.70</td>
      <td>39.09</td>
      <td>39.556452</td>
      <td>23.23</td>
      <td>22.50</td>
      <td>22.859032</td>
      <td>2390.526129</td>
      <td>3164.97</td>
      <td>1673.80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41.16</td>
      <td>40.96</td>
      <td>41.088065</td>
      <td>23.22</td>
      <td>22.43</td>
      <td>22.758387</td>
      <td>2227.282903</td>
      <td>3008.18</td>
      <td>1697.87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41.15</td>
      <td>41.05</td>
      <td>41.113226</td>
      <td>23.35</td>
      <td>22.87</td>
      <td>23.155484</td>
      <td>2851.274194</td>
      <td>3231.80</td>
      <td>2367.85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.09</td>
      <td>40.61</td>
      <td>40.968387</td>
      <td>23.78</td>
      <td>22.70</td>
      <td>23.032581</td>
      <td>2635.037742</td>
      <td>3967.33</td>
      <td>2069.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41.09</td>
      <td>39.60</td>
      <td>40.269677</td>
      <td>24.24</td>
      <td>22.87</td>
      <td>23.645806</td>
      <td>3924.234516</td>
      <td>5407.32</td>
      <td>2417.89</td>
    </tr>
  </tbody>
</table>
</div>


However, if we know that our file to read is a csv, we can use a simpler function of Pandas which is <b> read_csv () </b>.

No need to use sep='' option. He will find the separator by default.

```python
help(pd.read_csv)
```
Several options are available to the read_csv () function. It is important to know the list of possibilities and options offered by this simple command.

|  |  |
|--|--|
| <b>path</b> | Path to our file |
| <b>sep</b>| Delimiter like , ; \t or \s+ for a variable number of spaces |
| <b>header</b>| default 0, the first line contains the name of the variables; if None the names are generated or defined later |
| <b>index_col</b>| Names or numbers of columns defining the indexes of lines, indexes which can be hierarchized |
| <b>names</b>| If header = None, list of variable names |
| <b>nrows</b>| Useful for testing and limiting the number of lines to read |
| <b>skiprow</b>| List of lines to jump in reading |
| <b>skip_footer</b>| Number of lines to jump at the end of file |
| <b>na_values</b>| Definition of the code or codes signaling missing values. They can be defined in a dictionary to associate variables and codes specific missing values |
| <b>usecols</b>| Selects a list of variables to read to avoid reading large or unnecessary fields or variables |
| <b>skip_blank_lines</b>| If <b> True </b>, we skip the white lines |
| <b>thousand</b>| Separator: "." or "," |

```python
# Using example

file1 = "./DATA/DATA_EXTREME_Carillon_1963_2017_5.csv"
col_names = ['Variable1', 'Variable2', 'Variable3']
df2 = pd.read_csv(file1, skiprows=1, usecols=[0, 1, 3], names=col_names)
```
```python
df2.head()
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
      <th>Variable1</th>
      <th>Variable2</th>
      <th>Variable3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>39.70</td>
      <td>39.09</td>
      <td>23.23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41.16</td>
      <td>40.96</td>
      <td>23.22</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41.15</td>
      <td>41.05</td>
      <td>23.35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.09</td>
      <td>40.61</td>
      <td>23.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41.09</td>
      <td>39.60</td>
      <td>24.24</td>
    </tr>
  </tbody>
</table>
</div>



### <b>- c)</b> Create Dataframe loading ascii file: 


```python
with open('./DATA/Daily_Precipitation_1963-2017.txt', 'r') as file:
        rows = file.read() 
```


```python
with open('./DATA/Daily_Precipitation_1963-2017.txt', 'r') as file:
        rows = file.read()      
dataset = [float(row) for row in rows.split()]   
df3 = pd.DataFrame({"Precipitation" : dataset})
```


```python
df3.head()
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
      <th>Precipitation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



### <b>- d)</b> Create Dataframe loading excell (.xls) file: <b>read_excel()</b> function

We will open here an excel file (.xls extension). This file is a database containing information on all homogenized Environmental and Climate Change Canada temperature stations.

This database has 11 columns with data starting at the 4 th line.


We will define the "Province" column as index of our DataFrame.


```python
df4 = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", index_col=0,skiprows = range(0, 3))
df4.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



### 7.2.2  Access data from DataFrames 

The first thing to do when opening a new dataset is print out a few rows. We accomplish this with <b>.head()</b> method:

```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.head()
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
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BC</td>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



To see the last five rows use  <b>.tail()</b> method. tail() also accepts a number, and in this case we printing the bottom two rows.:


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.tail()
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
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>333</th>
      <td>NL</td>
      <td>PORT AUXBASQUES</td>
      <td>8402975</td>
      <td>1909</td>
      <td>2</td>
      <td>2017</td>
      <td>9</td>
      <td>47.58</td>
      <td>-58.97</td>
      <td>40</td>
      <td>N</td>
    </tr>
    <tr>
      <th>334</th>
      <td>NL</td>
      <td>ST ANTHONY</td>
      <td>8403389</td>
      <td>1946</td>
      <td>6</td>
      <td>2017</td>
      <td>12</td>
      <td>51.37</td>
      <td>-55.60</td>
      <td>33</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>335</th>
      <td>NL</td>
      <td>ST JOHN'S</td>
      <td>8403505</td>
      <td>1874</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>47.62</td>
      <td>-52.75</td>
      <td>141</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>336</th>
      <td>NL</td>
      <td>STEPHENVILLE</td>
      <td>8403801</td>
      <td>1895</td>
      <td>6</td>
      <td>2017</td>
      <td>12</td>
      <td>48.53</td>
      <td>-58.55</td>
      <td>26</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>337</th>
      <td>NL</td>
      <td>WABUSH LAKE</td>
      <td>8504177</td>
      <td>1960</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>52.93</td>
      <td>-66.87</td>
      <td>551</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



Before exploring a Dataframe, you can modify the index to make it easier to analyze the dataset. For this, we use the <b> .set_index () </b> function. We must create a new object.


```python
dataframe_Prov_index = dataframe.set_index("Prov")
```


```python
dataframe_Prov_index.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



We can directly select a column from a Dataframe: 


```python
dataframe_Prov_index['Nom de station'].head()
```


    Prov
    BC        AGASSIZ
    BC          ATLIN
    BC    BARKERVILLE
    BC     BEAVERDELL
    BC    BELLA COOLA
    Name: Nom de station, dtype: object



Pandas supports Multi-axes indexing to get the subset of pandas object.
Then, to access an element in a dataframe, there are two methods:

   - the <b> iloc () </b> method to access data from index numbers
   
   - the <b> loc () </b> method to access data from labels
   
   #### a- <b> iloc () </b> method:
   
We can access data from Dataframe using index integer. Like numpy, this method is 0-based indexing. 


```python
# Example1: select specific row and specific column
dataframe_Prov_index.iloc[0,0]
```




    'AGASSIZ'




```python
# Example2: iloc: # select first 4 rows f and all columns
dataframe_Prov_index.iloc[0:4,:]
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example3: iloc: # select all rows and 4 specific columns 
dataframe_Prov_index.iloc[:,0:4].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example4: iloc:# Slicing through list of values
print(dataframe_Prov_index.iloc[[1, 3, 5], [1, 3]])
print(dataframe_Prov_index.iloc[1:3, :])
dataframe_Prov_index.iloc[:,1:3].head()
```

            stnid  mois déb.
    Prov                    
    BC    1200560          8
    BC    1130771          1
    BC    1021480          7
         Nom de station    stnid  année déb.  mois déb.  année fin.  mois fin.  \
    Prov                                                                         
    BC            ATLIN  1200560        1905          8        2017         12   
    BC      BARKERVILLE  1090660        1888          2        2015          3   
    
          lat (deg)  long (deg)  élév (m) stns jointes  
    Prov                                                
    BC        59.57     -133.70       674            N  
    BC        53.07     -121.52      1265            N  
    




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
      <th>stnid</th>
      <th>année déb.</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>1100120</td>
      <td>1893</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>1200560</td>
      <td>1905</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>1090660</td>
      <td>1888</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>1130771</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>1060841</td>
      <td>1895</td>
    </tr>
  </tbody>
</table>
</div>



   #### b- La méthode loc():
   
This method has purely label based indexing.
   
.loc() has multiple access methods like −

        -single scalar label
        
        -list of labels
        
        -slice object
        
        -Boolean array

.loc takes two single/list/range operator separated by ','. The first one indicates the row and the second one indicates columns.
   


```python
# Example1: loc: select all rows for a specific column
dataframe_Prov_index.loc[:,"Nom de station"].head()
```




    Prov
    BC        AGASSIZ
    BC          ATLIN
    BC    BARKERVILLE
    BC     BEAVERDELL
    BC    BELLA COOLA
    Name: Nom de station, dtype: object




```python
# Example2: loc: select all rows for a specific index name
dataframe_Prov_index.loc["QC",:].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>QC</th>
      <td>AMOS</td>
      <td>709CEE9</td>
      <td>1913</td>
      <td>6</td>
      <td>2017</td>
      <td>8</td>
      <td>48.57</td>
      <td>-78.13</td>
      <td>305</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BAGOTVILLE</td>
      <td>7060400</td>
      <td>1880</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>48.33</td>
      <td>-71.00</td>
      <td>159</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BAIE COMEAU</td>
      <td>704S001</td>
      <td>1965</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.13</td>
      <td>-68.20</td>
      <td>130</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BEAUCEVILLE</td>
      <td>7027283</td>
      <td>1913</td>
      <td>8</td>
      <td>2017</td>
      <td>8</td>
      <td>46.15</td>
      <td>-70.70</td>
      <td>168</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BELLETERRE</td>
      <td>7080600</td>
      <td>1951</td>
      <td>9</td>
      <td>2004</td>
      <td>4</td>
      <td>47.38</td>
      <td>-78.70</td>
      <td>322</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example3: Select all rows for multiple columns, say list[]

dataframe_Prov_index.loc[:,["Nom de station", "année déb.", "année fin."]].head()
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
      <th>Nom de station</th>
      <th>année déb.</th>
      <th>année fin.</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1893</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1905</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1888</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1939</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1895</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example4: Select few rows for multiple columns, say list[]
dataframe_Prov_index.loc[['BC','QC'],["Nom de station", "année déb.", "année fin."]].head()
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
      <th>Nom de station</th>
      <th>année déb.</th>
      <th>année fin.</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1893</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1905</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1888</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1939</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1895</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example 5: # for getting values with a boolean array

(dataframe_Prov_index.loc['BC',["année déb."]]>1900).head()
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
      <th>année déb.</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>False</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>True</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>False</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>True</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example 6: # for getting values with a boolean array
dataframe_Prov_index.loc[dataframe_Prov_index["année fin."]>2015,:].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BLUE RIVER</td>
      <td>1160899</td>
      <td>1946</td>
      <td>9</td>
      <td>2017</td>
      <td>12</td>
      <td>52.13</td>
      <td>-119.28</td>
      <td>683</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Example 7: # for getting values with a boolean array
df2 = dataframe_Prov_index.loc["QC",:]
df2.loc[df2["année fin."]==2017,:].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>QC</th>
      <td>AMOS</td>
      <td>709CEE9</td>
      <td>1913</td>
      <td>6</td>
      <td>2017</td>
      <td>8</td>
      <td>48.57</td>
      <td>-78.13</td>
      <td>305</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BAGOTVILLE</td>
      <td>7060400</td>
      <td>1880</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>48.33</td>
      <td>-71.00</td>
      <td>159</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BAIE COMEAU</td>
      <td>704S001</td>
      <td>1965</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.13</td>
      <td>-68.20</td>
      <td>130</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>BEAUCEVILLE</td>
      <td>7027283</td>
      <td>1913</td>
      <td>8</td>
      <td>2017</td>
      <td>8</td>
      <td>46.15</td>
      <td>-70.70</td>
      <td>168</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>CAUSAPSCAL</td>
      <td>7051200</td>
      <td>1913</td>
      <td>11</td>
      <td>2017</td>
      <td>8</td>
      <td>48.37</td>
      <td>-67.23</td>
      <td>168</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



### 7.2.3  Change a Dataframe

   ### 7.2.3.1 Column Selection/Addition/Deletion-
 
We will use here our previous Dataframe.


```python
dataframe_Prov_index.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



#### a- Create a new variable

We can select columns from our Dataframe to create a new one. In this example, we will calculate the number of recording years for each station.  


```python
delta_year = (dataframe_Prov_index["année fin."] - dataframe_Prov_index["année déb."]) + 1
```


```python
delta_year.head()
```




    Prov
    BC    125
    BC    113
    BC    128
    BC     68
    BC    123
    dtype: int64



  #### b- Column Addition in  a DataFrame


```python
dataframe_Prov_index["total année"] = delta_year
```


```python
dataframe_Prov_index.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>total année</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
      <td>125</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
      <td>113</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
      <td>128</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
      <td>68</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
      <td>123</td>
    </tr>
  </tbody>
</table>
</div>



   #### c- Column Deletion in a DataFrame
   
Columns from a Dataframe can be deleted or popped; let us take an example to understand how.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
```


```python
# using del function
print ("Deleting 'stns jointes' column using DEL function:")
del dataframe['stns jointes']
dataframe.head()
```

    Deleting 'stns jointes' column using DEL function:
    




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
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BC</td>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
    </tr>
  </tbody>
</table>
</div>




```python
# using pop function
print ("Deleting 'stnid' column using POP function:")
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.pop('stnid')
dataframe.head()
```

    Deleting 'stnid' column using POP function:
    




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
      <th>Prov</th>
      <th>Nom de station</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BC</td>
      <td>BELLA COOLA</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
# using drop method
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.drop(["stns jointes"], axis=1).head()
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
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BC</td>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
    </tr>
  </tbody>
</table>
</div>



   ### 7.2.3.2  Row Selection/Addition/Deletion-
   
We will now understand row selection, addition and deletion through examples. Let us begin with the concept of selection.

 #### a-  Row Selection
 
Selection by Label
Rows can be selected by passing row label to a loc function.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataframe.loc['BC'].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



Rows can be selected by passing a boolean.


```python
dataframe.loc['BC'].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



Rows can be selected by passing integer location to an iloc function.


```python
dataframe.iloc[0]
```




    Nom de station    AGASSIZ
    stnid             1100120
    année déb.           1893
    mois déb.               1
    année fin.           2017
    mois fin.              12
    lat (deg)           49.25
    long (deg)        -121.77
    élév (m)               15
    stns jointes            N
    Name: BC, dtype: object



Multiple rows can be selected using ‘ : ’ operator.


```python
dataframe[2:4]
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>



#### b-  Row Addition

Add new rows to a DataFrame using function <b>append()</b> function. This function will append the rows at the end.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
```


```python
df_new = pd.DataFrame({'Nom de station': ['station1', 'station2'], 'stnid': [8888, 9999], 'Prov': ['BC', 'QC']}).set_index("Prov")
df_new
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
      <th>Nom de station</th>
      <th>stnid</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>station1</td>
      <td>8888</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>station2</td>
      <td>9999</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataframe = dataframe.append(df_new)
dataframe.tail()
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
      <th>Nom de station</th>
      <th>année déb.</th>
      <th>année fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>mois déb.</th>
      <th>mois fin.</th>
      <th>stnid</th>
      <th>stns jointes</th>
      <th>élév (m)</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NL</th>
      <td>ST JOHN'S</td>
      <td>1874.0</td>
      <td>2017.0</td>
      <td>47.62</td>
      <td>-52.75</td>
      <td>1.0</td>
      <td>12.0</td>
      <td>8403505</td>
      <td>Y</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>NL</th>
      <td>STEPHENVILLE</td>
      <td>1895.0</td>
      <td>2017.0</td>
      <td>48.53</td>
      <td>-58.55</td>
      <td>6.0</td>
      <td>12.0</td>
      <td>8403801</td>
      <td>Y</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>NL</th>
      <td>WABUSH LAKE</td>
      <td>1960.0</td>
      <td>2017.0</td>
      <td>52.93</td>
      <td>-66.87</td>
      <td>11.0</td>
      <td>12.0</td>
      <td>8504177</td>
      <td>Y</td>
      <td>551.0</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>station1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8888</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>station2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9999</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### c-  Row Deletion

Use index label to delete or drop rows from a DataFrame. If label is duplicated, then multiple rows will be dropped.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.head()

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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BC</th>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>BELLA COOLA</td>
      <td>1060841</td>
      <td>1895</td>
      <td>5</td>
      <td>2017</td>
      <td>11</td>
      <td>52.37</td>
      <td>-126.68</td>
      <td>18</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop rows with label 'BC'
dataframe = dataframe.drop('BC')
dataframe.head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>YT</th>
      <td>BURWASH</td>
      <td>2100181</td>
      <td>1966</td>
      <td>10</td>
      <td>2017</td>
      <td>12</td>
      <td>61.37</td>
      <td>-139.05</td>
      <td>807</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>YT</th>
      <td>DAWSON</td>
      <td>2100LRP</td>
      <td>1901</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>64.05</td>
      <td>-139.13</td>
      <td>370</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>N   YT</th>
      <td>HAINES JUNCTIO</td>
      <td>2100630</td>
      <td>1944</td>
      <td>10</td>
      <td>2017</td>
      <td>12</td>
      <td>60.75</td>
      <td>-137.50</td>
      <td>596</td>
      <td>N</td>
    </tr>
    <tr>
      <th>YT</th>
      <td>KOMAKUK BEACH</td>
      <td>2100682</td>
      <td>1958</td>
      <td>7</td>
      <td>2017</td>
      <td>12</td>
      <td>69.62</td>
      <td>-140.20</td>
      <td>13</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>YT</th>
      <td>MAYO</td>
      <td>2100701</td>
      <td>1924</td>
      <td>10</td>
      <td>2017</td>
      <td>12</td>
      <td>63.62</td>
      <td>-135.87</td>
      <td>504</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.loc['ON'].head()
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
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ON</th>
      <td>ATIKOKAN</td>
      <td>6020LPQ</td>
      <td>1917</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>48.80</td>
      <td>-91.58</td>
      <td>442</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>ON</th>
      <td>BEATRICE</td>
      <td>6110607</td>
      <td>1878</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>45.13</td>
      <td>-79.40</td>
      <td>297</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>ON</th>
      <td>BELLEVILLE</td>
      <td>6150689</td>
      <td>1921</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>44.15</td>
      <td>-77.40</td>
      <td>76</td>
      <td>N</td>
    </tr>
    <tr>
      <th>ON</th>
      <td>BIG TROUT LAKE</td>
      <td>6010735</td>
      <td>1939</td>
      <td>2</td>
      <td>2017</td>
      <td>12</td>
      <td>53.83</td>
      <td>-89.87</td>
      <td>224</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>ON</th>
      <td>BROCKVILLE</td>
      <td>6100971</td>
      <td>1915</td>
      <td>7</td>
      <td>2017</td>
      <td>12</td>
      <td>44.60</td>
      <td>-75.67</td>
      <td>96</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

###  7.2.3.3 Merging/Joining Dataframe-

Pandas has full-featured, high performance in-memory join operations idiomatically very similar to relational databases like SQL.

```python
pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,left_index=False, right_index=False, sort=True)
```
 
|  |  |
|--|--|
| <b>left</b> | DataFrame object |
| <b>right</b> | Another DataFrame object |
| <b>on</b> | Columns (names) to join on. Must be found in both the left and right DataFrame objects |
| <b>left_on</b> |Columns from the left DataFrame to use as keys. Can either be column names or arrays with length equal to the length of the DataFrame |
| <b>right_on</b> |Columns from the right DataFrame to use as keys. Can either be column names or arrays with length equal to the length of the DataFrame |
| <b>left_index</b> |If True, use the index (row labels) from the left DataFrame as its join key(s). In case of a DataFrame with a MultiIndex (hierarchical), the number of levels must match the number of join keys from the right DataFrame |
| <b>right_index</b> |Same usage as left_index for the right DataFrame |
| <b>how</b> |One of 'left', 'right', 'outer', 'inner'. Defaults to inner. Each method has been described below |
| <b>sort</b> |Sort the result DataFrame by the join keys in lexicographical order. Defaults to True, setting to False will improve the performance substantially in many cases |

Let us now create two different DataFrames and perform the merging operations on it.


```python
left_dataframe = pd.DataFrame({
   'id':[1,2,3,4],
   'Nom de station': ['MONTREAL TAVISH', 'QUEBEC', 'TADOUSSAC','OKA'],
   'variable':['var1','var2','var6','var5']})

right_dataframe = pd.DataFrame(
   {'id':[1,2,3,4],
   'Nom de station': ['TORONTO', 'OTTAWA', 'KINGSTON','CHAPLEAU'],
   'variable':['var3','var1','var6','var5']})
left_dataframe
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>




```python
right_dataframe
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



#### a-  Merge Two DataFrames on a Key


```python
pd.merge(left_dataframe,right_dataframe,on='id')
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
      <th>id</th>
      <th>Nom de station_x</th>
      <th>variable_x</th>
      <th>Nom de station_y</th>
      <th>variable_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



#### b-  Merge Two DataFrames on a Key


```python
pd.merge(left_dataframe,right_dataframe,on=['id','variable'])
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
      <th>id</th>
      <th>Nom de station_x</th>
      <th>variable</th>
      <th>Nom de station_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
      <td>KINGSTON</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
      <td>CHAPLEAU</td>
    </tr>
  </tbody>
</table>
</div>



#### c-  Merge Two DataFrames Using 'How' argument

The how argument to merge specifies how to determine which keys are to be included in the resulting table. If a key combination does not appear in either the left or the right tables, the values in the joined table will be NA.



```python
# Left Join
pd.merge(left_dataframe, right_dataframe, on='variable', how='left')
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
      <th>id_x</th>
      <th>Nom de station_x</th>
      <th>variable</th>
      <th>id_y</th>
      <th>Nom de station_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
      <td>2.0</td>
      <td>OTTAWA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
      <td>3.0</td>
      <td>KINGSTON</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
      <td>4.0</td>
      <td>CHAPLEAU</td>
    </tr>
  </tbody>
</table>
</div>

### 7.2.3.4  Dataframe Concatenation-

Pandas provides various facilities for easily combining together DataFrame objects.

    pd.concat(objs,axis=0,join='outer',join_axes=None,ignore_index=False)
    
|  |  |
|--|--|
| <b>objs</b> | This is a sequence or mapping of Series, DataFrame objects |
| <b>axis</b> |  {0, 1, ...}, default 0. This is the axis to concatenate along |
| <b>join</b> |  {‘inner’, ‘outer’}, default ‘outer’. How to handle indexes on other axis(es). Outer for union and inner for intersection |
| <b>ignore_index</b> |boolean, default False. If True, do not use the index values on the concatenation axis. The resulting axis will be labeled 0, ..., n - 1 |
| <b>join_axes</b> |This is the list of Index objects. Specific indexes to use for the other (n-1) axes instead of performing inner/outer set logic |

```python
dataframe1 = pd.DataFrame({
   'id':[1,2,3,4],
   'Nom de station': ['MONTREAL TAVISH', 'QUEBEC', 'TADOUSSAC','OKA'],
   'variable':['var1','var2','var6','var5']})

dataframe2 = pd.DataFrame(
   {'id':[1,2,3,4],
   'Nom de station': ['TORONTO', 'OTTAWA', 'KINGSTON','CHAPLEAU'],
   'variable':['var3','var1','var6','var5']})

pd.concat([dataframe1,dataframe2])
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



Suppose we wanted to associate specific keys with each of the pieces of the chopped up DataFrame. We can do this by using the keys argument −


```python
pd.concat([dataframe1,dataframe2],keys=['QC','ON'])
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
      <th></th>
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">QC</th>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">ON</th>
      <th>0</th>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



If we don't want the index being duplicated, set ignore_index to True.


```python
pd.concat([dataframe1,dataframe2],keys=['QC','ON'],ignore_index=True)
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



If the two Dataframes need to be added along axis=1, then the new columns will be appended.


```python
pd.concat([dataframe1,dataframe2],axis=1)
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



####  Concatenating Using append

A useful shortcut to concat are the append instance methods on DataFrame. They concatenate along axis=0, namely the index 


```python
dataframe1.append(dataframe2)
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
      <th>id</th>
      <th>Nom de station</th>
      <th>variable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>MONTREAL TAVISH</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>QUEBEC</td>
      <td>var2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TADOUSSAC</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>OKA</td>
      <td>var5</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>TORONTO</td>
      <td>var3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>OTTAWA</td>
      <td>var1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>KINGSTON</td>
      <td>var6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>CHAPLEAU</td>
      <td>var5</td>
    </tr>
  </tbody>
</table>
</div>



### 7.2.4  Basic Functionality on DataFrame

There are many built-in functions and methods:

https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.html


We will present some useful functions with exploring a dataset.


```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
dataframe.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
      <td>5.630427</td>
      <td>18.903333</td>
      <td>-3.460520</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
      <td>12.628017</td>
      <td>23.641667</td>
      <td>4.017479</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>N</td>
      <td>12.155616</td>
      <td>20.200667</td>
      <td>6.776893</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
  </tbody>
</table>
</div>



- <b>.shape</b> method: 

Returns a tuple representing the dimensionality of the DataFrame. Tuple (a,b), where a represents the number of rows and b represents the number of columns.


```python
dataframe.shape 
```




    (289, 17)



- <b>.columns</b> method:

Returns names of the columns in our Dataframe.


```python
dataframe.columns
```




    Index(['Unnamed: 0', 'Prov', 'Nom de station', 'stnid', 'année déb.',
           'mois déb.', 'année fin.', 'mois fin.', 'lat (deg)', 'long (deg)',
           'élév (m)', 'stns jointes', 'Tmax', 'Tmax90p', 'Tmin', 'Tmin10p',
           'DG0'],
          dtype='object')



- <b>.empty</b> method:

Returns the Boolean value saying whether the Object is empty or not; True indicates that the object is empty.


```python
dataframe.empty
```




    False



   - <b>.isnull</b> method: 
   
To detect missing values easier (and across different array dtypes), Pandas provides the isnull() and notnull() functions.




```python
dataframe['Tmax'].isnull().head()
```




    0     True
    1    False
    2     True
    3    False
    4    False
    Name: Tmax, dtype: bool



We combine this method with .sum() to know the number of missing values.


```python
dataframe['Tmax'].isnull().sum() 
```




    117



   - <b>.dropna</b> method: 
   
If you want to exclude the missing values, then use the dropna function along with the axis argument. By default, axis=0, i.e., along row, which means that if any value within a row is NA then the whole row is excluded.   


```python
dataframe_sans_NaN = dataframe.dropna() 
```


```python
dataframe_sans_NaN['Tmax'].isnull().sum() 
```




    0




```python
dataframe_sans_NaN.shape # nouvelle dimension de notre tableau 
```




    (169, 17)



 - <b>sort_values</b> method:
 
sort_values() is the method for sorting by values. It accepts a 'by' argument which will use the column name of the DataFrame with which the values are to be sorted.



```python
dataframe.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
      <td>5.630427</td>
      <td>18.903333</td>
      <td>-3.460520</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
      <td>12.628017</td>
      <td>23.641667</td>
      <td>4.017479</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>N</td>
      <td>12.155616</td>
      <td>20.200667</td>
      <td>6.776893</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_label_sorted = dataframe.sort_values(by="Prov")
df_label_sorted.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>127</th>
      <td>127</td>
      <td>AB</td>
      <td>SLAVE LAKE</td>
      <td>3065995</td>
      <td>1922</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>55.30</td>
      <td>-114.78</td>
      <td>583</td>
      <td>Y</td>
      <td>7.481366</td>
      <td>22.464333</td>
      <td>-3.422267</td>
      <td>-20.380333</td>
      <td>1131.030000</td>
    </tr>
    <tr>
      <th>106</th>
      <td>106</td>
      <td>AB</td>
      <td>EDMONTON</td>
      <td>3012216</td>
      <td>1880</td>
      <td>7</td>
      <td>2017</td>
      <td>12</td>
      <td>53.57</td>
      <td>-113.52</td>
      <td>723</td>
      <td>Y</td>
      <td>8.982117</td>
      <td>24.328000</td>
      <td>-3.117089</td>
      <td>-19.190667</td>
      <td>1095.933333</td>
    </tr>
    <tr>
      <th>104</th>
      <td>104</td>
      <td>AB</td>
      <td>COLD LAKE</td>
      <td>3081680</td>
      <td>1925</td>
      <td>7</td>
      <td>2017</td>
      <td>12</td>
      <td>54.42</td>
      <td>-110.28</td>
      <td>541</td>
      <td>Y</td>
      <td>7.724485</td>
      <td>24.273667</td>
      <td>-3.037595</td>
      <td>-21.203667</td>
      <td>1303.950000</td>
    </tr>
    <tr>
      <th>103</th>
      <td>103</td>
      <td>AB</td>
      <td>CARWAY</td>
      <td>3031402</td>
      <td>1914</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>49.00</td>
      <td>-113.37</td>
      <td>1354</td>
      <td>Y</td>
      <td>11.139694</td>
      <td>24.925000</td>
      <td>-1.618858</td>
      <td>-13.980000</td>
      <td>956.836667</td>
    </tr>
    <tr>
      <th>102</th>
      <td>102</td>
      <td>AB</td>
      <td>CAMROSE</td>
      <td>3011240</td>
      <td>1946</td>
      <td>3</td>
      <td>2017</td>
      <td>12</td>
      <td>53.03</td>
      <td>-112.82</td>
      <td>739</td>
      <td>N</td>
      <td>8.964966</td>
      <td>24.175667</td>
      <td>-3.714421</td>
      <td>-20.588000</td>
      <td>1048.130000</td>
    </tr>
  </tbody>
</table>
</div>



The argument could takes a list of column values.


```python
df_label_sorted = dataframe.sort_values(by=['Prov','année déb.'])
df_label_sorted.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>106</th>
      <td>106</td>
      <td>AB</td>
      <td>EDMONTON</td>
      <td>3012216</td>
      <td>1880</td>
      <td>7</td>
      <td>2017</td>
      <td>12</td>
      <td>53.57</td>
      <td>-113.52</td>
      <td>723</td>
      <td>Y</td>
      <td>8.982117</td>
      <td>24.328000</td>
      <td>-3.117089</td>
      <td>-19.190667</td>
      <td>1095.933333</td>
    </tr>
    <tr>
      <th>110</th>
      <td>110</td>
      <td>AB</td>
      <td>FORT CHIPEWYAN</td>
      <td>3072655</td>
      <td>1883</td>
      <td>10</td>
      <td>2017</td>
      <td>12</td>
      <td>58.77</td>
      <td>-111.12</td>
      <td>238</td>
      <td>Y</td>
      <td>4.282190</td>
      <td>23.566000</td>
      <td>-6.544206</td>
      <td>-28.629667</td>
      <td>1135.113333</td>
    </tr>
    <tr>
      <th>121</th>
      <td>121</td>
      <td>AB</td>
      <td>MEDICINE HAT</td>
      <td>3034485</td>
      <td>1883</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>50.02</td>
      <td>-110.72</td>
      <td>717</td>
      <td>Y</td>
      <td>12.648926</td>
      <td>28.497333</td>
      <td>-0.155900</td>
      <td>-15.783333</td>
      <td>1563.866667</td>
    </tr>
    <tr>
      <th>99</th>
      <td>99</td>
      <td>AB</td>
      <td>CALGARY</td>
      <td>3031092</td>
      <td>1885</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>51.12</td>
      <td>-114.02</td>
      <td>1084</td>
      <td>Y</td>
      <td>10.834976</td>
      <td>24.467333</td>
      <td>-1.444606</td>
      <td>-15.235000</td>
      <td>1172.050000</td>
    </tr>
    <tr>
      <th>97</th>
      <td>97</td>
      <td>AB</td>
      <td>BANFF</td>
      <td>3050519</td>
      <td>1887</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>51.20</td>
      <td>-115.55</td>
      <td>1397</td>
      <td>Y</td>
      <td>8.906518</td>
      <td>23.132000</td>
      <td>-3.084884</td>
      <td>-15.858333</td>
      <td>750.370000</td>
    </tr>
  </tbody>
</table>
</div>



- <b>sort_index()</b> method:

Using the sort_index() method, by passing the axis arguments and the order of sorting, DataFrame can be sorted. By default, sorting is done on row labels in ascending order.


```python
df_label_sorted.sort_index().head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
      <td>5.630427</td>
      <td>18.903333</td>
      <td>-3.460520</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
      <td>12.628017</td>
      <td>23.641667</td>
      <td>4.017479</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>N</td>
      <td>12.155616</td>
      <td>20.200667</td>
      <td>6.776893</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_label_sorted.sort_index(ascending=False).head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>288</th>
      <td>288</td>
      <td>NL</td>
      <td>WABUSH LAKE</td>
      <td>8504177</td>
      <td>1960</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>52.93</td>
      <td>-66.87</td>
      <td>551</td>
      <td>Y</td>
      <td>2.339743</td>
      <td>19.693667</td>
      <td>-8.024778</td>
      <td>-29.453667</td>
      <td>792.913333</td>
    </tr>
    <tr>
      <th>287</th>
      <td>287</td>
      <td>NL</td>
      <td>STEPHENVILLE</td>
      <td>8403801</td>
      <td>1895</td>
      <td>6</td>
      <td>2017</td>
      <td>12</td>
      <td>48.53</td>
      <td>-58.55</td>
      <td>26</td>
      <td>Y</td>
      <td>8.806534</td>
      <td>20.614000</td>
      <td>1.812748</td>
      <td>-10.582000</td>
      <td>1710.170000</td>
    </tr>
    <tr>
      <th>286</th>
      <td>286</td>
      <td>NL</td>
      <td>ST JOHN'S</td>
      <td>8403505</td>
      <td>1874</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>47.62</td>
      <td>-52.75</td>
      <td>141</td>
      <td>Y</td>
      <td>9.073669</td>
      <td>21.623667</td>
      <td>1.549770</td>
      <td>-8.919000</td>
      <td>1474.820000</td>
    </tr>
    <tr>
      <th>285</th>
      <td>285</td>
      <td>NL</td>
      <td>ST ANTHONY</td>
      <td>8403389</td>
      <td>1946</td>
      <td>6</td>
      <td>2017</td>
      <td>12</td>
      <td>51.37</td>
      <td>-55.60</td>
      <td>33</td>
      <td>Y</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>284</th>
      <td>284</td>
      <td>NL</td>
      <td>PORT AUXBASQUES</td>
      <td>8402975</td>
      <td>1909</td>
      <td>2</td>
      <td>2017</td>
      <td>9</td>
      <td>47.58</td>
      <td>-58.97</td>
      <td>40</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_label_sorted.sort_index(axis=1).head()
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
      <th>DG0</th>
      <th>Nom de station</th>
      <th>Prov</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>Unnamed: 0</th>
      <th>année déb.</th>
      <th>année fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>mois déb.</th>
      <th>mois fin.</th>
      <th>stnid</th>
      <th>stns jointes</th>
      <th>élév (m)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>106</th>
      <td>1095.933333</td>
      <td>EDMONTON</td>
      <td>AB</td>
      <td>8.982117</td>
      <td>24.328000</td>
      <td>-3.117089</td>
      <td>-19.190667</td>
      <td>106</td>
      <td>1880</td>
      <td>2017</td>
      <td>53.57</td>
      <td>-113.52</td>
      <td>7</td>
      <td>12</td>
      <td>3012216</td>
      <td>Y</td>
      <td>723</td>
    </tr>
    <tr>
      <th>110</th>
      <td>1135.113333</td>
      <td>FORT CHIPEWYAN</td>
      <td>AB</td>
      <td>4.282190</td>
      <td>23.566000</td>
      <td>-6.544206</td>
      <td>-28.629667</td>
      <td>110</td>
      <td>1883</td>
      <td>2017</td>
      <td>58.77</td>
      <td>-111.12</td>
      <td>10</td>
      <td>12</td>
      <td>3072655</td>
      <td>Y</td>
      <td>238</td>
    </tr>
    <tr>
      <th>121</th>
      <td>1563.866667</td>
      <td>MEDICINE HAT</td>
      <td>AB</td>
      <td>12.648926</td>
      <td>28.497333</td>
      <td>-0.155900</td>
      <td>-15.783333</td>
      <td>121</td>
      <td>1883</td>
      <td>2017</td>
      <td>50.02</td>
      <td>-110.72</td>
      <td>8</td>
      <td>12</td>
      <td>3034485</td>
      <td>Y</td>
      <td>717</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1172.050000</td>
      <td>CALGARY</td>
      <td>AB</td>
      <td>10.834976</td>
      <td>24.467333</td>
      <td>-1.444606</td>
      <td>-15.235000</td>
      <td>99</td>
      <td>1885</td>
      <td>2017</td>
      <td>51.12</td>
      <td>-114.02</td>
      <td>1</td>
      <td>12</td>
      <td>3031092</td>
      <td>Y</td>
      <td>1084</td>
    </tr>
    <tr>
      <th>97</th>
      <td>750.370000</td>
      <td>BANFF</td>
      <td>AB</td>
      <td>8.906518</td>
      <td>23.132000</td>
      <td>-3.084884</td>
      <td>-15.858333</td>
      <td>97</td>
      <td>1887</td>
      <td>2017</td>
      <td>51.20</td>
      <td>-115.55</td>
      <td>11</td>
      <td>12</td>
      <td>3050519</td>
      <td>Y</td>
      <td>1397</td>
    </tr>
  </tbody>
</table>
</div>



- <b>.describe()</b> method:  

Generates descriptive statistics that summarize the central tendency, dispersion and shape of a dataset’s distribution, excluding NaN values.


```python
dataframe['Tmax'].describe()
```




    count    172.000000
    mean       7.916314
    std        5.524630
    min      -15.366463
    25%        7.364646
    50%        8.988052
    75%       11.018241
    max       16.105511
    Name: Tmax, dtype: float64



- <b>.dtypes()</b> method:  

Returns the dtypes in this object.


```python
dataframe.dtypes
```




    Unnamed: 0          int64
    Prov               object
    Nom de station     object
    stnid              object
    année déb.          int64
    mois déb.           int64
    année fin.          int64
    mois fin.           int64
    lat (deg)         float64
    long (deg)        float64
    élév (m)            int64
    stns jointes       object
    Tmax              float64
    Tmax90p           float64
    Tmin              float64
    Tmin10p           float64
    DG0               float64
    dtype: object



### 7.2.5  DataFrame Function Application

To apply your own or another library’s functions to Pandas objects, you should be aware of the three important methods. The methods have been discussed below. The appropriate method to use depends on whether your function expects to operate on an entire DataFrame, row- or column-wise, or element wise.

- Table wise Function Application: <b>.pipe()</b>

- Row or Column Wise Function Application: <b>.apply()</b>

- Element wise Function Application: <b>.applymap()</b>

- <b>.apply()</b> method: 

Arbitrary functions can be applied along the axes of a DataFrame or Panel using the apply() method, which, like the descriptive statistics methods, takes an optional axis argument. By default, the operation performs column wise, taking each column as an array-like.




```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
```


```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
dataframe["stns jointes"]=dataframe["stns jointes"].apply(lambda x: x.replace("N", "NaN"))
dataframe["stns jointes"]=dataframe["stns jointes"].apply(lambda x: x.replace("Y", "1"))
dataframe = dataframe.dropna() 
dataframe.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>NaN</td>
      <td>5.630427</td>
      <td>18.903333</td>
      <td>-3.460520</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>1</td>
      <td>12.628017</td>
      <td>23.641667</td>
      <td>4.017479</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>NaN</td>
      <td>12.155616</td>
      <td>20.200667</td>
      <td>6.776893</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>BC</td>
      <td>BLUE RIVER</td>
      <td>1160899</td>
      <td>1946</td>
      <td>9</td>
      <td>2017</td>
      <td>12</td>
      <td>52.13</td>
      <td>-119.28</td>
      <td>683</td>
      <td>1</td>
      <td>10.440754</td>
      <td>25.991667</td>
      <td>-1.125014</td>
      <td>-12.582333</td>
      <td>987.363333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>BC</td>
      <td>COMOX</td>
      <td>1021830</td>
      <td>1935</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>49.72</td>
      <td>-124.90</td>
      <td>26</td>
      <td>1</td>
      <td>13.737613</td>
      <td>23.102333</td>
      <td>6.424850</td>
      <td>-0.526000</td>
      <td>2444.393333</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataframe["Tmin"]=dataframe["Tmin"].apply(lambda x: round(x,2))
dataframe["Tmax"]=dataframe["Tmax"].apply(lambda x: int(x))
dataframe.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>NaN</td>
      <td>5</td>
      <td>18.903333</td>
      <td>-3.46</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>1</td>
      <td>12</td>
      <td>23.641667</td>
      <td>4.02</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>NaN</td>
      <td>12</td>
      <td>20.200667</td>
      <td>6.78</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>BC</td>
      <td>BLUE RIVER</td>
      <td>1160899</td>
      <td>1946</td>
      <td>9</td>
      <td>2017</td>
      <td>12</td>
      <td>52.13</td>
      <td>-119.28</td>
      <td>683</td>
      <td>1</td>
      <td>10</td>
      <td>25.991667</td>
      <td>-1.13</td>
      <td>-12.582333</td>
      <td>987.363333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>BC</td>
      <td>COMOX</td>
      <td>1021830</td>
      <td>1935</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>49.72</td>
      <td>-124.90</td>
      <td>26</td>
      <td>1</td>
      <td>13</td>
      <td>23.102333</td>
      <td>6.42</td>
      <td>-0.526000</td>
      <td>2444.393333</td>
    </tr>
  </tbody>
</table>
</div>



### 7.2.6  DataFrame GroupBY method

Any groupby operation involves one of the following operations on the original object. They are −

 - Splitting the Object
 - Applying a function
 - Combining the results

In many situations, we split the data into sets and we apply some functionality on each subset. In the apply functionality, we can perform the following operations −

 - Aggregation − computing a summary statistic
 - Transformation − perform some group-specific operation
 - Filtration − discarding the data with some condition

Let us now create a DataFrame object and perform all the operations on it −

```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
dataframe.head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>BC</td>
      <td>AGASSIZ</td>
      <td>1100120</td>
      <td>1893</td>
      <td>1</td>
      <td>2017</td>
      <td>12</td>
      <td>49.25</td>
      <td>-121.77</td>
      <td>15</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>BC</td>
      <td>ATLIN</td>
      <td>1200560</td>
      <td>1905</td>
      <td>8</td>
      <td>2017</td>
      <td>12</td>
      <td>59.57</td>
      <td>-133.70</td>
      <td>674</td>
      <td>N</td>
      <td>5.630427</td>
      <td>18.903333</td>
      <td>-3.460520</td>
      <td>-19.235000</td>
      <td>860.083333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>BC</td>
      <td>BARKERVILLE</td>
      <td>1090660</td>
      <td>1888</td>
      <td>2</td>
      <td>2015</td>
      <td>3</td>
      <td>53.07</td>
      <td>-121.52</td>
      <td>1265</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>BC</td>
      <td>BEAVERDELL</td>
      <td>1130771</td>
      <td>1939</td>
      <td>1</td>
      <td>2006</td>
      <td>9</td>
      <td>49.48</td>
      <td>-119.05</td>
      <td>838</td>
      <td>Y</td>
      <td>12.628017</td>
      <td>23.641667</td>
      <td>4.017479</td>
      <td>-3.646000</td>
      <td>1798.093333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>BC</td>
      <td>BLIND CHANNEL</td>
      <td>1021480</td>
      <td>1958</td>
      <td>7</td>
      <td>2016</td>
      <td>2</td>
      <td>50.42</td>
      <td>-125.50</td>
      <td>23</td>
      <td>N</td>
      <td>12.155616</td>
      <td>20.200667</td>
      <td>6.776893</td>
      <td>1.094667</td>
      <td>2518.680000</td>
    </tr>
  </tbody>
</table>
</div>



Looking at the DataFrame above, we see that there are at least 3 variables that we can use to group our dataset. For example, we can group our data by province (Prov), by year of beginning of recording or year of end of recording.

We will use the Pandas groupby module to group our data.

- <b>.unique()</b> method : 

Returns the unique values of a column.

```python
dataframe["Prov"].unique() 
```
    array(['BC', 'YT', 'N   YT', 'NT', 'NU', 'AB', 'SK', 'MB', 'ON', 'QC',
           'NB', 'NS', 'PE', 'NL'], dtype=object)



#### Split Data into Groups:


```python
dataframe.groupby('Prov')
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x0000000008D35860>



- To view groups:


```python
dataframe.groupby('Prov').groups
```




    {'AB': Int64Index([ 96,  97,  98,  99, 100, 101, 102, 103, 104, 105, 106, 107, 108,
                 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121,
                 122, 123, 124, 125, 126, 127, 128, 129, 130],
                dtype='int64'),
     'BC': Int64Index([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
                 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
                 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49,
                 50],
                dtype='int64'),
     'MB': Int64Index([156, 157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168,
                 169, 170, 171, 172, 173, 174, 175],
                dtype='int64'),
     'N   YT': Int64Index([52], dtype='int64'),
     'NB': Int64Index([254, 255, 256, 257, 258, 259, 260, 261], dtype='int64'),
     'NL': Int64Index([275, 276, 277, 278, 279, 280, 281, 282, 283, 284, 285, 286, 287,
                 288],
                dtype='int64'),
     'NS': Int64Index([262, 263, 264, 265, 266, 267, 268, 269, 270, 271, 272, 273], dtype='int64'),
     'NT': Int64Index([61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73], dtype='int64'),
     'NU': Int64Index([74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90,
                 91, 92, 93, 94, 95],
                dtype='int64'),
     'ON': Int64Index([176, 177, 178, 179, 180, 181, 182, 183, 184, 185, 186, 187, 188,
                 189, 190, 191, 192, 193, 194, 195, 196, 197, 198, 199, 200, 201,
                 202, 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214,
                 215],
                dtype='int64'),
     'PE': Int64Index([274], dtype='int64'),
     'QC': Int64Index([216, 217, 218, 219, 220, 221, 222, 223, 224, 225, 226, 227, 228,
                 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241,
                 242, 243, 244, 245, 246, 247, 248, 249, 250, 251, 252, 253],
                dtype='int64'),
     'SK': Int64Index([131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143,
                 144, 145, 146, 147, 148, 149, 150, 151, 152, 153, 154, 155],
                dtype='int64'),
     'YT': Int64Index([51, 53, 54, 55, 56, 57, 58, 59, 60], dtype='int64')}



- Group by with multiple columns:

```python
dataframe.groupby(['Prov','année fin.']).groups
```

    {('AB', 2011): Int64Index([116], dtype='int64'),
     ('AB', 2013): Int64Index([101], dtype='int64'),
     ('AB', 2016): Int64Index([100, 130], dtype='int64'),
     ('AB',
      2017): Int64Index([ 96,  97,  98,  99, 102, 103, 104, 105, 106, 107, 108, 109, 110,
                 111, 112, 113, 114, 115, 117, 118, 119, 120, 121, 122, 123, 124,
                 125, 126, 127, 128, 129],
                dtype='int64'),
     ('BC', 2006): Int64Index([3], dtype='int64'),
     ('BC', 2013): Int64Index([20], dtype='int64'),
     ('BC', 2014): Int64Index([21, 25], dtype='int64'),
     ('BC', 2015): Int64Index([2, 8, 11, 16], dtype='int64'),
     ('BC', 2016): Int64Index([4, 6, 41], dtype='int64'),
     ('BC',
      2017): Int64Index([ 0,  1,  5,  7,  9, 10, 12, 13, 14, 15, 17, 18, 19, 22, 23, 24, 26,
                 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 42, 43, 44,
                 45, 46, 47, 48, 49, 50],
                dtype='int64'),
     ('MB', 2016): Int64Index([156], dtype='int64'),
     ('MB',
      2017): Int64Index([157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168, 169,
                 170, 171, 172, 173, 174, 175],
                dtype='int64'),
     ('N   YT', 2017): Int64Index([52], dtype='int64'),
     ('NB',
      2017): Int64Index([254, 255, 256, 257, 258, 259, 260, 261], dtype='int64'),
     ('NL', 2011): Int64Index([282], dtype='int64'),
     ('NL', 2015): Int64Index([276], dtype='int64')}


### Iterating through Groups:


```python
grouped = dataframe.groupby('Prov')

for name,group in grouped:
   print(name)
   print(group)
```

    AB
         Unnamed: 0 Prov   Nom de station    stnid  année déb.  mois déb.  \
    96           96   AB        ATHABASCA  3060L20        1918          6   
    97           97   AB            BANFF  3050519        1887         11   
    98           98   AB      BEAVERLODGE  3070600        1913          4   
    99           99   AB          CALGARY  3031092        1885          1   
     
    
         année fin.  mois fin.  lat (deg)  long (deg)  élév (m) stns jointes  \
    96         2017         12      54.82     -113.53       626            Y   
    97         2017         12      51.20     -115.55      1397            Y   
    98         2017         12      55.20     -119.40       745            Y   
    99         2017         12      51.12     -114.02      1084            Y   
    
 
 
#### Select a group:

- <b>.get_group()</b> method:

We can select a single group.


```python
grouped.get_group('QC').head()
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>216</th>
      <td>216</td>
      <td>QC</td>
      <td>AMOS</td>
      <td>709CEE9</td>
      <td>1913</td>
      <td>6</td>
      <td>2017</td>
      <td>8</td>
      <td>48.57</td>
      <td>-78.13</td>
      <td>305</td>
      <td>Y</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>217</th>
      <td>217</td>
      <td>QC</td>
      <td>BAGOTVILLE</td>
      <td>7060400</td>
      <td>1880</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>48.33</td>
      <td>-71.00</td>
      <td>159</td>
      <td>Y</td>
      <td>8.281390</td>
      <td>25.297333</td>
      <td>-1.833594</td>
      <td>-20.811667</td>
      <td>1528.413333</td>
    </tr>
    <tr>
      <th>218</th>
      <td>218</td>
      <td>QC</td>
      <td>BEAUCEVILLE</td>
      <td>7027283</td>
      <td>1913</td>
      <td>8</td>
      <td>2017</td>
      <td>8</td>
      <td>46.15</td>
      <td>-70.70</td>
      <td>168</td>
      <td>Y</td>
      <td>10.551494</td>
      <td>26.078333</td>
      <td>-1.376339</td>
      <td>-19.628333</td>
      <td>1509.360000</td>
    </tr>
    <tr>
      <th>219</th>
      <td>219</td>
      <td>QC</td>
      <td>BROME</td>
      <td>7020840</td>
      <td>1890</td>
      <td>9</td>
      <td>2014</td>
      <td>7</td>
      <td>45.18</td>
      <td>-72.57</td>
      <td>206</td>
      <td>N</td>
      <td>11.140937</td>
      <td>26.176667</td>
      <td>-0.294151</td>
      <td>-17.560000</td>
      <td>1676.226667</td>
    </tr>
    <tr>
      <th>220</th>
      <td>220</td>
      <td>QC</td>
      <td>CAUSAPSCAL</td>
      <td>7051200</td>
      <td>1913</td>
      <td>11</td>
      <td>2017</td>
      <td>8</td>
      <td>48.37</td>
      <td>-67.23</td>
      <td>168</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### Aggregations

An aggregated function returns a single aggregated value for each group. Once the group by object is created, several aggregation operations can be performed on the grouped data.

An obvious one is aggregation via the aggregate or equivalent agg method −


```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
grouped = dataframe.groupby('Prov')
```


```python
grouped['Tmin'].agg(np.mean)
```




    Prov
    AB        -3.050928
    BC         1.578024
    MB        -4.493900
    N   YT          NaN
    NB         0.341750
    NL        -1.324334
    NS         2.542629
    NT        -8.518655
    NU       -16.522658
    ON         0.031970
    PE         1.986827
    QC        -1.992695
    SK        -3.208984
    YT        -8.995421
    Name: Tmin, dtype: float64



#### Applying Multiple Aggregation Functions at Once
With grouped Series, you can also pass a list or dict of functions to do aggregation with, and generate DataFrame as output −


```python
grouped['Tmin'].agg([np.min, np.mean, np.max, np.std])
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
      <th>amin</th>
      <th>mean</th>
      <th>amax</th>
      <th>std</th>
    </tr>
    <tr>
      <th>Prov</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AB</th>
      <td>-6.544206</td>
      <td>-3.050928</td>
      <td>-0.155900</td>
      <td>1.401326</td>
    </tr>
    <tr>
      <th>BC</th>
      <td>-6.068580</td>
      <td>1.578024</td>
      <td>7.016292</td>
      <td>3.896384</td>
    </tr>
    <tr>
      <th>MB</th>
      <td>-10.094295</td>
      <td>-4.493900</td>
      <td>-1.980265</td>
      <td>2.618348</td>
    </tr>
    <tr>
      <th>N   YT</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NB</th>
      <td>-0.491043</td>
      <td>0.341750</td>
      <td>0.840796</td>
      <td>0.598429</td>
    </tr>
    <tr>
      <th>NL</th>
      <td>-8.024778</td>
      <td>-1.324334</td>
      <td>1.812748</td>
      <td>3.425846</td>
    </tr>
    <tr>
      <th>NS</th>
      <td>1.214131</td>
      <td>2.542629</td>
      <td>3.759460</td>
      <td>0.982653</td>
    </tr>
    <tr>
      <th>NT</th>
      <td>-12.451845</td>
      <td>-8.518655</td>
      <td>-6.683226</td>
      <td>2.169370</td>
    </tr>
    <tr>
      <th>NU</th>
      <td>-21.935075</td>
      <td>-16.522658</td>
      <td>-12.233232</td>
      <td>3.049096</td>
    </tr>
    <tr>
      <th>ON</th>
      <td>-7.484845</td>
      <td>0.031970</td>
      <td>5.918716</td>
      <td>3.647877</td>
    </tr>
    <tr>
      <th>PE</th>
      <td>1.986827</td>
      <td>1.986827</td>
      <td>1.986827</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>QC</th>
      <td>-8.768054</td>
      <td>-1.992695</td>
      <td>1.622124</td>
      <td>2.706681</td>
    </tr>
    <tr>
      <th>SK</th>
      <td>-5.016558</td>
      <td>-3.208984</td>
      <td>-1.428850</td>
      <td>1.030549</td>
    </tr>
    <tr>
      <th>YT</th>
      <td>-10.217714</td>
      <td>-8.995421</td>
      <td>-7.773129</td>
      <td>1.728582</td>
    </tr>
  </tbody>
</table>
</div>



#### Transformations

Transformation on a group or a column returns an object that is indexed the same size of that is being grouped. Thus, the transform should return a result that is the same size as that of a group chunk.


```python
grouped = dataframe.groupby('Prov')
and_stand = lambda x: (x - x.mean()) / x.std()
grouped['Tmin'].transform(and_stand).head()
```




    0         NaN
    1   -1.293133
    2         NaN
    3    0.626082
    4    1.334280
    Name: Tmin, dtype: float64



#### Filtration

Filtration filters the data on a defined criteria and returns the subset of data. The filter() function is used to filter the data.


```python
dataframe.groupby('Prov').filter(lambda x: len(x) == 1)
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
      <th>Unnamed: 0</th>
      <th>Prov</th>
      <th>Nom de station</th>
      <th>stnid</th>
      <th>année déb.</th>
      <th>mois déb.</th>
      <th>année fin.</th>
      <th>mois fin.</th>
      <th>lat (deg)</th>
      <th>long (deg)</th>
      <th>élév (m)</th>
      <th>stns jointes</th>
      <th>Tmax</th>
      <th>Tmax90p</th>
      <th>Tmin</th>
      <th>Tmin10p</th>
      <th>DG0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>52</th>
      <td>52</td>
      <td>N   YT</td>
      <td>HAINES JUNCTIO</td>
      <td>2100630</td>
      <td>1944</td>
      <td>10</td>
      <td>2017</td>
      <td>12</td>
      <td>60.75</td>
      <td>-137.50</td>
      <td>596</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>274</th>
      <td>274</td>
      <td>PE</td>
      <td>CHARLOTTETOWN</td>
      <td>8300301</td>
      <td>1872</td>
      <td>11</td>
      <td>2017</td>
      <td>12</td>
      <td>46.28</td>
      <td>-63.13</td>
      <td>49</td>
      <td>Y</td>
      <td>10.00633</td>
      <td>23.768333</td>
      <td>1.986827</td>
      <td>-12.036667</td>
      <td>1912.156667</td>
    </tr>
  </tbody>
</table>
</div>



In the above filter condition, we are asking to return the Provinces which have only one station.


```python

```

### 7.2.7  Save a DataFrame: 

For writing a DataFrame, use the <b> .to_csv </b> or <b> _table </b> functions with similar options as read_csv () seen previously.


```python
dataframe.to_csv("./DATA/My_new_DataFrame.csv", index = False, header = True, sep = ',')
```

### 7.3 Date Functionality:

Using the <b>date.range()</b> function by specifying the periods and the frequency, we can create the date series. By default, the frequency of range is Days.


```python
pd.date_range('1/1/2011', periods=5)
```




    DatetimeIndex(['2011-01-01', '2011-01-02', '2011-01-03', '2011-01-04',
                   '2011-01-05'],
                  dtype='datetime64[ns]', freq='D')



We can change the date frequency:


```python
pd.date_range('1/1/2011', periods=5,freq='M')
```




    DatetimeIndex(['2011-01-31', '2011-02-28', '2011-03-31', '2011-04-30',
                   '2011-05-31'],
                  dtype='datetime64[ns]', freq='M')



<b>bdate_range()</b> stands for business date ranges. Unlike date_range(), it excludes Saturday and Sunday.


```python
pd.bdate_range('1/1/2011', periods=10)
```




    DatetimeIndex(['2011-01-03', '2011-01-04', '2011-01-05', '2011-01-06',
                   '2011-01-07', '2011-01-10', '2011-01-11', '2011-01-12',
                   '2011-01-13', '2011-01-14'],
                  dtype='datetime64[ns]', freq='B')



Convenience functions like date_range and bdate_range utilize a variety of frequency aliases. The default frequency for date_range is a calendar day while the default for bdate_range is a business day.


```python
start = pd.datetime(2011, 1, 1)
end = pd.datetime(2011, 1, 5)
pd.date_range(start, end)
```




    DatetimeIndex(['2011-01-01', '2011-01-02', '2011-01-03', '2011-01-04',
                   '2011-01-05'],
                  dtype='datetime64[ns]', freq='D')



### 7.4 Format dates with the Datetime module:

Python provides many features to work with dates and time.

Datetime is a module that allows you to manipulate dates and times as objects. The idea is simple: you manipulate the object to do all your calculations, and when you need to display it, you format the object into a string.

https://docs.python.org/2/library/datetime.html

You can artificially create a datetime object with the following parameters:

        datetime (year, month, day, hour, minute, second, microsecond, timezone)

The parameters "year", "month" and "day" are mandatory.

The datetime module provides the following classes:

<table border="1" class="docutils">
<colgroup>
<col width="27%">
<col width="57%">
</colgroup>
<tbody valign="top">
   <tr>
    <th>Classe</th>
    <th>Description</th>
  </tr>
<tr><td><tt class="docutils literal"><span class="pre"><b>datetime.date</b></span></tt></td>
<td>A date instance represents a date</td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre"><b>datetime.datetime</b></span></tt></td>
<td>An instance of datetime represents a date and time according to the Gregorian calendar
</td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre"><b>datetime.time</b></span></tt></td>
<td>An instance of time represents the time, except for the date. </td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre"><b>datetime.timedelta</b></span></tt></td>
<td>The timedelta class is used to keep the differences between two temporal or dated objects.</td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre"><b>datetime.tzinfo</b></span></tt></td>
<td>The tzinfo class is used to implement time zone support for time and datetime objects. </td>
</tr>
</tbody>
</table>



We will see some examples of using DateTime and its classe.


#### 1-  The <b> datetime </b> class of the datetime module

<b>-a Creating a datetime object</b>


```python
from datetime import datetime
datetime(2019, 3, 1)       # instance of datetime
```




    datetime.datetime(2019, 3, 1, 0, 0)




```python
now = datetime.now()
now
```




    datetime.datetime(2019, 10, 24, 14, 8, 0, 512783)




```python
now = now.today()
now
```




    datetime.datetime(2019, 10, 24, 14, 8, 0, 531785)




```python
now = datetime.utcnow()
now
```




    datetime.datetime(2019, 10, 24, 18, 8, 0, 546785)



When opening a csv or text file, we have information about the date and time of the measurements but in the form of strings: "2018-11-01 15:20" or "2017/12/1 16:35:22 "...

It is possible during the reading to convert these strings into a datetime object.


```python
dt = datetime.strptime("2018/11/01 15:20", "%Y/%m/%d %H:%M")
dt
```




    datetime.datetime(2018, 11, 1, 15, 20)




```python
dt = datetime.strptime("2017/12/1 16:35:22", "%Y/%m/%d %H:%M:%S")
dt
```




    datetime.datetime(2017, 12, 1, 16, 35, 22)




```python
dt = datetime.strptime("01/11/19 10-35:22", "%d/%m/%y %H-%M:%S")
dt

```




    datetime.datetime(2019, 11, 1, 10, 35, 22)




```python
dt = datetime.strptime("1Mar 2019 à 09h35", "%d%b %Y à %Hh%M")
dt
```




    datetime.datetime(2019, 3, 1, 9, 35)



<b>b- Manipulate datetime object</b>

From an object or instance of datetime, you can retrieve the time and date.


```python
#now.year
#now.month
#now.day
#maintenant.hour
now.minute
#now.second
#now.microsecond
#now
```




    8



We can change datetime instance:


```python
now.replace(year=1995) 
```




    datetime.datetime(1995, 10, 24, 18, 8, 0, 546785)




```python
now.replace(month=1)
```




    datetime.datetime(2019, 1, 24, 18, 8, 0, 546785)



We can then convert datetime instance to string:


```python
d = datetime.now(); print(d)
d
```

    2019-10-24 14:08:00.720795
    




    datetime.datetime(2019, 10, 24, 14, 8, 0, 720795)




```python
d.strftime("%H:%M"), d.strftime("%Hh%Mmin")
```




    ('14:08', '14h08min')




```python
d.strftime("%Y-%m %H:%M")
```




    '2019-10 14:08'




```python
'The day today is {0:%d} {0:%B} and it s  {0:%Hh%Mmin} '.format(d, "day", "month", "time")
```




    'The day today is 24 October and it s  14h08min '



- <b>date</b> et <b>time</b> class

These two classes can be used to create a datetime instance.


```python
from datetime import datetime, date, time
d = date(2005, 7, 14)
t = time(12, 30)
t
```




    datetime.time(12, 30)




```python
datetime.combine(d, t)
```




    datetime.datetime(2005, 7, 14, 12, 30)




```python
now = datetime.utcnow()
now.date()
now.time()

```




    datetime.time(18, 8, 0, 855803)



- The <b> timedelta </b> class of the datetime module


```python
from datetime import timedelta
delta = timedelta(days=3, seconds=100)    # we create our own timedelta
```


```python
datetime.now()
```




    datetime.datetime(2019, 10, 24, 14, 8, 0, 899806)




```python
datetime.now() + delta
```




    datetime.datetime(2019, 10, 27, 14, 9, 40, 935808)




```python
datetime.now() + timedelta(days=2, hours=4, minutes=3, seconds=12)
```




    datetime.datetime(2019, 10, 26, 18, 11, 12, 966809)




```python
time_range = datetime(2010, 12, 31) - datetime(1981, 12, 31)
time_range
```




    datetime.timedelta(days=10592)



- Example1: Calculate the year of birth from a given age


```python
from datetime import datetime
 
old = 25
month = 10
 
actual_year = datetime.today().year
actual_month = datetime.today().month
 
result = actual_year - old - (1 if month > actual_month else 0)
print(result)
```

    1994
    

- Example2: Calculate the year of birth from a given age


We can  generate dates for time series with an arbitrary time step:


```python
from datetime import timedelta
dt = timedelta(days = 5, hours = 6, minutes = 25)
d0 = datetime(2000, 2, 21)
[str(d0 + i * dt) for i in range(10)]
```




    ['2000-02-21 00:00:00',
     '2000-02-26 06:25:00',
     '2000-03-02 12:50:00',
     '2000-03-07 19:15:00',
     '2000-03-13 01:40:00',
     '2000-03-18 08:05:00',
     '2000-03-23 14:30:00',
     '2000-03-28 20:55:00',
     '2000-04-03 03:20:00',
     '2000-04-08 09:45:00']