---
title: 1 Basic data types 
linktitle: 
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python tutorial 
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
![image0](/img/pylogo.png)

## 1.1 Variables 

A variable is an identifier or name to store information or results.
All python programs use variables. It is important to remember that each type of information is stored in a special type of variable.
A type of variable is an information about the contents of the variable. The type of variable will tell the python interpreter what it can do or not with this variable.

 - Python can make the difference between upper and lower case letters  
 - You can not start a variable with a number
 - Do not use accents in variable names
 - Function : type() give you informations on the type of our variable

```python
m=3.2
```
```python
int(m)
```
    3


### 1.1.1 Numeric type: 
  Type| Description   |
|------|------|
|  Integer: int()  | 1 is an integer, 1.0 is not an integer|
|   Float: float()| Number that includes a decimal part|
|   Complex numbers| Association between a real number and an imaginary number|


```python
type(m)
```
    float
```python
int(3)
```
    3
```python
int(3.5)
```
    3
```python
float(3)
```
    3.0
```python
3+5
```
    8

### 1.1.2 Booleans: 

- variable storing binary values: True or False
- data types result from logical operations

Very useful in if() conditional structures. 

```python
3>5
```
    False
```python
3<5
```
    True

### 1.1.3 Strings:

Python can also manipulate strings, which can be expressed in several ways. They can be enclosed in single quotes ('...') or double quotes ("...") 

```python
print("Hello")
```
    Hello
   
```python
type('Hello')
```
    str
```python
type("15")
```
    str
```python
"15" + 2 
```
    ---------------------------------------------------------------------------
    TypeError                                 Traceback (most recent call last)
    <ipython-input-13-3fe5846cb1c2> in <module>
    ----> 1 "15" + 2
    TypeError: can only concatenate str (not "int") to str
    ----------------------------------------------------------------------------

But we can concatenate two strings together. 
```python
"15" + "56"
```
    '1556'
```python
str(15)
```
    '15'
String objects have a bunch of useful methods; for example:

```python
s = "hello"
print(s.capitalize())  # Capitalize a string; prints "Hello"
print(s.upper())       # Convert a string to uppercase; prints "HELLO"
print(s.rjust(7))      # Right-justify a string, padding with spaces; prints "  hello"
print(s.center(7))     # Center a string, padding with spaces; prints " hello "
print(s.replace('l', '(ell)'))  # Replace all instances of one substring with another;
                           # prints "he(ell)(ell)o"
print('  world '.strip())  # Strip leading and trailing whitespace; prints "world"
```

    Hello
    HELLO
      hello
     hello 
    he(ell)(ell)o
    world
    
## 1.2 Python Arithmetic Operators 

 Operator| Description   |
|------|------|
|  +  | Adds values|
|  -  | Subtracts right hand operand from left hand operand|
|   * | Multiplies values on either side of the operator|
|   / | Divides left hand operand by right hand operand|
|   % | Divides left hand operand by right hand operand and returns remainder (modulus)|
|   %% | Performs exponential (power) calculation on operators|
|   // | Floor Division - The division of operands where the result is the quotient in which the digits after the decimal point are removed. But if one of the operands is negative, the result is floored, i.e., rounded away from zero (towards negative infinity)|

```python
5-3 # Subtraction 
```

    2
```python
5+3 # Addition 
```

    8
```python
5*3 # Multiplication
```
    15
```python
5/3 # division  
```
    1.6666666666666667
```python
5//3 # Floor Division 
```
    1
```python
5%3 # Modulus  
```
    2
```python
5**3 # power
```
    125

```python
ma_variable1=10
ma_variable2=20
ma_variable1*ma_variable2
```
    200
```python
ma_variable1*10
```
    100

We cannot apply arithmetic operators on text. 
```python
"mon texte" - "mon texte"
```
    ---------------------------------------------------------------------------
    TypeError                                 Traceback (most recent call last)
    <ipython-input-26-5483fafb4a74> in <module>
    ----> 1 "mon texte" - "mon texte" 
    TypeError: unsupported operand type(s) for -: 'str' and 'str'
    ----------------------------------------------------------------------------

```python
"Hi" + " how are you ?"
```
    'Hi how are you ?'
```python
"Hi " * 5
```
    'Hi Hi Hi Hi Hi '

## 1.3 Python Comparison Operators

These operators compare the values on either sides of them and decide the relation among them. They are also called Relational operators.
The true value of relationships is often used to make decisions by ensuring that conditions are met to perform a certain task. 

 Operator| Description   |
|------|------|
|  ==  | If the values of two operands are equal, then the condition becomes true|
|  != | If values of two operands are not equal, then condition becomes true|
|  > | If the value of left operand is greater than the value of right operand, then condition becomes true|
|  < | If the value of left operand is less than the value of right operand, then condition becomes true|
|  >= | If the value of left operand is greater than or equal to the value of right operand, then condition becomes true|
|  <= | If the value of left operand is less than or equal to the value of right operand, then condition becomes true|
|  is | Identity operators compare the memory locations of two objects. Evaluates to true if the variables on either side of the operator point to the same object and false otherwise|
|  is not | Identity operators compare the memory locations of two objects. Evaluates to false if the variables on either side of the operator point to the same object and true otherwise|

```python
1 == 1
```
    True
```python
1==2
```
    False
```python
1!=2
```
    True
```python
1>2
```
    False
```python
2>1
```
    True
```python
1>1
```
    False
```python
1<2
```
    True
```python
1>=1
```
    True
```python
2 <= 5
```
    True

```python
a=1 # Warning !!!! this is an assignment  operator
a
```
    1

## 1.4 Python Logical Operators

Logical operators compare Boolean expressions instead of values as in the previous point.

They are used to create Boolean expressions that help us know if a certain task should be performed or not. 
Operator| Description   |
|------|------|
|  and| If both operands are true then condition becomes true|
|  or| If any of the two operands are non-zero then condition becomes true|
|  not| Used to reverse the logical state of its operand|

```python
# and
(3==3) and (4==4)
```




    True




```python
(3==3) and (4==5)
```




    False




```python
# or
(3==3) or (4==5)
```




    True




```python
(3!=3) or (4==5)
```




    False




```python
#  not
not((3!=3) or (4==5))
```




    True



## 1.5 Python Assignment Operators

Assignment operators store a value in a variable. We have already seen the simplest case (=), but python offers many other operators of this type, in particular to perform an arithmetic operation at the same time as the assignment.

Operator| Description   |
|------|------|
|  =| Assigns values from right side operands to left side operand|
|  +=| It adds right operand to the left operand and assign the result to left operand|
|  -=|It subtracts right operand from the left operand and assign the result to left operand|
|  *=|It multiplies right operand with the left operand and assign the result to left operand|
|  /=|It divides left operand with the right operand and assign the result to left operand|
|  %=|It takes modulus using two operands and assign the result to left operand|
|  **=|Performs exponential (power) calculation on operators and assign value to the left operande|
|  //=|It performs floor division on operators and assign value to the left operand|


```python
Mavariable = 5 
```


```python
Mavariable = 2
Mavariable
```




    2




```python
Mavariable = 5 
Mavariable += 2 
Mavariable
```




    7




```python
Mavariable = 5 
Mavariable -= 2 
Mavariable
```




    3




```python
Mavariable = 5 
Mavariable *= 2 
Mavariable
```




    10




```python
Mavariable = 5. 
Mavariable /= 2 
Mavariable
```




    2.5




```python
Mavariable = 5 
Mavariable %= 2 
Mavariable
```




    1




```python
Mavariable = 5 
Mavariable **= 2 
Mavariable
```




    25




```python
Mavariable = 5. 
Mavariable //= 2 
Mavariable
```




    2.0


