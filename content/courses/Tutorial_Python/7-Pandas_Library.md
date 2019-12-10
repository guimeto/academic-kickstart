
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
    weight: 1
---
<img src="/img/pandas.png" alt="Indentation" width="30%" height="30%">
![image0](/img/pandas.png)
  

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
|    |   Amont Max |   Amont Min |   Amont Mean |   Aval Max |   Aval Max |   Aval Mean |   Debit Mean |   Debit Max |   Debit Min |
|---:|------------:|------------:|-------------:|-----------:|-----------:|------------:|-------------:|------------:|------------:|
|  0 |       39.7  |       39.09 |      39.5565 |      23.23 |      22.5  |     22.859  |      2390.53 |     3164.97 |     1673.8  |
|  1 |       41.16 |       40.96 |      41.0881 |      23.22 |      22.43 |     22.7584 |      2227.28 |     3008.18 |     1697.87 |
|  2 |       41.15 |       41.05 |      41.1132 |      23.35 |      22.87 |     23.1555 |      2851.27 |     3231.8  |     2367.85 |
|  3 |       41.09 |       40.61 |      40.9684 |      23.78 |      22.7  |     23.0326 |      2635.04 |     3967.33 |     2069.65 |
|  4 |       41.09 |       39.6  |      40.2697 |      24.24 |      22.87 |     23.6458 |      3924.23 |     5407.32 |     2417.89 |



### - b) Create Dataframe loading csv file: <b>read_table()</b> or <b>read_csv()</b> function

- <b> read_table () </b> and <b> read_csv () </b> are the most useful functions under Pandas for reading text files and generating a DataFrame.

We will work with a dataset from a hydraulic dam.
Our csv file has 9 variables, the first line gives us the names of the variables (or labels).

A csv document can be read with the <b> read_table () </b> function, with the separator attribute ",".


```python
barrage = pd.read_table("./DATA/DATA_EXTREME_Carillon_1963_2017_5.csv", sep=",")
barrage.head()
```
|    |   Amont_max |   Amont_min |   Amont_moyen |   Aval_max |   Aval_min |   Aval_moyen |   Debit_Moyen |   Debit_max |   Debit_min |
|---:|------------:|------------:|--------------:|-----------:|-----------:|-------------:|--------------:|------------:|------------:|
|  0 |       39.7  |       39.09 |       39.5565 |      23.23 |      22.5  |      22.859  |      2390.53  |     3164.97 |     1673.8  |
|  1 |       41.16 |       40.96 |       41.0881 |      23.22 |      22.43 |      22.7584 |      2227.28  |     3008.18 |     1697.87 |
|  2 |       41.15 |       41.05 |       41.1132 |      23.35 |      22.87 |      23.1555 |      2851.27  |     3231.8  |     2367.85 |
|  3 |       41.09 |       40.61 |       40.9684 |      23.78 |      22.7  |      23.0326 |      2635.04  |     3967.33 |     2069.65 |
|  4 |       41.09 |       39.6  |       40.2697 |      24.24 |      22.87 |      23.6458 |      3924.23  |     5407.32 |     2417.89 |

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
|    |   Variable1 |   Variable2 |   Variable3 |
|---:|------------:|------------:|------------:|
|  0 |       39.7  |       39.09 |       23.23 |
|  1 |       41.16 |       40.96 |       23.22 |
|  2 |       41.15 |       41.05 |       23.35 |
|  3 |       41.09 |       40.61 |       23.78 |
|  4 |       41.09 |       39.6  |       24.24 |

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

|       |   Precipitation |
|------:|----------------:|
|     0 |             0   |
|     1 |             0   |
|     2 |             0   |
|     3 |             0   |
|     4 |             0   |
|     5 |             0   |
|     6 |             0   |
|     7 |             0   |
|     8 |             1.3 |


### <b>- d)</b> Create Dataframe loading excell (.xls) file: <b>read_excel()</b> function

We will open here an excel file (.xls extension). This file is a database containing information on all homogenized Environmental and Climate Change Canada temperature stations.

This database has 11 columns with data starting at the 4 th line.


We will define the "Province" column as index of our DataFrame.


```python
df4 = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", index_col=0,skiprows = range(0, 3))
df4.head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |


### 7.2.2  Access data from DataFrames 

The first thing to do when opening a new dataset is print out a few rows. We accomplish this with <b>.head()</b> method:

```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.head()
```
|     | Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|----:|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
|   0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
|   1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
|   2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
|   3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
|   4 | BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |



To see the last five rows use  <b>.tail()</b> method. tail() also accepts a number, and in this case we printing the bottom two rows.:


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.tail()
```
|     | Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|----:|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| 332 | NL     | PLUM POINT       | 8402958 |         1972 |           7 |         2016 |           6 |       51.07 |       -56.88 |          6 | N              |
| 333 | NL     | PORT AUXBASQUES  | 8402975 |         1909 |           2 |         2017 |           9 |       47.58 |       -58.97 |         40 | N              |
| 334 | NL     | ST ANTHONY       | 8403389 |         1946 |           6 |         2017 |          12 |       51.37 |       -55.6  |         33 | Y              |
| 335 | NL     | ST JOHN'S        | 8403505 |         1874 |           1 |         2017 |          12 |       47.62 |       -52.75 |        141 | Y              |
| 336 | NL     | STEPHENVILLE     | 8403801 |         1895 |           6 |         2017 |          12 |       48.53 |       -58.55 |         26 | Y              |
| 337 | NL     | WABUSH LAKE      | 8504177 |         1960 |          11 |         2017 |          12 |       52.93 |       -66.87 |        551 | Y              |



Before exploring a Dataframe, you can modify the index to make it easier to analyze the dataset. For this, we use the <b> .set_index () </b> function. We must create a new object.


```python
dataframe_Prov_index = dataframe.set_index("Prov")
```
```python
dataframe_Prov_index.head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |

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

| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |

```python
# Example3: iloc: # select all rows and 4 specific columns 
dataframe_Prov_index.iloc[:,0:4].head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |
|:-------|:-----------------|:--------|-------------:|------------:|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |
| BC     | ATLIN            | 1200560 |         1905 |           8 |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |


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
    

| Prov   | stnid   |   année déb. |
|:-------|:--------|-------------:|
| BC     | 1100120 |         1893 |
| BC     | 1200560 |         1905 |
| BC     | 1090660 |         1888 |
| BC     | 1130771 |         1939 |
| BC     | 1060841 |         1895 |

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
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| QC     | AMOS             | 709CEE9 |         1913 |           6 |         2017 |           8 |       48.57 |       -78.13 |        305 | Y              |
| QC     | BAGOTVILLE       | 7060400 |         1880 |          11 |         2017 |          12 |       48.33 |       -71    |        159 | Y              |
| QC     | BAIE COMEAU      | 704S001 |         1965 |           1 |         2017 |          12 |       49.13 |       -68.2  |        130 | Y              |
| QC     | BEAUCEVILLE      | 7027283 |         1913 |           8 |         2017 |           8 |       46.15 |       -70.7  |        168 | Y              |
| QC     | BELLETERRE       | 7080600 |         1951 |           9 |         2004 |           4 |       47.38 |       -78.7  |        322 | N              |

```python
# Example3: Select all rows for multiple columns, say list[]

dataframe_Prov_index.loc[:,["Nom de station", "année déb.", "année fin."]].head()
```
| Prov   | Nom de station   |   année déb. |   année fin. |
|:-------|:-----------------|-------------:|-------------:|
| BC     | AGASSIZ          |         1893 |         2017 |
| BC     | ATLIN            |         1905 |         2017 |
| BC     | BARKERVILLE      |         1888 |         2015 |
| BC     | BEAVERDELL       |         1939 |         2006 |
| BC     | BELLA COOLA      |         1895 |         2017 |

```python
# Example4: Select few rows for multiple columns, say list[]
dataframe_Prov_index.loc[['BC','QC'],["Nom de station", "année déb.", "année fin."]].head()
```
| Prov   | Nom de station   |   année déb. |   année fin. |
|:-------|:-----------------|-------------:|-------------:|
| BC     | AGASSIZ          |         1893 |         2017 |
| BC     | ATLIN            |         1905 |         2017 |
| BC     | BARKERVILLE      |         1888 |         2015 |
| BC     | BEAVERDELL       |         1939 |         2006 |
| BC     | BELLA COOLA      |         1895 |         2017 |

```python
# Example 5: # for getting values with a boolean array

(dataframe_Prov_index.loc['BC',["année déb."]]>1900).head()
```
| Prov   |   année déb. |
|:-------|-------------:|
| BC     |            False |
| BC     |            True |
| BC     |            False |
| BC     |            True |
| BC     |            False |

```python
# Example 6: # for getting values with a boolean array
dataframe_Prov_index.loc[dataframe_Prov_index["année fin."]>2015,:].head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |
| BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 | N              |
| BC     | BLUE RIVER       | 1160899 |         1946 |           9 |         2017 |          12 |       52.13 |      -119.28 |        683 | Y              |


```python
# Example 7: # for getting values with a boolean array
df2 = dataframe_Prov_index.loc["QC",:]
df2.loc[df2["année fin."]==2017,:].head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| QC     | AMOS             | 709CEE9 |         1913 |           6 |         2017 |           8 |       48.57 |       -78.13 |        305 | Y              |
| QC     | BAGOTVILLE       | 7060400 |         1880 |          11 |         2017 |          12 |       48.33 |       -71    |        159 | Y              |
| QC     | BAIE COMEAU      | 704S001 |         1965 |           1 |         2017 |          12 |       49.13 |       -68.2  |        130 | Y              |
| QC     | BEAUCEVILLE      | 7027283 |         1913 |           8 |         2017 |           8 |       46.15 |       -70.7  |        168 | Y              |
| QC     | CAUSAPSCAL       | 7051200 |         1913 |          11 |         2017 |           8 |       48.37 |       -67.23 |        168 | N              |



### 7.2.3  Change a Dataframe

   ### 7.2.3.1 Column Selection/Addition/Deletion-
 
We will use here our previous Dataframe.


```python
dataframe_Prov_index.head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |

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
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |   total année |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|--------------:|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |           125 |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |           113 |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |           128 |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |            68 |





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
    
|     | Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) |
|----:|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|
|   0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 |
|   1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 |
|   2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 |
|   3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 |
|   4 | BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 |

```python
# using pop function
print ("Deleting 'stnid' column using POP function:")
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.pop('stnid')
dataframe.head()
```

    Deleting 'stnid' column using POP function:
    
|     | Prov   | Nom de station   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|----:|:-------|:-----------------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
|   0 | BC     | AGASSIZ          |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
|   1 | BC     | ATLIN            |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
|   2 | BC     | BARKERVILLE      |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
|   3 | BC     | BEAVERDELL       |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
|   4 | BC     | BELLA COOLA      |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |


```python
# using drop method
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3))
dataframe.drop(["stns jointes"], axis=1).head()
```
|     | Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) |
|----:|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|
|   0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 |
|   1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 |
|   2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 |
|   3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 |
|   4 | BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 |


   ### 7.2.3.2  Row Selection/Addition/Deletion-
   
We will now understand row selection, addition and deletion through examples. Let us begin with the concept of selection.

 #### a-  Row Selection
 
Selection by Label
Rows can be selected by passing row label to a loc function.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |


```python
dataframe.loc['BC'].head()
```
| Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |


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
| Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |


#### b-  Row Addition

Add new rows to a DataFrame using function <b>append()</b> function. This function will append the rows at the end.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
```


```python
df_new = pd.DataFrame({'Nom de station': ['station1', 'station2'], 'stnid': [8888, 9999], 'Prov': ['BC', 'QC']}).set_index("Prov")
df_new
```
| Prov   | Nom de station   |   stnid |
|:-------|:-----------------|--------:|
| BC     | station1         |    8888 |
| QC     | station2         |    9999 |


```python
dataframe = dataframe.append(df_new)
dataframe.tail()
```
| Prov   | Nom de station   |   année déb. |   année fin. |   lat (deg) |   long (deg) |   mois déb. |   mois fin. |   stnid | stns jointes   |   élév (m) |
|:-------|:-----------------|-------------:|-------------:|------------:|-------------:|------------:|------------:|--------:|:---------------|-----------:|
| NL     | ST JOHN'S        |         1874 |         2017 |       47.62 |       -52.75 |           1 |          12 | 8403505 | Y              |        141 |
| NL     | STEPHENVILLE     |         1895 |         2017 |       48.53 |       -58.55 |           6 |          12 | 8403801 | Y              |         26 |
| NL     | WABUSH LAKE      |         1960 |         2017 |       52.93 |       -66.87 |          11 |          12 | 8504177 | Y              |        551 |
| BC     | station1         |          nan |          nan |      nan    |       nan    |         nan |         nan |    8888 | nan            |        nan |
| QC     | station2         |          nan |          nan |      nan    |       nan    |         nan |         nan |    9999 | nan            |        nan |


#### c-  Row Deletion

Use index label to delete or drop rows from a DataFrame. If label is duplicated, then multiple rows will be dropped.


```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.head()

```
| Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              |
| BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |
| BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              |
| BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |
| BC     | BELLA COOLA      | 1060841 |         1895 |           5 |         2017 |          11 |       52.37 |      -126.68 |         18 | Y              |


```python
# Drop rows with label 'BC'
dataframe = dataframe.drop('BC')
dataframe.head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| YT     | BURWASH          | 2100181 |         1966 |          10 |         2017 |          12 |       61.37 |      -139.05 |        807 | Y              |
| YT     | DAWSON           | 2100LRP |         1901 |           1 |         2017 |          12 |       64.05 |      -139.13 |        370 | Y              |
| N   YT | HAINES JUNCTIO   | 2100630 |         1944 |          10 |         2017 |          12 |       60.75 |      -137.5  |        596 | N              |
| YT     | KOMAKUK BEACH    | 2100682 |         1958 |           7 |         2017 |          12 |       69.62 |      -140.2  |         13 | Y              |
| YT     | MAYO             | 2100701 |         1924 |          10 |         2017 |          12 |       63.62 |      -135.87 |        504 | Y              |

```python
dataframe = pd.read_excel("./DATA/Homog_Temperature_Stations.xls", skiprows = range(0, 3)).set_index("Prov")
dataframe.loc['ON'].head()
```
| Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |
|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|
| ON     | ATIKOKAN         | 6020LPQ |         1917 |           1 |         2017 |          12 |       48.8  |       -91.58 |        442 | Y              |
| ON     | BEATRICE         | 6110607 |         1878 |           1 |         2017 |          12 |       45.13 |       -79.4  |        297 | Y              |
| ON     | BELLEVILLE       | 6150689 |         1921 |           1 |         2017 |          12 |       44.15 |       -77.4  |         76 | N              |
| ON     | BIG TROUT LAKE   | 6010735 |         1939 |           2 |         2017 |          12 |       53.83 |       -89.87 |        224 | Y              |
| ON     | BROCKVILLE       | 6100971 |         1915 |           7 |         2017 |          12 |       44.6  |       -75.67 |         96 | Y              |

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

|    |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|
|  0 |    1 | MONTREAL TAVISH  | var1       |
|  1 |    2 | QUEBEC           | var2       |
|  2 |    3 | TADOUSSAC        | var6       |
|  3 |    4 | OKA              | var5       |



```python
right_dataframe
```

|    |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|
|  0 |    1 | TORONTO          | var3       |
|  1 |    2 | OTTAWA           | var1       |
|  2 |    3 | KINGSTON         | var6       |
|  3 |    4 | CHAPLEAU         | var5       |




#### a-  Merge Two DataFrames on a Key


```python
pd.merge(left_dataframe,right_dataframe,on='id')
```

|    |   id | Nom de station_x   | variable_x   | Nom de station_y   | variable_y   |
|---:|-----:|:-------------------|:-------------|:-------------------|:-------------|
|  0 |    1 | MONTREAL TAVISH    | var1         | TORONTO            | var3         |
|  1 |    2 | QUEBEC             | var2         | OTTAWA             | var1         |
|  2 |    3 | TADOUSSAC          | var6         | KINGSTON           | var6         |
|  3 |    4 | OKA                | var5         | CHAPLEAU           | var5         |





#### b-  Merge Two DataFrames on a Key


```python
pd.merge(left_dataframe,right_dataframe,on=['id','variable'])
```
|    |   id | Nom de station_x   | variable   | Nom de station_y   |
|---:|-----:|:-------------------|:-----------|:-------------------|
|  0 |    3 | TADOUSSAC          | var6       | KINGSTON           |
|  1 |    4 | OKA                | var5       | CHAPLEAU           |






#### c-  Merge Two DataFrames Using 'How' argument

The how argument to merge specifies how to determine which keys are to be included in the resulting table. If a key combination does not appear in either the left or the right tables, the values in the joined table will be NA.



```python
# Left Join
pd.merge(left_dataframe, right_dataframe, on='variable', how='left')
```
|    |   id_x | Nom de station_x   | variable   |   id_y | Nom de station_y   |
|---:|-------:|:-------------------|:-----------|-------:|:-------------------|
|  0 |      1 | MONTREAL TAVISH    | var1       |      2 | OTTAWA             |
|  1 |      2 | QUEBEC             | var2       |    nan | nan                |
|  2 |      3 | TADOUSSAC          | var6       |      3 | KINGSTON           |
|  3 |      4 | OKA                | var5       |      4 | CHAPLEAU           |

```python
# right Join
pd.merge(left_dataframe, right_dataframe, on='variable', how='right')
```
|    |   id_x | Nom de station_x   | variable   |   id_y | Nom de station_y   |
|---:|-------:|:-------------------|:-----------|-------:|:-------------------|
|  0 |      1 | MONTREAL TAVISH    | var1       |      2 | OTTAWA             |
|  1 |      3 | TADOUSSAC          | var6       |      3 | KINGSTON           |
|  2 |      4 | OKA                | var5       |      4 | CHAPLEAU           |
|  3 |    nan | nan                | var3       |      1 | TORONTO            |

```python
# outer Join
pd.merge(left_dataframe, right_dataframe, on='variable', how='outer')
```
|    |   id_x | Nom de station_x   | variable   |   id_y | Nom de station_y   |
|---:|-------:|:-------------------|:-----------|-------:|:-------------------|
|  0 |      1 | MONTREAL TAVISH    | var1       |      2 | OTTAWA             |
|  1 |      2 | QUEBEC             | var2       |    nan | nan                |
|  2 |      3 | TADOUSSAC          | var6       |      3 | KINGSTON           |
|  3 |      4 | OKA                | var5       |      4 | CHAPLEAU           |
|  4 |    nan | nan                | var3       |      1 | TORONTO            |


```python
# inner Join
pd.merge(left_dataframe, right_dataframe, on='variable', how='inner')
```
|    |   id_x | Nom de station_x   | variable   |   id_y | Nom de station_y   |
|---:|-------:|:-------------------|:-----------|-------:|:-------------------|
|  0 |      1 | MONTREAL TAVISH    | var1       |      2 | OTTAWA             |
|  1 |      3 | TADOUSSAC          | var6       |      3 | KINGSTON           |
|  2 |      4 | OKA                | var5       |      4 | CHAPLEAU           |

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
|    |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|
|  0 |    1 | MONTREAL TAVISH  | var1       |
|  1 |    2 | QUEBEC           | var2       |
|  2 |    3 | TADOUSSAC        | var6       |
|  3 |    4 | OKA              | var5       |
|  0 |    1 | TORONTO          | var3       |
|  1 |    2 | OTTAWA           | var1       |
|  2 |    3 | KINGSTON         | var6       |
|  3 |    4 | CHAPLEAU         | var5       |




Suppose we wanted to associate specific keys with each of the pieces of the chopped up DataFrame. We can do this by using the keys argument −


```python
pd.concat([dataframe1,dataframe2],keys=['QC','ON'])
```
|           |   id | Nom de station   | variable   |
|:----------|-----:|:-----------------|:-----------|
| ('QC', 0) |    1 | MONTREAL TAVISH  | var1       |
| ('QC', 1) |    2 | QUEBEC           | var2       |
| ('QC', 2) |    3 | TADOUSSAC        | var6       |
| ('QC', 3) |    4 | OKA              | var5       |
| ('ON', 0) |    1 | TORONTO          | var3       |
| ('ON', 1) |    2 | OTTAWA           | var1       |
| ('ON', 2) |    3 | KINGSTON         | var6       |
| ('ON', 3) |    4 | CHAPLEAU         | var5       |




If we don't want the index being duplicated, set ignore_index to True.


```python
pd.concat([dataframe1,dataframe2],keys=['QC','ON'],ignore_index=True)
```
|    |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|
|  0 |    1 | MONTREAL TAVISH  | var1       |
|  1 |    2 | QUEBEC           | var2       |
|  2 |    3 | TADOUSSAC        | var6       |
|  3 |    4 | OKA              | var5       |
|  4 |    1 | TORONTO          | var3       |
|  5 |    2 | OTTAWA           | var1       |
|  6 |    3 | KINGSTON         | var6       |
|  7 |    4 | CHAPLEAU         | var5       |


If the two Dataframes need to be added along axis=1, then the new columns will be appended.


```python
pd.concat([dataframe1,dataframe2],axis=1)
```
|    |   id | Nom de station   | variable   |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|-----:|:-----------------|:-----------|
|  0 |    1 | MONTREAL TAVISH  | var1       |    1 | TORONTO          | var3       |
|  1 |    2 | QUEBEC           | var2       |    2 | OTTAWA           | var1       |
|  2 |    3 | TADOUSSAC        | var6       |    3 | KINGSTON         | var6       |
|  3 |    4 | OKA              | var5       |    4 | CHAPLEAU         | var5       |



####  Concatenating Using append

A useful shortcut to concat are the append instance methods on DataFrame. They concatenate along axis=0, namely the index 


```python
dataframe1.append(dataframe2)
```
|    |   id | Nom de station   | variable   |
|---:|-----:|:-----------------|:-----------|
|  0 |    1 | MONTREAL TAVISH  | var1       |
|  1 |    2 | QUEBEC           | var2       |
|  2 |    3 | TADOUSSAC        | var6       |
|  3 |    4 | OKA              | var5       |
|  0 |    1 | TORONTO          | var3       |
|  1 |    2 | OTTAWA           | var1       |
|  2 |    3 | KINGSTON         | var6       |
|  3 |    4 | CHAPLEAU         | var5       |


### 7.2.4  Basic Functionality on DataFrame

There are many built-in functions and methods:

https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.html


We will present some useful functions with exploring a dataset.


```python
dataframe = pd.read_csv("./DATA/Climato_Stations_ECCC_1981_2010_YEAR.csv", encoding='latin-1')
dataframe.head()
```
|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |      Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|----------:|----------:|---------:|
|  0 |            0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |   5.63043 |   18.9033 |  -3.46052 | -19.235   |  860.083 |
|  2 |            2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |  12.628   |   23.6417 |   4.01748 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 | N              |  12.1556  |   20.2007 |   6.77689 |   1.09467 | 2518.68  |

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

|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |      Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|----------:|----------:|---------:|
|  0 |            0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |   5.63043 |   18.9033 |  -3.46052 | -19.235   |  860.083 |
|  2 |            2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |  12.628   |   23.6417 |   4.01748 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 | N              |  12.1556  |   20.2007 |   6.77689 |   1.09467 | 2518.68  |

```python
df_label_sorted = dataframe.sort_values(by="Prov")
df_label_sorted.head()
```
|     |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |     Tmax |   Tmax90p |     Tmin |   Tmin10p |      DG0 |
|----:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|---------:|----------:|---------:|----------:|---------:|
| 127 |          127 | AB     | SLAVE LAKE       | 3065995 |         1922 |           8 |         2017 |          12 |       55.3  |      -114.78 |        583 | Y              |  7.48137 |   22.4643 | -3.42227 |  -20.3803 | 1131.03  |
| 106 |          106 | AB     | EDMONTON         | 3012216 |         1880 |           7 |         2017 |          12 |       53.57 |      -113.52 |        723 | Y              |  8.98212 |   24.328  | -3.11709 |  -19.1907 | 1095.93  |
| 104 |          104 | AB     | COLD LAKE        | 3081680 |         1925 |           7 |         2017 |          12 |       54.42 |      -110.28 |        541 | Y              |  7.72448 |   24.2737 | -3.03759 |  -21.2037 | 1303.95  |
| 103 |          103 | AB     | CARWAY           | 3031402 |         1914 |           8 |         2017 |          12 |       49    |      -113.37 |       1354 | Y              | 11.1397  |   24.925  | -1.61886 |  -13.98   |  956.837 |
| 102 |          102 | AB     | CAMROSE          | 3011240 |         1946 |           3 |         2017 |          12 |       53.03 |      -112.82 |        739 | N              |  8.96497 |   24.1757 | -3.71442 |  -20.588  | 1048.13  |

The argument could takes a list of column values.

```python
df_label_sorted = dataframe.sort_values(by=['Prov','année déb.'])
df_label_sorted.head()
```
|     |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |     Tmax |   Tmax90p |     Tmin |   Tmin10p |     DG0 |
|----:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|---------:|----------:|---------:|----------:|--------:|
| 106 |          106 | AB     | EDMONTON         | 3012216 |         1880 |           7 |         2017 |          12 |       53.57 |      -113.52 |        723 | Y              |  8.98212 |   24.328  | -3.11709 |  -19.1907 | 1095.93 |
| 110 |          110 | AB     | FORT CHIPEWYAN   | 3072655 |         1883 |          10 |         2017 |          12 |       58.77 |      -111.12 |        238 | Y              |  4.28219 |   23.566  | -6.54421 |  -28.6297 | 1135.11 |
| 121 |          121 | AB     | MEDICINE HAT     | 3034485 |         1883 |           8 |         2017 |          12 |       50.02 |      -110.72 |        717 | Y              | 12.6489  |   28.4973 | -0.1559  |  -15.7833 | 1563.87 |
|  99 |           99 | AB     | CALGARY          | 3031092 |         1885 |           1 |         2017 |          12 |       51.12 |      -114.02 |       1084 | Y              | 10.835   |   24.4673 | -1.44461 |  -15.235  | 1172.05 |
|  97 |           97 | AB     | BANFF            | 3050519 |         1887 |          11 |         2017 |          12 |       51.2  |      -115.55 |       1397 | Y              |  8.90652 |   23.132  | -3.08488 |  -15.8583 |  750.37 |

- <b>sort_index()</b> method:

Using the sort_index() method, by passing the axis arguments and the order of sorting, DataFrame can be sorted. By default, sorting is done on row labels in ascending order.


```python
df_label_sorted.sort_index().head()
```
|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |      Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|----------:|----------:|---------:|
|  0 |            0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |   5.63043 |   18.9033 |  -3.46052 | -19.235   |  860.083 |
|  2 |            2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |  12.628   |   23.6417 |   4.01748 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 | N              |  12.1556  |   20.2007 |   6.77689 |   1.09467 | 2518.68  |


```python
df_label_sorted.sort_index(ascending=False).head()
```
|     |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |      Tmin |   Tmin10p |      DG0 |
|----:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|----------:|----------:|---------:|
| 288 |          288 | NL     | WABUSH LAKE      | 8504177 |         1960 |          11 |         2017 |          12 |       52.93 |       -66.87 |        551 | Y              |   2.33974 |   19.6937 |  -8.02478 |  -29.4537 |  792.913 |
| 287 |          287 | NL     | STEPHENVILLE     | 8403801 |         1895 |           6 |         2017 |          12 |       48.53 |       -58.55 |         26 | Y              |   8.80653 |   20.614  |   1.81275 |  -10.582  | 1710.17  |
| 286 |          286 | NL     | ST JOHN'S        | 8403505 |         1874 |           1 |         2017 |          12 |       47.62 |       -52.75 |        141 | Y              |   9.07367 |   21.6237 |   1.54977 |   -8.919  | 1474.82  |
| 285 |          285 | NL     | ST ANTHONY       | 8403389 |         1946 |           6 |         2017 |          12 |       51.37 |       -55.6  |         33 | Y              | nan       |  nan      | nan       |  nan      |  nan     |
| 284 |          284 | NL     | PORT AUXBASQUES  | 8402975 |         1909 |           2 |         2017 |           9 |       47.58 |       -58.97 |         40 | N              | nan       |  nan      | nan       |  nan      |  nan     |


```python
df_label_sorted.sort_index(axis=1).head()
```
|     |     DG0 | Nom de station   | Prov   |     Tmax |   Tmax90p |     Tmin |   Tmin10p |   Unnamed: 0 |   année déb. |   année fin. |   lat (deg) |   long (deg) |   mois déb. |   mois fin. |   stnid | stns jointes   |   élév (m) |
|----:|--------:|:-----------------|:-------|---------:|----------:|---------:|----------:|-------------:|-------------:|-------------:|------------:|-------------:|------------:|------------:|--------:|:---------------|-----------:|
| 106 | 1095.93 | EDMONTON         | AB     |  8.98212 |   24.328  | -3.11709 |  -19.1907 |          106 |         1880 |         2017 |       53.57 |      -113.52 |           7 |          12 | 3012216 | Y              |        723 |
| 110 | 1135.11 | FORT CHIPEWYAN   | AB     |  4.28219 |   23.566  | -6.54421 |  -28.6297 |          110 |         1883 |         2017 |       58.77 |      -111.12 |          10 |          12 | 3072655 | Y              |        238 |
| 121 | 1563.87 | MEDICINE HAT     | AB     | 12.6489  |   28.4973 | -0.1559  |  -15.7833 |          121 |         1883 |         2017 |       50.02 |      -110.72 |           8 |          12 | 3034485 | Y              |        717 |
|  99 | 1172.05 | CALGARY          | AB     | 10.835   |   24.4673 | -1.44461 |  -15.235  |           99 |         1885 |         2017 |       51.12 |      -114.02 |           1 |          12 | 3031092 | Y              |       1084 |
|  97 |  750.37 | BANFF            | AB     |  8.90652 |   23.132  | -3.08488 |  -15.8583 |           97 |         1887 |         2017 |       51.2  |      -115.55 |          11 |          12 | 3050519 | Y              |       1397 |

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
|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) |   stns jointes |     Tmax |   Tmax90p |     Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|---------------:|---------:|----------:|---------:|----------:|---------:|
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 |            nan |  5.63043 |   18.9033 | -3.46052 | -19.235   |  860.083 |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 |              1 | 12.628   |   23.6417 |  4.01748 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 |            nan | 12.1556  |   20.2007 |  6.77689 |   1.09467 | 2518.68  |
|  5 |            5 | BC     | BLUE RIVER       | 1160899 |         1946 |           9 |         2017 |          12 |       52.13 |      -119.28 |        683 |              1 | 10.4408  |   25.9917 | -1.12501 | -12.5823  |  987.363 |
|  9 |            9 | BC     | COMOX            | 1021830 |         1935 |          11 |         2017 |          12 |       49.72 |      -124.9  |         26 |              1 | 13.7376  |   23.1023 |  6.42485 |  -0.526   | 2444.39  |


```python
dataframe["Tmin"]=dataframe["Tmin"].apply(lambda x: round(x,2))
dataframe["Tmax"]=dataframe["Tmax"].apply(lambda x: int(x))
dataframe.head()
```

|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) |   stns jointes |   Tmax |   Tmax90p |   Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|---------------:|-------:|----------:|-------:|----------:|---------:|
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 |            nan |      5 |   18.9033 |  -3.46 | -19.235   |  860.083 |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 |              1 |     12 |   23.6417 |   4.02 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 |            nan |     12 |   20.2007 |   6.78 |   1.09467 | 2518.68  |
|  5 |            5 | BC     | BLUE RIVER       | 1160899 |         1946 |           9 |         2017 |          12 |       52.13 |      -119.28 |        683 |              1 |     10 |   25.9917 |  -1.13 | -12.5823  |  987.363 |
|  9 |            9 | BC     | COMOX            | 1021830 |         1935 |          11 |         2017 |          12 |       49.72 |      -124.9  |         26 |              1 |     13 |   23.1023 |   6.42 |  -0.526   | 2444.39  |


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
|    |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |      Tmin |   Tmin10p |      DG0 |
|---:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|----------:|----------:|---------:|
|  0 |            0 | BC     | AGASSIZ          | 1100120 |         1893 |           1 |         2017 |          12 |       49.25 |      -121.77 |         15 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  1 |            1 | BC     | ATLIN            | 1200560 |         1905 |           8 |         2017 |          12 |       59.57 |      -133.7  |        674 | N              |   5.63043 |   18.9033 |  -3.46052 | -19.235   |  860.083 |
|  2 |            2 | BC     | BARKERVILLE      | 1090660 |         1888 |           2 |         2015 |           3 |       53.07 |      -121.52 |       1265 | N              | nan       |  nan      | nan       | nan       |  nan     |
|  3 |            3 | BC     | BEAVERDELL       | 1130771 |         1939 |           1 |         2006 |           9 |       49.48 |      -119.05 |        838 | Y              |  12.628   |   23.6417 |   4.01748 |  -3.646   | 1798.09  |
|  4 |            4 | BC     | BLIND CHANNEL    | 1021480 |         1958 |           7 |         2016 |           2 |       50.42 |      -125.5  |         23 | N              |  12.1556  |   20.2007 |   6.77689 |   1.09467 | 2518.68  |


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
|     |   Unnamed: 0 | Prov   | Nom de station   | stnid   |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |      Tmax |   Tmax90p |       Tmin |   Tmin10p |     DG0 |
|----:|-------------:|:-------|:-----------------|:--------|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|----------:|----------:|-----------:|----------:|--------:|
| 216 |          216 | QC     | AMOS             | 709CEE9 |         1913 |           6 |         2017 |           8 |       48.57 |       -78.13 |        305 | Y              | nan       |  nan      | nan        |  nan      |  nan    |
| 217 |          217 | QC     | BAGOTVILLE       | 7060400 |         1880 |          11 |         2017 |          12 |       48.33 |       -71    |        159 | Y              |   8.28139 |   25.2973 |  -1.83359  |  -20.8117 | 1528.41 |
| 218 |          218 | QC     | BEAUCEVILLE      | 7027283 |         1913 |           8 |         2017 |           8 |       46.15 |       -70.7  |        168 | Y              |  10.5515  |   26.0783 |  -1.37634  |  -19.6283 | 1509.36 |
| 219 |          219 | QC     | BROME            | 7020840 |         1890 |           9 |         2014 |           7 |       45.18 |       -72.57 |        206 | N              |  11.1409  |   26.1767 |  -0.294151 |  -17.56   | 1676.23 |
| 220 |          220 | QC     | CAUSAPSCAL       | 7051200 |         1913 |          11 |         2017 |           8 |       48.37 |       -67.23 |        168 | N              | nan       |  nan      | nan        |  nan      |  nan    |


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
| Prov   |       amin |        mean |       amax |        std |
|:-------|-----------:|------------:|-----------:|-----------:|
| AB     |  -6.54421  |  -3.05093   |  -0.1559   |   1.40133  |
| BC     |  -6.06858  |   1.57802   |   7.01629  |   3.89638  |
| MB     | -10.0943   |  -4.4939    |  -1.98027  |   2.61835  |
| N   YT | nan        | nan         | nan        | nan        |
| NB     |  -0.491043 |   0.34175   |   0.840796 |   0.598429 |
| NL     |  -8.02478  |  -1.32433   |   1.81275  |   3.42585  |
| NS     |   1.21413  |   2.54263   |   3.75946  |   0.982653 |
| NT     | -12.4518   |  -8.51865   |  -6.68323  |   2.16937  |
| NU     | -21.9351   | -16.5227    | -12.2332   |   3.0491   |
| ON     |  -7.48484  |   0.0319696 |   5.91872  |   3.64788  |
| PE     |   1.98683  |   1.98683   |   1.98683  | nan        |
| QC     |  -8.76805  |  -1.99269   |   1.62212  |   2.70668  |
| SK     |  -5.01656  |  -3.20898   |  -1.42885  |   1.03055  |
| YT     | -10.2177   |  -8.99542   |  -7.77313  |   1.72858  |


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

|     |   Unnamed: 0 | Prov   | Nom de station   |   stnid |   année déb. |   mois déb. |   année fin. |   mois fin. |   lat (deg) |   long (deg) |   élév (m) | stns jointes   |     Tmax |   Tmax90p |      Tmin |   Tmin10p |     DG0 |
|----:|-------------:|:-------|:-----------------|--------:|-------------:|------------:|-------------:|------------:|------------:|-------------:|-----------:|:---------------|---------:|----------:|----------:|----------:|--------:|
|  52 |           52 | N   YT | HAINES JUNCTIO   | 2100630 |         1944 |          10 |         2017 |          12 |       60.75 |      -137.5  |        596 | N              | nan      |  nan      | nan       |  nan      |  nan    |
| 274 |          274 | PE     | CHARLOTTETOWN    | 8300301 |         1872 |          11 |         2017 |          12 |       46.28 |       -63.13 |         49 | Y              |  10.0063 |   23.7683 |   1.98683 |  -12.0367 | 1912.16 |

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

| Class | Description |
|--|--|
| <b>datetime.date</b> | A date instance represents a date |
| <b>datetime.datetime</b> |  An instance of datetime represents a date and time according to the Gregorian calendar |
| <b>datetime.time</b> |  An instance of time represents the time, except for the date |
| <b>datetime.timedelta</b> |The timedelta class is used to keep the differences between two temporal or dated objects |
| <b>datetime.tzinfo</b> |The tzinfo class is used to implement time zone support for time and datetime objects |




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