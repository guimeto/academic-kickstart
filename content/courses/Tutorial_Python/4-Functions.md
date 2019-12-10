---
title: 4 Functions
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



# 4  Libraries and functions in  Python


## 4.1 Introduction to librairies

To facilitate the processing, manipulation and visualization of data, Python has many libraries.

Python libraries allow you to import codes and functions that will make our analysis easier.

Here are the most popular libraries:

- numpy: mathematics or scientific calculations: http://www.numpy.org/
- pandas: data manipulation: http://pandas.pydata.org/
- matplotlib: visualization of data: https://matplotlib.org/
- scikit-learn: machine learning: https://scikit-learn.org
- Datetime: formatting dates: https: //docs.python.org/2/library/datetime.html


To import a library under Python, use the function: <b> import </b> + library_name

```python
# To import a library
import numpy
```
Every library imported under python has help.

To know what a library contains, we use the function: dir ()
 
        - Example: dir(numpy)    
        
```python
dir(numpy)
```
 The <b> help () </b> function provides help with a function in the library

        - Example: help(numpy.mean)


```python
help(numpy.mean)
```

    Help on function mean in module numpy:
    
    mean(a, axis=None, dtype=None, out=None, keepdims=<no value>)
        Compute the arithmetic mean along the specified axis.
        
        Returns the average of the array elements.  The average is taken over
        the flattened array by default, otherwise over the specified axis.
        `float64` intermediate and return values are used for integer inputs.
        
        Parameters
        ----------
        a : array_like
            Array containing numbers whose mean is desired. If `a` is not an
            array, a conversion is attempted.
        axis : None or int or tuple of ints, optional
            Axis or axes along which the means are computed. The default is to
            compute the mean of the flattened array.
        
            .. versionadded:: 1.7.0
        
            If this is a tuple of ints, a mean is performed over multiple axes,
            instead of a single axis or all the axes as before.
        dtype : data-type, optional
            Type to use in computing the mean.  For integer inputs, the default
            is `float64`; for floating point inputs, it is the same as the
            input dtype.
        out : ndarray, optional
            Alternate output array in which to place the result.  The default
            is ``None``; if provided, it must have the same shape as the
            expected output, but the type will be cast if necessary.
            See `doc.ufuncs` for details.
        
        keepdims : bool, optional
            If this is set to True, the axes which are reduced are left
            in the result as dimensions with size one. With this option,
            the result will broadcast correctly against the input array.
        
            If the default value is passed, then `keepdims` will not be
            passed through to the `mean` method of sub-classes of
            `ndarray`, however any non-default value will be.  If the
            sub-class' method does not implement `keepdims` any
            exceptions will be raised.
        
        Returns
        -------
        m : ndarray, see dtype parameter above
            If `out=None`, returns a new array containing the mean values,
            otherwise a reference to the output array is returned.
        
        See Also
        --------
        average : Weighted average
        std, var, nanmean, nanstd, nanvar
        
        Notes
        -----
        The arithmetic mean is the sum of the elements along the axis divided
        by the number of elements.
        
        Note that for floating-point input, the mean is computed using the
        same precision the input has.  Depending on the input data, this can
        cause the results to be inaccurate, especially for `float32` (see
        example below).  Specifying a higher-precision accumulator using the
        `dtype` keyword can alleviate this issue.
        
        By default, `float16` results are computed using `float32` intermediates
        for extra precision.
        
        Examples
        --------
        >>> a = np.array([[1, 2], [3, 4]])
        >>> np.mean(a)
        2.5
        >>> np.mean(a, axis=0)
        array([ 2.,  3.])
        >>> np.mean(a, axis=1)
        array([ 1.5,  3.5])
        
        In single precision, `mean` can be inaccurate:
        
        >>> a = np.zeros((2, 512*512), dtype=np.float32)
        >>> a[0, :] = 1.0
        >>> a[1, :] = 0.1
        >>> np.mean(a)
        0.54999924
        
        Computing the mean in float64 is more accurate:
        
        >>> np.mean(a, dtype=np.float64)
        0.55000000074505806
    
    
```python
list_1=[1,2,3,4,5,6,7,8,9,10]
list_1
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```python
numpy.mean(list_1)  # name of library + name of function 
```

    5.5




```python
numpy.max(list_1)
```




    10



## 4.2  Built-in function

Python gives you many built-in functions like print(), etc 

Here's a list: https://docs.python.org/3/library/functions.html

### Some examples: 

```python
abs(-1)  # Return the absolute value of a number 
```

    1

```python
len([1,2,3]) # Return the length (the number of items) of an object. 
```
    3


```python
max([1,3,2,6,99,1])    #Return max value from a list
```




    99




```python
round(1.2)  # Return number rounded to ndigits precision 
```




    1



## 4.3  Create own functions.

These functions are called user-defined functions.

- a function makes our code more fluid and readable:

- Syntax: to write a function, we start with the def() keyword

                   def sum (a, b): # we define the parameters
       indentation ---> return a + b # return keyword to return result variable
                
 - It does not specify the type of return, it is dynamically resolved at the time of execution of the program.
 
 - Call of the function: result = sum (12,4) # result = 16
 
 
 Python also supports keyword arguments.
 
                    def sum (a, b): # we define the parameters
                        return a + b # return keyword to return result variable
                    result = sum (12, b = 4)
                -----------------------------
                    def sum (a, b = 4): # we define the parameters
                          return a + b # return keyword to return result variable
                    result = sum (12)
                    
                                      


```python
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0:
        return 'negative'
    else:
        return 'zero'
```


```python
my_list_to_test = [0,2,-8,10,1,-6]
```


```python
for element in my_list_to_test:
    print(sign(element))
```

    zero
    positive
    negative
    positive
    positive
    negative
    

We will often define functions to take optional keyword arguments, like this:


```python
def hello(name, loud=False):
    if loud:
        print('HELLO, %s' % name.upper())
    else:
        print('Hello, %s!' % name)

hello('Bob')
hello('Fred', loud=True)
```

    Hello, Bob!
    HELLO, FRED
    

## 4.4  Functions with *args

- Special syntax in python that allows to manage a variable number of parameters when calling a function
- It's the * that counts
- args is a convention
- * args is a list of parameters containing the parameters of a function

Syntax * args:
            
            def print_ingredients (* args):
                for ingredients in args:
                    print (ingredient)
                    
            print_ingredients ( 'Tomatoes')
            print_ingredients ( 'Tomatoes' Banana)
            print_ingredients ( 'Tomatoes' Banana, apple)


```python
def sum(*args):
    total = 0 
    for number in args: 
        total += number 
    print(total)
```


```python
sum(2,3)
sum(2,3,10,90,23)
```

    5
    128
    

## 4.5 Functions with **kwargs

- Like * args, but for keyword arguments
- It's the * that counts
- ** kwargs is a python dictionary containing the keys / values ​​of the parameters of a function
- it must always be present last in the list of parameters of a function

Syntax ** kwargs:
            
            def print_languages ​​(** args):
                for language, definition in kwargs.items ():
                    print ('{} is {}'. format (language, definition))
                    
            print_languages ​​(Python = 'awesome')
            print_languages ​​(Python = 'awesome', Java = 'verbose')


```python
def capitals(**kwargs):
    for country, capital in kwargs.items():
        print("The capital of {} in {}".format(country, capital))
```


```python
capitals(France = 'Paris', Germany='Berlin')
```

    The capital of France in Paris
    The capital of Germany in Berlin
    


```python
def capitals(title, ending='',  **kwargs):
    print(title)
    for country, capital in kwargs.items():
        print("The capital of {} in {}".format(country, capital))
    if ending:
        print(ending)
```


```python
capitals("List of countries",
    France = 'Paris', Germany='Berlin')
```

    List of countries
    The capital of France in Paris
    The capital of Germany in Berlin
    


```python
keywords = {'france': 'Paris', 'Germany' : 'Allemage'}
capitals("List of countries 2 ", **keywords)
```

    List of countries 2 
    The capital of france in Paris
    The capital of Germany in Allemage
    

## 4.6 Import own functions

Modules refer to a file containing Python statements and definitions.

A file containing Python code, for e.g.: example.py, is called a module and its module name would be example.

We use modules to break down large programs into small manageable and organized files. Furthermore, modules provide reusability of code.

We can define our most used functions in a module and import it, instead of copying their definitions into different programs.

Here, we have defined different funcitons inside a module named my_functions.


We use the import keyword to import our module and then our functions. To import our previously defined module example we type the following in the Python prompt:


```python
import my_functions
```

Using the module name we can access the function using the dot . operator. For example:


```python
my_functions.substraction(4,6)
```




    -2




```python

```
