---
title: 5 Dictionaries
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 5
---
![image0](/img/pylogo.png)
<img src="./figures/pylogo.png" alt="Indentation" width="50%" height="50%">


 - The dictionary stores (key, value) pairs 
 - They are unordered data structures
 - Principle: we can link a key to a value
 - The values of a dictionary can be of any type, but the keys must be of an immutable data type such as strings, numbers, or tuples.
 - Keys are unique within a dictionary while values may not be.
 - Each key is separated from its value by a colon (:), the items are separated by commas, and the whole thing is enclosed in curly braces. 
 - An empty dictionary without any items is written with just two curly braces, like this: {}.
 - Dictionary values have no restrictions. They can be any arbitrary Python object, either standard objects or user-defined objects. However, same is not true for the keys.
 - Keys must be immutable. Which means you can use strings, numbers or tuples as dictionary keys but something like ['key'] is not allowed. 
 
You can find all you need to know about dictionaries in the documentation:
https://docs.python.org/2/library/stdtypes.html#dict


## 5.1 Create a dictionary:

In a dictionary, each key is separated from its value by a colon (:), the items are separated by commas, and the whole thing is enclosed in curly braces like this: {}.

```python
# exemple : students' note dictionary
my_dictionary = {
    "Marie" : 15,
    "Thomas" : 12,
    "Julien" : "absent",
    "Elise" : 9,
    "Samuel" : 17
}
```


```python
my_dictionary  # We have the key : the value 
```




    {'Marie': 15, 'Thomas': 12, 'Julien': 'absent', 'Elise': 9, 'Samuel': 17}



## 5.2 Update a dictionary: 

You can update a dictionary by adding a new entry or a key-value pair, modifying an existing entry, or deleting an existing entry as shown below.

- To <b>add</b> key-value pair 


```python
# Adding a key-value pair in a dictionary
my_dictionary["Julie"]=9
print(my_dictionary)
```

    {'Marie': 15, 'Thomas': 12, 'Julien': 'absent', 'Elise': 9, 'Samuel': 17, 'Julie': 9}
    

- To <b>change</b> a value using existing key


```python
my_dictionary["Julien"]=13
print(my_dictionary)
```

    {'Marie': 15, 'Thomas': 12, 'Julien': 13, 'Elise': 9, 'Samuel': 17, 'Julie': 9}
    

More than one entry per key not allowed. Which means no duplicate key is allowed. When duplicate keys encountered during assignment, the last assignment wins.


```python
dict = {'Name': 'Zara', 'Age': 7, 'Name': 'Manni'}
dict
```




    {'Name': 'Manni', 'Age': 7}



- To <b>delete</b> a value using a key

You can either remove individual dictionary elements or clear the entire contents of a dictionary. You can also delete entire dictionary in a single operation.

To explicitly remove an entire dictionary, just use the del statement. Following is a simple example −



```python
del my_dictionary["Julie"] # remove entry with key 'Name'
my_dictionary.clear()     # remove all entries in my_dictionary
del my_dictionary       # delete entire dictionary
```


```python
print(my_dictionary)
```
    ---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)
    <ipython-input-7-04bcd56b6daf> in <module>
    ----> 1 print(my_dictionary)
    NameError: name 'my_dictionary' is not defined
    ---------------------------------------------------------------------------


## 5.3 Access a dictionary: 

To access dictionary elements, you can use the familiar square brackets along with the key to obtain its value.

```python
my_dictionary = {
    "Marie" : 15,
    "Thomas" : 12,
    "Julien" : "absent",
    "Elise" : 9,
    "Samuel" : 17
}
```


```python
my_dictionary["Samuel"]   
```
    17

- We can access ditionary elements using <b>FOR</b> loop: 
    - by value valeur
    - by key
    - by key-value pair



```python
# .keys() method returns list of dictionary dict's keys:
my_dictionary.keys()
```




    dict_keys(['Marie', 'Thomas', 'Julien', 'Elise', 'Samuel'])




```python
# .values() method returns list of dictionary dict's values
my_dictionary.values()
```




    dict_values([15, 12, 'absent', 9, 17])




```python
# Example using for loop and keys dictionary
for key in my_dictionary.keys():
    print(key)
```

    Marie
    Thomas
    Julien
    Elise
    Samuel
    


```python
for value in my_dictionary.values():
    print(value)
```

    15
    12
    absent
    9
    17
    


```python
# .items() method returns a list of dict's (key, value) tuple pairs
my_dictionary.items()
```




    dict_items([('Marie', 15), ('Thomas', 12), ('Julien', 'absent'), ('Elise', 9), ('Samuel', 17)])




```python
# Example using for loop and key-value pairs in dictionary
for key,value in my_dictionary.items(): # la boucle for obtient un tuple à chaque itération
    if value == 'absent':
        print('Absent')
    else:
        print('The average of %s is %s /20' % (key, value))
```

    The average of Marie is 15 /20
    The average of Thomas is 12 /20
    Absent
    The average of Elise is 9 /20
    The average of Samuel is 17 /20
    

## Exercise on dictionaries
## Goal: To manipulate a dictionary containing the notes of 15 students. 

    1- Create a dictionary named notes_levels containing the following notes:
    Mary: 15; Samuel: 17; Gaston: 12; Fred: 10; Mae: 5; Julie: 15; Zoe: 7; Claire: 20; Chloe: 8; Julian: 14, Gael: 9, Samia: 15, Omar: 11, Gabriel: 16, Manon: 2

    2- What is the average of the class?

    3- Display the total number of students in the class.

    4- How many students have a grade strictly above average?

    5- What is the name of the best student in the class?

    6- How many students have a first name with strictly less than 4 letters?

    7- Show the first name of the pupils who have an even note (multiple of 2).! 


#### Correction

- 1: 

```python
notes_levels ={
    "Marie" : 15,
    "Samuel" : 17,
    "Gaston" : 12,
    "Fred" : 10,
    "Mae" : 5,
    "Julie" : 15,
    "Zoe" : 7,
    "Claire" : 20,
    "Chloe" : 8,
    "Julien" : 14,
    "Gaël" : 9,
    "Samia" : 15,
    "Omar" : 11,
    "Gabriel" : 16,
    "Manon" : 2
}
```

- 2: 

```python
notes_eleves.values()
```

    dict_values([15, 17, 12, 10, 5, 15, 7, 20, 8, 14, 9, 15, 11, 16, 2])

```python

import numpy  
average_note =numpy.mean(list(notes_eleves.values()))  

``
```python
average_note 
```
    11.733333333333333



- 3: 

```python
nombre_eleves=len(notes_eleves)
print("Le nombre d'élèves dans la classe est de %d" % (nombre_eleves))
```
    Le nombre d'élèves dans la classe est de 15
    
```python
len(notes_eleves.keys())  
```
    15

- 4: 
```python
nombre_eleves_avec_note_sup_moyenne=0
for valeur in notes_eleves.values():
    if valeur > moyenne_generale:   
        nombre_eleves_avec_note_sup_moyenne=nombre_eleves_avec_note_sup_moyenne+1
print("Le nombre d'élèves avec une note supérieure à %.2f est de %d élèves" % (moyenne_generale, nombre_eleves_avec_note_sup_moyenne))
```

    Le nombre d'élèves avec une note supérieure à 11.73 est de 8 élèves
    

- 5:  


```python
# On va d'abord déterminer  la meilleure note: utilisation de la fonction max()
meilleure_note=max(notes_eleves.values())
```python
meilleure_note
```
    20

```python
# On va parcourir notre dictionnaire et trouver la clef associée à notre valeur
# Pour cela on va travailler sur les tuples avec la méthode item()
for prenom,note in notes_eleves.items():
    if note == meilleure_note:
        print(prenom)
```

    Claire
    

- 6: 


```python
# On va parcourir les clefs de notre dictionnaire et mettre une condition sur la longueur de chaque clef

nombre_eleves=0
for prenom in notes_eleves.keys():
    if len(prenom) < 4:
        nombre_eleves=nombre_eleves+1
print(nombre_eleves)
```

    2
    

- 7: 


```python
# On va parcourir les tuples du dictionnaire et mettre une condition sur les valeurs 
for prenom,note in notes_eleves.items():
    if note % 2 == 0:
        print(prenom, note)
```

    Gaston 12
    Fred 10
    Claire 20
    Chloe 8
    Julien 14
    Gabriel 16
    Manon 2
    