---
title: 2 List in Python
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 2
---
![image0](/img/pylogo.png)
<img src="./figures/pylogo.png" alt="Indentation" width="50%" height="50%">


Python includes several built-in container types, but the most common ones are lists and tuples, which we would see in this tutorial.

There are certain things you can do with all container types. These operations include indexing, slicing, adding, multiplying. In addition, Python has built-in functions like finding the length of a sequence, finding its largest and smallest elements...

Each element of a sequence is assigned by a number - its position or index. The first index is zero, the second index is one...

Creating a list is as simple as putting different comma-separated values between square brackets : 

 - list1 = [ a, b, c, d, e]
 - list2 = [ 1, 2, 3, 4, 5]
 
Python is an object-oriented language, lists are associated with methods: object.method()
Functions can be applied to lists. 

## 2.1 Create a list
To create a list, we use comma-separated values between square brackets.

```python
my_list = [1,2,3,4,5,6,7,8,"hello",10.5]
```


```python
print(my_list)  # fonction to print elements in list 
```

    [1, 2, 3, 4, 5, 6, 7, 8, 'hello', 10.5]
    

We can use <b>range()</b> function to generate a sequence of numbers over time.

```python
my_list = list(range(10))
my_list
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
my_list = list(range(1981,2011,2))
my_list
```
    [1981,
     1983,
     1985,
     1987,
     1989,
     1991,
     1993,
     1995,
     1997,
     1999,
     2001,
     2003,
     2005,
     2007,
     2009]

When we work with Python object, dir() command always shows us the tasks we can do with this object: dir(my_list)

```python
dir(my_list)
```

    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__delitem__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__gt__',
     '__hash__',
     '__iadd__',
     '__imul__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__reversed__',
     '__rmul__',
     '__setattr__',
     '__setitem__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'append',
     'clear',
     'copy',
     'count',
     'extend',
     'index',
     'insert',
     'pop',
     'remove',
     'reverse',
     'sort']

## 2.2 Accessing Values in Lists : 

To access values in a list, use the square brackets for slicing along with the index or indices to obtain value available at that index.

The first index is zero, the second index is one... to read first element, we use index 0. Then to read last element, we use -1 index. 

It is also possible to modify a value with its index.


```python
my_list = [1,2,3,4,5,6,7,8,"hello",10.5]
my_list[:]  # To use all elements
```




    [1, 2, 3, 4, 5, 6, 7, 8, 'hello', 10.5]




```python
my_list[1] # to access an item from the list: here we access the second element. 
```




    2




```python
my_list[2:4] # slicing:  to access the elements between the 3rd position and the 4th

```




    [3, 4]




```python
my_list[:4] # slicing: to access all elements up to index 4 or 4th position
```




    [1, 2, 3, 4]




```python
my_list[3:] # slicing: to access all elements from index 3
```




    [4, 5, 6, 7, 8, 'hello', 10.5]




```python
my_list[-2] # to get the 2nd value from the end, with use negative indexes, we do not start from 0 anymore.

```




    'hello'




```python
my_list[1:-4] # we start from the index 1, with slicing, we stop at the 4th index from the end
```




    [2, 3, 4, 5, 6]




```python
my_list[::2] # to extract the elements with an increment
```




    [1, 3, 5, 7, 'hello']




```python
my_list[1::2] # to extract the elements with an increment
```




    [2, 4, 6, 8, 10.5]



## 2.3 Updating Lists

https://docs.python.org/2/tutorial/datastructures.html#more-on-lists

### 2.3.1 Add elements
To <b>add</b> an element: we use <b>.append()</b> method

```python
my_list = [1,2,3,4,5,6,7,8,"hello",10.5]
my_list
```




    [1, 2, 3, 4, 5, 6, 7, 8, 'hello', 10.5]




```python
my_list.append(2)
```


```python
print(my_list)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 'hello', 10.5, 2]
    


```python
my_list
```




    [1, 2, 3, 4, 5, 6, 7, 8, 'hello', 10.5, 2]



### 2.3.2 Insert elements

To <b>insert</b> an element to our list using index: <b>insert()</b> method


```python
my_list.insert(5,"new")
```


```python
print(my_list)
```

    [1, 2, 3, 4, 5, 'new', 6, 7, 8, 'hello', 10.5, 2]
    

### 2.3.3 Update elements

To <b>change</b> an element in our list using index


```python
my_list[0]="a"
```


```python
print(my_list)
```

    ['a', 2, 3, 4, 5, 'new', 6, 7, 8, 'hello', 10.5, 2]
    

To <b>change</b> several elements in our list: slicing


```python
my_list[3:5]=[8,10,11,22]
```


```python
print(my_list)
```

    ['a', 2, 3, 8, 10, 11, 22, 'new', 6, 7, 8, 'hello', 10.5, 2]
    

### 2.3.4 Remove elements

To <b>remove</b> in our list: 2 methods 


```python
my_list[0:2]=[]  # remove using slicing 
print(my_list)
```

    [3, 8, 10, 11, 22, 'new', 6, 7, 8, 'hello', 10.5, 2]
    


```python
my_list
```




    [3, 8, 10, 11, 22, 'new', 6, 7, 8, 'hello', 10.5, 2]




```python
del my_list[3] # to remove using keywords
```


```python
print(my_list)
```

    [3, 8, 10, 22, 'new', 6, 7, 8, 'hello', 10.5, 2]
    

https://www.programiz.com/python-programming/keyword-list

## 2.4  Some useful operations on lists

- Concatenate two lists

```python
my_list1=[1,2,3,4,5]
```

```python
my_list2=[6,7,8,9,10]
```
```python
my_list3=my_list1+my_list2
```
```python
my_list3
```
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

- Duplicate a list


```python
my_list1=[1,2,3,4,5]
my_list1*3
```




    [1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5]



-  Reverse elements in list

<b>.reverse()</b> method is used to reverse elements in list


```python
my_list1=[1,2,3,4,5]
print(my_list1)
my_list1.reverse()
print(my_list1)
```

    [1, 2, 3, 4, 5]
    [5, 4, 3, 2, 1]
    

- Count elements in list

<b>.count()</b> method is used to return count of how many times obj occurs in list.


```python
my_list2= ["a","a","a","b","c","c"]
my_list2.count("a")
```




    3




- <b>.index()</b> method returns the lowest index in list that obj appears


```python
my_list2=["a","a","a","b","c","c"]
my_list2.index("c")
```




    4



- function <b>sum()</b>


```python
my_list1=[1,2,3,4,5]
sum(my_list1)
```




    15



- function <b>.len()</b> gives the total length of the list.


```python
len(my_list1)
```




    5



- <b>.sort()</b> function to sort objects of list


```python
my_list = [90,3,8,4,1,10,25,99]
my_list.sort() 
```


```python
my_list
```




    [1, 3, 4, 8, 10, 25, 90, 99]




```python
my_list = [90,3,8,4,1,10,25,99]
my_list
```




    [90, 3, 8, 4, 1, 10, 25, 99]




```python
my_list.sort()
```


```python
my_list.reverse()
```


```python
my_list
```




    [99, 90, 25, 10, 8, 4, 3, 1]



- <b>min()</b> and <b>max()</b> functions to return the <b>minimum</b> and the <b>maximum</b> from list


```python
my_list
```




    [99, 90, 25, 10, 8, 4, 3, 1]




```python
min(my_list)
```




    1




```python
max(my_list)
```




    99



- example applying a loop <b>for</b> and <b>print()</b> function to return values from a list


```python
list_month = ["jan","feb","mar"]
for month in list_month:
    print(month)
```

    jan
    feb
    mar
    

- <b>enumerate()</b> function to return values and index


```python
list_month = ["jan","feb","mar"]
for month in enumerate(list_month):
     print(month)
```

    (0, 'jan')
    (1, 'feb')
    (2, 'mar')
    

- <b>.split()</b> method to transform string into list 


```python
my_string = "January-February-March"
my_string.split("-")
```




    ['January', 'February', 'March']



- <b>.join()</b> method to transform list into string


```python
list1 = ['January', 'February', 'March']
":".join(list1)
```




    'January:February:March'



## 2.5 Loop over lists

You can loop over the elements of a list like this:


```python
list1 = ['January', 'February', 'March']
```


```python
for month in list1:
    print(month)
```

    January
    February
    March
    

If you want access to the index of each element within the body of a loop, use the built-in enumerate function:


```python
list1 = ['January', 'February', 'March']
for idx, month in enumerate(list1):
    print('#%d: %s' % (idx + 1, month))
```

    #1: January
    #2: February
    #3: March
    

## 2.6 List comprehensions

When programming, frequently we want to transform one type of data into another. As a simple example, consider the following code that computes square numbers:


```python
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print(squares)
```

    [0, 1, 4, 9, 16]
    

But, with You can make this code simpler using a list comprehension:


```python
nums = [0, 1, 2, 3, 4]
squares = [x ** 2 for x in nums]
print(squares)
```

    [0, 1, 4, 9, 16]
    

List comprehensions can also contain conditions:


```python
nums = [0, 1, 2, 3, 4]
even_squares = [x ** 2 for x in nums if x % 2 == 0]
print(even_squares)
```

    [0, 4, 16]
    

## 2.7 Tuples


- 1 tuple is a list, a set of stored values, but with the difference that a tuple can not be modified as in a list.

- the interest of a tuple is what is stored in a tuple will never be modifiable

- We write all the elements of a tuple by separating them with commas and all surrounded by parentheses:
             - my_tuple = (,,,,)
             
We will use a tuple to define some kinds of constants that are not intended to change


```python
tuple1=(1,2,3,4,5)
```


```python
tuple1
```




    (1, 2, 3, 4, 5)




```python
tuple1[0]=0 # we can't change a tuple
```
    ---------------------------------------------------------------------------
    TypeError                                 Traceback (most recent call last)
    <ipython-input-60-c1b0272b0229> in <module>
    ----> 1 tuple1[0]=0 # we can't change a tuple
    TypeError: 'tuple' object does not support item assignment
    ----------------------------------------------------------------------------

```python
tuple1[1]
```
    2

## - Exercice on lists:


        1- Create a list named "my_notes" which contains the following numbers:
                     19,7,15,9,10,6,18,10,16,14,13,10,2,20,17,8,12,10,11,4

        2- Calculate the overall average of this class of 20 students and put the result in a variable called "general_note"

        3- Find the lowest score and the highest score

        4- Sort the list of notes from largest to smallest
        
        5- Replace note 2 by 6
        
        6- Count the number of notes equal to 10 in the class

        7- Count the number of notes equal to 10 in the class
        
        8- Find the number of students with a grade> 10




1- Create a list named "my_notes" which contains the following numbers

```python
mes_notes=[19,7,15,9,10,6,18,10,16,14,13,10,2,20,17,8,12,10,11,4]
```
```python
mes_notes
```
    [19, 7, 15, 9, 10, 6, 18, 10, 16, 14, 13, 10, 2, 20, 17, 8, 12, 10, 11, 4]

2 - Calculate the overall average of this class of 20 students and put the result in a variable called "general_note"

```python
import numpy
moyenne_generale=numpy.mean(mes_notes)
```


```python
moyenne_generale
```




    11.55



3- Find the lowest score and the highest score


```python
min(mes_notes)
```




    2




```python
max(mes_notes)
```




    20



4- Sort the list of notes from largest to smallest 
    - method 1 : 


```python
mes_notes.sort()
```


```python
mes_notes
```




    [2, 4, 6, 7, 8, 9, 10, 10, 10, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]




```python
mes_notes.reverse()
```


```python
mes_notes
```




    [20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10, 10, 10, 10, 9, 8, 7, 6, 4, 2]



   - method 2: using .sort() method 


```python
help(mes_notes.sort)
```

    Help on built-in function sort:
    
    sort(*, key=None, reverse=False) method of builtins.list instance
        Stable sort *IN PLACE*.
    
    


```python
mes_notes.sort(reverse=True)
```


```python
mes_notes
```




    [20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10, 10, 10, 10, 9, 8, 7, 6, 4, 2]



 5- Replace note 2 by 6


```python
mes_notes[19]=6
```


```python
mes_notes
```




    [20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10, 10, 10, 10, 9, 8, 7, 6, 4, 6]



6-  Count the number of notes equal to 10 in the class? : method count()


```python
mes_notes.count(10)
```




    4



7- Count the number of notes equal to 10 in the class


```python
mes_notes_array=numpy.asarray(mes_notes)
```


```python
mes_notes_array
```




    array([20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10, 10, 10, 10,  9,  8,  7,
            6,  4,  6])




```python
mes_notes_array[mes_notes_array>10] # affichage des notes supérieures à 10 
```




    array([20, 19, 18, 17, 16, 15, 14, 13, 12, 11])




```python
mes_notes_array>10 # cette opération est un masque avec des booléens
```




    array([ True,  True,  True,  True,  True,  True,  True,  True,  True,
            True, False, False, False, False, False, False, False, False,
           False, False])




```python
len(mes_notes_array[mes_notes_array>10])
```




    10




```python
mes_notes_array[mes_notes_array>10]
```




    array([20, 19, 18, 17, 16, 15, 14, 13, 12, 11])


