---
title: 6 Numpy library
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 6
---

<img src="./figures/NumPy_logo.svg" alt="Indentation" width="30%" height="30%">
![image0](/img/Numpy_logo.svg)


- Numpy is the core library for scientific computing in Python
- A new data container will be used: the ndarray (N-dimensional array). There are vectors (one-dimensional arrays), multidimensional arrays
- It provides a high-performance multidimensional array object, and tools for working with these arrays
We'll see how to initialize Numpy arrays in several ways, access values in arrays, perform math and matrix operations, and use arrays for both masking and comparisons.

https://docs.scipy.org/doc/numpy/reference/


## 6.1- Create a Numpy array or ndarray
 
We first need to import the numpy package:


```python
# We will import Numpy library and create alias. 
# Codes with aliases are easier to write and read. 
import numpy as np
import warnings
warnings.filterwarnings("ignore")
```

A numpy array is a grid of values, all of the same type, and is indexed by a tuple of nonnegative integers. The number of dimensions is the rank of the array; the shape of an array is a tuple of integers giving the size of the array along each dimension.

Unlike a list, you can not create empty Numpy tables. You will find below several ways to initialize a Numpy table according to your needs:

- Using <b>array()</b> function to create Numpy array:


```python
table1 = np.array([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20])
table1
```




    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17,
           18, 19, 20])



Creation of a two-dimensional array with rows and columns; we create a list of lists. Each list is a row of the table.


```python
#  2 rows and 3 columns
table2 = np.array([[1,2,3], [4,5,6]])
table2
```




    array([[1, 2, 3],
           [4, 5, 6]])




```python
#  3 rows and 3 columns
table3 = np.array([[1,2,3], [4,5,6], [7,8,9]])
table3
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



- Using <b>range()</b> function to create Numpy array:


```python
table4 = np.array(range(10)) # table with values from 0 to 9
table4
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])



-  Using <b>zeros()</b> function to create Numpy array with '0' value :


```python
table5 = np.zeros((4,3)) # table with 4 rows and 3 columns
table5
```




    array([[0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.]])



- Using <b>ones()</b> function to create Numpy array with ones:


```python
table6 = np.ones((4,3)) # table with 4 rows and 3 columns
table6
```




    array([[1., 1., 1.],
           [1., 1., 1.],
           [1., 1., 1.],
           [1., 1., 1.]])



- Using <b>identity()</b> function to create Numpy array as matrix identity:


```python
table7 = np.identity(4) # 4 dimensions
table7
```




    array([[1., 0., 0., 0.],
           [0., 1., 0., 0.],
           [0., 0., 1., 0.],
           [0., 0., 0., 1.]])



- Converting list to ndarray with <b>array()</b> function


```python
my_list = [0,1,2,3,4,5,6]
my_list
```




    [0, 1, 2, 3, 4, 5, 6]




```python
table8 = np.array(my_list)
table8
```




    array([0, 1, 2, 3, 4, 5, 6])



- Using <b>random()</b> function to create ndarray with random values:


```python
table9 = np.random.randint(100,size=(4,3))  #  4*3  ndarray with random values between  0 and 100 
table9
```




    array([[78, 47, 23],
           [79, 17,  5],
           [61, 41, 71],
           [12, 41, 27]])



- Using <b>full()</b>  to create a constant array.


```python
table10 = np.full((2,2), 7) # Create a constant array
table10
```




    array([[7, 7],
           [7, 7]])



## 6.2 Access data in a Numpy or ndarray array

We can access an individual element or a slice of values. Similar to lists, the first element is indexed to 0. For example, array1 [0,0] indicates that we are accessing the first row and the first column. The first number of the tuple [0,0] indicates the index of the line and the second number indicates the index of the column:



```python
my_table = np.array([[1,2,3], [4,5,6], [7,8,9]])
my_table
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



- Here are some examples to access values in a numpy array:


```python
my_table[1,2]     # We want the element located at row with index 1 and column with index 2
                  #  ndarray(row,column) 
```




    6




```python
my_table[1,-1]    # We want the element at row index 1 and last column
```




    6




```python
my_table[0,1]     # We want the element located at row with index 0 and column with index 1
```




    2




```python
my_table[1,0]     # We want the element located at row with index 1 and column with index 0                     
```




    4



- Here are some examples to access data using <b>Slicing</b>


```python
my_table[:,0]    # We want all rows with column index 0
```




    array([1, 4, 7])




```python
my_table[0,:]    # We want all columns with row index 0
```




    array([1, 2, 3])




```python
my_table[:,0:3:2] # We want all rows and index columns from 0 to 3 with steps of 2.
                  # So all rows and columns 1 and 2.
```




    array([[1, 3],
           [4, 6],
           [7, 9]])




```python
my_table[:,-1]  #We want all rows at last column
```




    array([3, 6, 9])




```python
my_table[:,1:-1] # We want all rows with columns between index 1 and last index
```




    array([[2],
           [5],
           [8]])




```python
my_table[2,1:-1] # We want values at row with index 2 and rows between index 1 and last index
```




    array([8])



## 6.3 Mathematical and matrix calculations on a Numpy array:

Numpy tables are very easy to manipulate: concatenate, add, multiply, transpose with a single line of code.
Below you will find some examples of various arithmetic and multiplicative operations with Numpy tables.


```python
array1 = np.arange(9).reshape(3,3)
array1
```




    array([[0, 1, 2],
           [3, 4, 5],
           [6, 7, 8]])




```python
array2 = np.random.randint(50, size=(3,3))
array2
```




    array([[47, 20, 49],
           [40, 15,  7],
           [ 4, 35, 14]])



- Basic arithmetic operations: addition, subtraction, multiplication, division
Here a list of mathematical functions provided by numpy in: https://docs.scipy.org/doc/numpy/reference/routines.math.html


```python
array1 + 10 # add a value to each element
```




    array([[10, 11, 12],
           [13, 14, 15],
           [16, 17, 18]])




```python
array1 - 10 # substract value to each element 
```




    array([[-10,  -9,  -8],
           [ -7,  -6,  -5],
           [ -4,  -3,  -2]])




```python
array1 * 100 # multiply value to each element 
```




    array([[  0, 100, 200],
           [300, 400, 500],
           [600, 700, 800]])




```python
array1[:,0] * 10 # we multiply by 10 all elements at column with index 0
```




    array([ 0, 30, 60])




```python
array1 / 2 # we divide a value to each element
```




    array([[0. , 0.5, 1. ],
           [1.5, 2. , 2.5],
           [3. , 3.5, 4. ]])



- some Numpy functions and methods applicable on Numpy tables:

<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.all.html#numpy.all" title="numpy.all"><code class="xref py py-obj docutils literal"><span class="pre">all</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.any.html#numpy.any" title="numpy.any"><code class="xref py py-obj docutils literal"><span class="pre">any</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.apply_along_axis.html#numpy.apply_along_axis" title="numpy.apply_along_axis"><code class="xref py py-obj docutils literal"><span class="pre">apply_along_axis</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.argmax.html#numpy.argmax" title="numpy.argmax"><code class="xref py py-obj docutils literal"><span class="pre">argmax</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.argmin.html#numpy.argmin" title="numpy.argmin"><code class="xref py py-obj docutils literal"><span class="pre">argmin</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.argsort.html#numpy.argsort" title="numpy.argsort"><code class="xref py py-obj docutils literal"><span class="pre">argsort</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.average.html#numpy.average" title="numpy.average"><code class="xref py py-obj docutils literal"><span class="pre">average</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.bincount.html#numpy.bincount" title="numpy.bincount"><code class="xref py py-obj docutils literal"><span class="pre">bincount</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.ceil.html#numpy.ceil" title="numpy.ceil"><code class="xref py py-obj docutils literal"><span class="pre">ceil</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.clip.html#numpy.clip" title="numpy.clip"><code class="xref py py-obj docutils literal"><span class="pre">clip</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.conj.html#numpy.conj" title="numpy.conj"><code class="xref py py-obj docutils literal"><span class="pre">conj</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.corrcoef.html#numpy.corrcoef" title="numpy.corrcoef"><code class="xref py py-obj docutils literal"><span class="pre">corrcoef</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.cov.html#numpy.cov" title="numpy.cov"><code class="xref py py-obj docutils literal"><span class="pre">cov</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.cross.html#numpy.cross" title="numpy.cross">
<code class="xref py py-obj docutils literal"><span class="pre">cross</span></code></a><a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.cumprod.html#numpy.cumprod" title="numpy.cumprod"><code class="xref py py-obj docutils literal"><span class="pre">cumprod</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.cumsum.html#numpy.cumsum" title="numpy.cumsum"><code class="xref py py-obj docutils literal"><span class="pre">cumsum</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.diff.html#numpy.diff" title="numpy.diff"><code class="xref py py-obj docutils literal"><span class="pre">diff</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.dot.html#numpy.dot" title="numpy.dot"><code class="xref py py-obj docutils literal"><span class="pre">dot</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.floor.html#numpy.floor" title="numpy.floor"><code class="xref py py-obj docutils literal"><span class="pre">floor</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.inner.html#numpy.inner" title="numpy.inner"><code class="xref py py-obj docutils literal"><span class="pre">inner</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.lexsort.html#numpy.lexsort" title="numpy.lexsort"><code class="xref py py-obj docutils literal"><span class="pre">lexsort</span></code></a>,<a class="reference external" href="https://docs.python.org/dev/library/functions.html#max" title="(in Python v3.7)"><code class="xref py py-obj docutils literal"><span class="pre">max</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.maximum.html#numpy.maximum" title="numpy.maximum"><code class="xref py py-obj docutils literal"><span class="pre">maximum</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.mean.html#numpy.mean" title="numpy.mean"><code class="xref py py-obj docutils literal"><span class="pre">mean</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.median.html#numpy.median" title="numpy.median"><code class="xref py py-obj docutils literal"><span class="pre">median</span></code></a>,<a class="reference external" href="https://docs.python.org/dev/library/functions.html#min" title="(in Python v3.7)"><code class="xref py py-obj docutils literal"><span class="pre">min</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.minimum.html#numpy.minimum" title="numpy.minimum"><code class="xref py py-obj docutils literal"><span class="pre">minimum</span>
</code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.nonzero.html#numpy.nonzero" title="numpy.nonzero"><code class="xref py py-obj docutils literal"><span class="pre">nonzero</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.outer.html#numpy.outer" title="numpy.outer"><code class="xref py py-obj docutils literal"><span class="pre">outer</span></code></a>,<a class="reference external" href="https://docs.python.org/dev/library/re.html#module-re" title="(in Python v3.7)"><code class="xref py py-obj docutils literal"><span class="pre">re</span></code></a>,<a class="reference external" href="https://docs.python.org/dev/library/functions.html#round" title="(in Python v3.7)"><code class="xref py py-obj docutils literal"><span class="pre">round</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.sort.html#numpy.sort" title="numpy.sort"><code class="xref py py-obj docutils literal"><span class="pre">sort</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.std.html#numpy.std" title="numpy.std"><code class="xref py py-obj docutils literal"><span class="pre">std</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.sum.html#numpy.sum" title="numpy.sum"><code class="xref py py-obj docutils literal"><span class="pre">sum</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.trace.html#numpy.trace" title="numpy.trace"><code class="xref py py-obj docutils literal"><span class="pre">trace</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.transpose.html#numpy.transpose" title="numpy.transpose"><code class="xref py py-obj docutils literal"><span class="pre">transpose</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.var.html#numpy.var" title="numpy.var"><code class="xref py py-obj docutils literal"><span class="pre">var</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.vdot.html#numpy.vdot" title="numpy.vdot"><code class="xref py py-obj docutils literal"><span class="pre">vdot</span></code></a><a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.vectorize.html#numpy.vectorize" title="numpy.vectorize"><code class="xref py py-obj docutils literal"><span class="pre">vectorize</span></code></a>,<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.where.html#numpy.where" title="numpy.where"><code class="xref py py-obj docutils literal"><span class="pre">where</span></code></a>

```python
np.add(array1,10) # add a value to each element
```
    array([[10, 11, 12],
           [13, 14, 15],
           [16, 17, 18]])




```python
np.subtract(array1,10) # substract a value to each element 
```




    array([[-10,  -9,  -8],
           [ -7,  -6,  -5],
           [ -4,  -3,  -2]])




```python
np.multiply(array1,100) # multiply a value to each element
```




    array([[  0, 100, 200],
           [300, 400, 500],
           [600, 700, 800]])




```python
np.divide(array1, 2) # divide a value to each element
```




    array([[0. , 0.5, 1. ],
           [1.5, 2. , 2.5],
           [3. , 3.5, 4. ]])




```python
np.mean(array1) # computing the Numpy table average using the mean() function
```




    4.0




```python
array1.mean()  #  computing the Numpy table average using the mean() method
```




    4.0




```python
array1.min()  #  computing the Numpy table mimimum using the min() method
```




    0




```python
array1.max()  # computing the Numpy table maximum using the max() method
```




    8




```python
np.mean(array1, axis=0)  # we apply mean() function only over columns 
```




    array([3., 4., 5.])




```python
np.mean(array1, axis=1) # we apply mean() function only over rows 
```




    array([1., 4., 7.])



- Operations between several tables


```python
(array1 +1) * array2     # multiplication of 2 tables
```




    array([[ 47,  40, 147],
           [160,  75,  42],
           [ 28, 280, 126]])




```python
array1 + array2 # sum of 2 tables
```




    array([[47, 21, 51],
           [43, 19, 12],
           [10, 42, 22]])




```python
np.dot(array1, array2) # dot product of 2 tables
```




    array([[ 48,  85,  35],
           [321, 295, 245],
           [594, 505, 455]])



## 6.4 Update Numpy array: 

Other interesting features include concatenation, splitting, transposition (changing elements from one row to another and vice versa) and obtaining elements diagonally.

### a) - To manipulate / modify the dimensions of a Numpy array:

The dimension of a table is given by the number of elements following each axis. We have specific methods and attributes specific to ndarray ():

<table border="1" class="docutils">
<colgroup>
<col width="27%">
<col width="57%">
</colgroup>
<tbody valign="top">

<tr><td><tt class="docutils literal"><span class="pre">ndim</span></tt></td>
<td>Tool to know Numpy array dimension</td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre">shape</span></tt></td>
<td>Tool to know Numpy array shape </td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre">dtype</span></tt></td>
<td>Tool to know Numpy array type </td>
</tr>
<tr><td><tt class="docutils literal"><span class="pre">size</span></tt></td>
<td>Tool to know Numpy array size</td>
</tr>

</tbody>
</table>





```python
np.floor(10*np.random.random((3,4)))
```




    array([[1., 5., 5., 0.],
           [5., 5., 4., 4.],
           [6., 2., 5., 2.]])




```python
a = np.floor(10*np.random.random((3,4)))
print(a, a.shape, a.ndim)
```

    [[3. 5. 5. 6.]
     [0. 7. 1. 6.]
     [4. 8. 2. 5.]] (3, 4) 2
    

Depending on our programming needs, we can change the size of a table.


```python
a.ravel() # ravel() function to write over table on 1 dimension (flattened)
```




    array([3., 5., 5., 6., 0., 7., 1., 6., 4., 8., 2., 5.])




```python
a.reshape(6,2)  # reshape() function to change the dimension of our array
```




    array([[3., 5.],
           [5., 6.],
           [0., 7.],
           [1., 6.],
           [4., 8.],
           [2., 5.]])




```python
a.T  #T method to calculate the transpose of our array.
```




    array([[3., 0., 4.],
           [5., 7., 8.],
           [5., 1., 2.],
           [6., 6., 5.]])




```python
print(a.T.shape, a.shape)
```

    (4, 3) (3, 4)
    

The reshape function returns its argument with a modified form, while the ndarray.resize method modifies the array itself:


```python
a.resize((2,6))
a
```




    array([[3., 5., 5., 6., 0., 7.],
           [1., 6., 4., 8., 2., 5.]])



If a dimension is set to -1 in a resizing operation, the other dimensions are automatically calculated:


```python
a.reshape(4,-1)
```




    array([[3., 5., 5.],
           [6., 0., 7.],
           [1., 6., 4.],
           [8., 2., 5.]])



### b) - Working with a subset of a Numpy table:


```python
my_table = np.array([[1,2,3], [4,5,6], [7,8,9]])
my_table
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



We will select a subset of our ndarray with selecting the first row.


```python
subset = my_table[0]
subset
```




    array([1, 2, 3])



We want to change the first element of our subset. 


```python
subset[0] = 100
subset
```




    array([100,   2,   3])



But by modifying our sub-table, we realize that we have modified our initial table.


```python
my_table
```




    array([[100,   2,   3],
           [  4,   5,   6],
           [  7,   8,   9]])



A modification of the subset causes a modification of the initial table.
Our subset array is a view of our initial table. Reason: saving memory when working with large volumes of data.

If you really want to work with a subset without modifying the original array, you must make a copy with the <b> copy () </ b> function.



```python
my_table = np.array([[1,2,3], [4,5,6], [7,8,9]])
subset = my_table[0].copy()
subset[0]=101
```


```python
subset
```




    array([101,   2,   3])




```python
my_table
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



   ### c)- To concatenate Numpy array:
    
<a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.vstack.html#numpy.vstack" title="numpy.vstack"><code class="xref py py-obj docutils literal"><span class="pre">vstack</span></code></a>, <a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.column_stack.html#numpy.column_stack" title="numpy.column_stack"><code class="xref py py-obj docutils literal"><span class="pre">column_stack</span></code></a>, <a class="reference internal" href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.concatenate.html#numpy.concatenate" title="numpy.concatenate"><code class="xref py py-obj docutils literal"><span class="pre">concatenate</span></code></a>

-  <b>concatenate()</b> function to join a sequence of arrays along an existing axis.

 Concatenate function can take two or more arrays of the same shape and by default it concatenates row-wise i.e. axis=0. 


```python
array1=np.array([[1,2,3],[4,5,6],[7,8,9]])
array1
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
array2=np.array([[2,5,6],[9,10,11],[5,6,9]])
array2
```




    array([[ 2,  5,  6],
           [ 9, 10, 11],
           [ 5,  6,  9]])




```python
np.concatenate([array1,array2], axis=0)   # to join a sequence of arrays along rows  (axis = 0) 
```




    array([[ 1,  2,  3],
           [ 4,  5,  6],
           [ 7,  8,  9],
           [ 2,  5,  6],
           [ 9, 10, 11],
           [ 5,  6,  9]])




```python
np.concatenate([array1,array2], axis=1)    # to join a sequence of arrays along columns  (axis = 1) 
```




    array([[ 1,  2,  3,  2,  5,  6],
           [ 4,  5,  6,  9, 10, 11],
           [ 7,  8,  9,  5,  6,  9]])



In addition to the concatenate function, NumPy also offers two convenient functions hstack and vstack to stack/combine arrays horizontally or vertically.

 
- <b>vstack()</b> function stacks arrays in sequence vertically i.e. row wise. And the result is the same as using concatenate with axis=0.
- <b>hstack()</b> function stacks arrays horizontally i.e. column wise. And the result is the same as using concatenate with axis=1.


```python
array3=np.array([10,20,30]) # 1D Numpy array
```


```python
array3
```




    array([10, 20, 30])




```python
array4=np.array([[1,2,3],[4,5,6],[7,8,9]]) # bi-dimentionnal Numpy array
```


```python
array4
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
np.vstack([array4,array3])    
```




    array([[ 1,  2,  3],
           [ 4,  5,  6],
           [ 7,  8,  9],
           [10, 20, 30]])




```python
array5=np.array([[10],[20],[30]]) 
array5.shape
```




    (3, 1)




```python
np.hstack([array4,array5]) 
```




    array([[ 1,  2,  3, 10],
           [ 4,  5,  6, 20],
           [ 7,  8,  9, 30]])



 ### d)- To split Numpy arrays:

This is the opposite of concatenation.
We have the split (), hsplit () and vsplit () functions.


```python
array=np.array([15,16,17,12,49,52,12,14,36]) 
```


```python
len(array) # array size
```




    9




```python
np.split(array,3) # we split the array into 3 arrays
```




    [array([15, 16, 17]), array([12, 49, 52]), array([12, 14, 36])]



We can split our numpy array using breaking point with index. 


```python
np.split(array,[2,6]) # we want to cut our table into 3 tables, the numbers between [] are the breakpoints.
                      # corresponds to the indexes where we cut
```




    [array([15, 16]), array([17, 12, 49, 52]), array([12, 14, 36])]




```python
array1,array2,array3=np.split(array,[2,6]) 
```


```python
print(array1,array2,array3)
```

    [15 16] [17 12 49 52] [12 14 36]
    


```python
array1,array2,array3,array4=np.split(array,[2,4,6]) 
```


```python
print(array1,array2,array3,array4)
```

    [15 16] [17 12] [49 52] [12 14 36]
    

To break 2-dimensional tables. we use hsplit or vsplit. 


```python
array2=np.array([[1,2,3],[4,5,6],[7,8,9]])
array2
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
array1,array1bis=np.vsplit(array2, [2]) 
print(array1,array1bis)
```

    [[1 2 3]
     [4 5 6]] [[7 8 9]]
    


```python
array2
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
array1,array1bis=np.hsplit(array2,[2]) 
print(array1,array1bis)
```

    [[1 2]
     [4 5]
     [7 8]] [[3]
     [6]
     [9]]
    

###  e)- To delete rows and  columns in a Numpy array: <b>delete()</b> function 


```python
array=np.array([[1,2,3],[4,5,6],[7,8,9]])
array
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
np.delete(array,2,axis=0) # to delete row with index 2 
```




    array([[1, 2, 3],
           [4, 5, 6]])




```python
np.delete(array2,2,axis=1)  # to delete column with index 2 
```




    array([[1, 2],
           [4, 5],
           [7, 8]])



### f)- To calculate the transpose of a Numpy table: <b>transpose()</b> function


```python
np.transpose(array)
```




    array([[1, 4, 7],
           [2, 5, 8],
           [3, 6, 9]])



### g)- To get the values of the diagonal of a Numpy table: <b>diagonal()</b> function


```python
array.diagonal() 
```




    array([1, 5, 9])



## 6.5 Comparisons and masks :

With Numpy arrays, you can use a boolean matrix to filter and compare Numpy arrays.


```python
table = np.random.randint(100,size=(6,6))  #  4*3 Numpy array with random values between 0 and 100 
table
```




    array([[62, 72, 26, 37, 76, 39],
           [38, 66, 42, 78, 15, 97],
           [81, 19, 83, 89, 87, 66],
           [11, 49, 53, 71, 63, 25],
           [75, 87, 68, 88, 30, 12],
           [95, 61, 14, 40, 61, 31]])




```python
mask = table>50 # we generate here a mask with same dimension than our original table but with Boolean values
mask
```




    array([[ True,  True, False, False,  True, False],
           [False,  True, False,  True, False,  True],
           [ True, False,  True,  True,  True,  True],
           [False, False,  True,  True,  True, False],
           [ True,  True,  True,  True, False, False],
           [ True,  True, False, False,  True, False]])



Being both of the same size, we can use this Boolean matrix to our advantage. In other words, we can do Boolean masking. With this Boolean matrix as a mask, we can use it to select the particular subset of data that interests us.


```python
table[mask] 
#table[table>50]  # same job
```




    array([62, 72, 76, 66, 78, 97, 81, 83, 89, 87, 66, 53, 71, 63, 75, 87, 68,
           88, 95, 61, 61])




```python
table[table>50]
```




    array([62, 72, 76, 66, 78, 97, 81, 83, 89, 87, 66, 53, 71, 63, 75, 87, 68,
           88, 95, 61, 61])



We have many other comparison operators to compare two arrays such as == (equality),! = (No equality), <= (less than or equal to). We can even combine two Boolean statements & (for "AND" conditions) or | (for the "OR" conditions).


```python
#table[table>=50]                 
#table[table<50]                     
#table[table!=50]                    
#table[table==50]                     
#table[(table >=50) & (table <=70)]  
table[(table>=50) | (table<=40)]     
```




    array([62, 72, 26, 37, 76, 39, 38, 66, 78, 15, 97, 81, 19, 83, 89, 87, 66,
           11, 53, 71, 63, 25, 75, 87, 68, 88, 30, 12, 95, 61, 14, 40, 61, 31])



## Exercise using Numpy library:
### we will work on data station using Numpy library.

- read the file containing the daily precipitation and temperature data for the Ottawa station for the year 2017

1- Create a Numpy table with a column for temperature and a column for precipitation. (With two Numpy 1D tables, create a 2D array (365 rows and 2 columns).

2- Convert the temperature data into Celcius (T [Celcius] = T [Kelvin] - 273.15).

3- How many days have an accumulation greater than 25mm?

4- What temperature was recorded for the day with the greatest accumulation?

5- Calculate the number of degree days (> 0degC) for the year 2017.

6- Calculate the daily precipitation totals for the year 2017 and assign this variable to the cumul_recipitation table. Add the cumul_recipitation table to the table.

7- Just for the exercise, split the array into 2 arrays, then concatenate them again to get the initial array.



```python
import numpy as np
# to read a csv file with numpy, we can use genfromtxt() function. 
temperature = np.genfromtxt("./DATA/OTTAWA_tasmoy_2017.csv", dtype=float)
precipitation = np.genfromtxt("./DATA/OTTAWA_PrecTOT_2017.csv", dtype=float)
```


```python
print(temperature.shape, precipitation.shape)
```

    (365,) (365,)
    



### Correction


```python
#1- 

tableau = np.column_stack([temperature,precipitation])
```


```python
#tableau = np.hstack([temperature,precipitation])
tableau = np.hstack([temperature.reshape(len(temperature),-1),precipitation.reshape(len(precipitation),-1)])
```

`
```python
print(tableau.shape)
```
    (365, 2)
    
```python
#2- 
tableau[:,0]=tableau[:,0]-273.15  
``

```python
len(tableau[tableau[:,1]>=25])   
```

    10

```python
# 4- 
precipitation_max = np.nanmax(tableau[:,1]) 
print(precipitation_max)
```

    45.01
    


```python
tableau[tableau[:,1] == precipitation_max] 
```

    array([[15.8 , 45.01]])




```python
# 5- 
```


```python
sum(tableau[:,1][tableau[:,1]>0])
```




    1328.5300000000002




```python
# 6- 
cumul_precipitation = np.nancumsum(tableau[:,1])
```


```python
# 
tableau = np.column_stack([tableau, cumul_precipitation])
```




    array([[-6.50000e+00,  1.10000e-01,  1.10000e-01],
           [-6.80000e+00,  3.03000e+00,  3.14000e+00],
           [-1.80000e+00,  2.65700e+01,  2.97100e+01],
           ...,
           [         nan,  0.00000e+00,  1.32726e+03],
           [-2.15000e+01,  1.27000e+00,  1.32853e+03],
           [-2.20000e+01,  0.00000e+00,  1.32853e+03]])


```python
# 7. 

temperature2,precipitation2,cumul2 = np.hsplit(tableau, 3)
```


```python
tableau_original=np.concatenate([temperature2+273.15, precipitation2], axis = 1)
```
```python
print(tableau_original)
```