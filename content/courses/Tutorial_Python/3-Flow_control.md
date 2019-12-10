---
title: 3 Flow control
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
![image0](/img/pylogo.png)
<img src="./figures/pylogo.png" alt="Indentation" width="50%" height="50%">


## 3.1  Flow control with the conditional structure: If, else

The flow control statements can be classified into Conditional Statements and Iteration Statements. 

- The Conditional Statements selects a particular set of statements for execution depending upon a specified condition.
The most popular conditional control statement is ‘if else’, so let’s see how it works in python.:

                                         Syntax IF:
        
                                         if condition:
                                         indentation ---> action 1
                                         elif:
                                         indentation ---> action 2
                                         else:
                                         indentation ---> action 3
         
- WARNING: python works in indentation
![image0](/img/indentation.png)


- Multiple tasks can be assigned in conditional structures.


```python
my_variable = 5
```


```python
if (my_variable > 5 ):
    my_variable = my_variable + 1 
my_variable    
```




    5




```python
if (my_variable > 5 ):
    my_variable = my_variable + 1 
else:
    my_variable = my_variable - 1 
my_variable   

```




    4




```python
if (my_variable > 5 ):
    my_variable = my_variable + 1 
elif (my_variable == 5) :
    my_variable = my_variable * 10 
else:
    my_variable = my_variable - 1 
my_variable   
```




    3



## 3.2 Flow control: Loop for: 

A loop allows to repeat instructions according to your needs.

                             Syntax FOR:
                                         items = [1,2,3]
                                         for i in items:
                                         indentation ---> print (i) # 1,2,3
    
Be careful once again to respect the indentation.



```python
my_list=[1,2,3,4,5,6,7,8,9,10]
```


```python
for value in my_list:
    print(value*2)
    print("---")
```

    2
    ---
    4
    ---
    6
    ---
    8
    ---
    10
    ---
    12
    ---
    14
    ---
    16
    ---
    18
    ---
    20
    ---
    


```python
for value in my_list:
    my_new_value=value*2
    print("The multiplication of 2 * %d = %d" % (value,my_new_value))  # to concatenate text and a variable
                               #% d: python knows we'll display an integer
                               #% s: python knows we'll display a string
                               #% f: python knows we will display a float
                               # we give a tuple to display
```

    The multiplication of 2 * 1 = 2
    The multiplication of 2 * 2 = 4
    The multiplication of 2 * 3 = 6
    The multiplication of 2 * 4 = 8
    The multiplication of 2 * 5 = 10
    The multiplication of 2 * 6 = 12
    The multiplication of 2 * 7 = 14
    The multiplication of 2 * 8 = 16
    The multiplication of 2 * 9 = 18
    The multiplication of 2 * 10 = 20
    

## 3.3 Flow control:  while() loop , same as if structure but repeated 

                            Syntaxe WHILE:
                                           run = True
                                           while run:
                                           indentation ---> print('running')
                                                if <condition>:
                                                   run = False
                                                   
As long as the condition is met, the iteration in the loop continues.
Be careful to respect the indentation.



```python
my_list=[1,2,3,4,5,6,7,8,9,10]
counter=0
while (counter < 10):
    print("My counter = %d" % (counter))
    print("My value = %d" % (my_list[counter]))   # in a tuple, we want the value from our list
    counter=counter+1
```

    My counter = 0
    My value = 1
    My counter = 1
    My value = 2
    My counter = 2
    My value = 3
    My counter = 3
    My value = 4
    My counter = 4
    My value = 5
    My counter = 5
    My value = 6
    My counter = 6
    My value = 7
    My counter = 7
    My value = 8
    My counter = 8
    My value = 9
    My counter = 9
    My value = 10
    


```python
# we can combine several conditions in a while loop
# we will for example extract only the even values
# If modulo value = 0, even number
counter=0
counter_true_result=0
while (counter < 10):
    if my_list[counter] % 2 == 0:
        print("My counter = %d" % (counter))
        print("My value = %d" % (my_list[counter]))  
        counter_true_result=counter_true_result+1
    counter=counter+1
print(counter_true_result)
```

    My counter = 1
    My value = 2
    My counter = 3
    My value = 4
    My counter = 5
    My value = 6
    My counter = 7
    My value = 8
    My counter = 9
    My value = 10
    5
    

## 3.4 Loop  range

It's possible to create a loop with range() function:       


```python
for my_value in range(0,10):
    print(my_value*2)
    print("---")
```

    0
    ---
    2
    ---
    4
    ---
    6
    ---
    8
    ---
    10
    ---
    12
    ---
    14
    ---
    16
    ---
    18
    ---
    

## 3.5 To stop a loop: 

It's possible to stop a loop with break command.  


```python
my_list=[1,2,3,4,5,6,7,8,9,10]
for i in my_list:
     if i > 5:
             print("stop: the following values are greater than 5.")
             break
     print(i)

```

    1
    2
    3
    4
    5
    stop: the following values are greater than 5.
    


```python
# to import a library
import numpy as np
```

```python
dir(np)    
```
  
The <b>help()</b> function provides help on a function of the library.

        - Example: help(numpy.mean)


```python
help (np.median) # for help on a library function
                 # we can distinguish between optional and mandatory arguments
```

    Help on function median in module numpy:
    
    median(a, axis=None, out=None, overwrite_input=False, keepdims=False)
        Compute the median along the specified axis.
        
        Returns the median of the array elements.
        
        Parameters
        ----------
        a : array_like
            Input array or object that can be converted to an array.
        axis : {int, sequence of int, None}, optional
            Axis or axes along which the medians are computed. The default
            is to compute the median along a flattened version of the array.
            A sequence of axes is supported since version 1.9.0.
        out : ndarray, optional
            Alternative output array in which to place the result. It must
            have the same shape and buffer length as the expected output,
            but the type (of the output) will be cast if necessary.
        overwrite_input : bool, optional
           If True, then allow use of memory of input array `a` for
           calculations. The input array will be modified by the call to
           `median`. This will save memory when you do not need to preserve
           the contents of the input array. Treat the input as undefined,
           but it will probably be fully or partially sorted. Default is
           False. If `overwrite_input` is ``True`` and `a` is not already an
           `ndarray`, an error will be raised.
        keepdims : bool, optional
            If this is set to True, the axes which are reduced are left
            in the result as dimensions with size one. With this option,
            the result will broadcast correctly against the original `arr`.
        
            .. versionadded:: 1.9.0
        
        Returns
        -------
        median : ndarray
            A new array holding the result. If the input contains integers
            or floats smaller than ``float64``, then the output data-type is
            ``np.float64``.  Otherwise, the data-type of the output is the
            same as that of the input. If `out` is specified, that array is
            returned instead.
        
        See Also
        --------
        mean, percentile
        
        Notes
        -----
        Given a vector ``V`` of length ``N``, the median of ``V`` is the
        middle value of a sorted copy of ``V``, ``V_sorted`` - i
        e., ``V_sorted[(N-1)/2]``, when ``N`` is odd, and the average of the
        two middle values of ``V_sorted`` when ``N`` is even.
        
        Examples
        --------
        >>> a = np.array([[10, 7, 4], [3, 2, 1]])
        >>> a
        array([[10,  7,  4],
               [ 3,  2,  1]])
        >>> np.median(a)
        3.5
        >>> np.median(a, axis=0)
        array([ 6.5,  4.5,  2.5])
        >>> np.median(a, axis=1)
        array([ 7.,  2.])
        >>> m = np.median(a, axis=0)
        >>> out = np.zeros_like(m)
        >>> np.median(a, axis=0, out=m)
        array([ 6.5,  4.5,  2.5])
        >>> m
        array([ 6.5,  4.5,  2.5])
        >>> b = a.copy()
        >>> np.median(b, axis=1, overwrite_input=True)
        array([ 7.,  2.])
        >>> assert not np.all(a==b)
        >>> b = a.copy()
        >>> np.median(b, axis=None, overwrite_input=True)
        3.5
        >>> assert not np.all(a==b)
    
    

## - Exercise 

## Objective: To manipulate a list containing the prices of 58 houses

Creation of the list "price_of_58_houses"


```python
price_of_58_houses=list(range(125000,700000,10000))   
```


```python
price_of_58_houses[0:20]
```




    [125000,
     135000,
     145000,
     155000,
     165000,
     175000,
     185000,
     195000,
     205000,
     215000,
     225000,
     235000,
     245000,
     255000,
     265000,
     275000,
     285000,
     295000,
     305000,
     315000]




```python
len(price_of_58_houses)
```




    58



    1- How many houses have a price greater than or equal to 300000 euros?

    2- How many houses have a price between 250000 and 400000 euros?

    3- How many houses have a price that is not higher than 600000 euros?

    4- How many houses have a price lower than 150000 euros or more than 650000 euros?
    
Hint: Scroll through the list with a loop, use if condition statements, and a counter to count the true results.


```python

```


```python

```


```python
# 1. 
nombre_maisons=0
for prix in price_of_58_houses:    
    if prix >= 300000:             
        nombre_maisons=nombre_maisons+1
print("Number of house with price greater than or equal to 300000 euros : %d" % (nombre_maisons))
```

    Number of house with price greater than or equal to 300000 euros : 40
    


```python
# 2. 

nombre_maisons=0
for prix in price_of_58_houses:   
    if (prix >= 250000) and (prix <= 400000):  compteur
        nombre_maisons=nombre_maisons+1
print("The result is : %d" % (nombre_maisons))
```
    The result is : 15
    


```python
# 3.
nombre_maisons=0
for prix in price_of_58_houses:
    if not(prix > 600000):
        nombre_maisons=nombre_maisons+1
print("The result is : %d" % (nombre_maisons))
```

    The result is : 48
    


```python
# 4. 
nombre_maisons=0
for prix in price_of_58_houses:
    if (prix < 150000) or (prix > 650000):
        nombre_maisons=nombre_maisons+1
print("The result is : : %d" % (nombre_maisons))
```

   The result is : 8
    