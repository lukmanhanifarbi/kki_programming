# Session 4

- I/O
- Control Flow
- Functions
- Modules
- List Comprehensions

## Overview

- In this session we will learn some concepts which will be useful for the first assignment
- We will first discuss I/O (input/output) to get an idea of how to get and present data in Python through files
- We will then discuss control flow, functions, and modules to help simplify our code
- We will close this session with comprehensions which are unique to Python
- **Remember that your main goal is to hand in the assignment, so only focus on the material you need**
- The rest is just to help explain what happens "behind the scenes"

## Input/Output (I/O)

- The general programming workflow we discussed in the first session is to receive data (input), manipulate it, then present it (output)
- So far, we have manually typed in the inputs to our programs
- We have also relied on JupyterLab and the `print()` function for output
- While this is convenient, our data input and output might disappear when we close JupyterLab
- To keep our data (data persistence), we can save them to files

## Working with Files

- Let's say you're doing some complicated data processing and would like to present your work in a text file:

```python
x=4
y=x**0.5
print('I have found that the square root of ' + str(x) + ' is ' + str(y) + '.')
```

- If you close JupyterLab, you might lose your work
- The following code creates a file (if it does not exist) and writes the result of your work to it:

```python
x=4
y=x**0.5

with open('work.txt', 'w') as file:
    file.write('I have found that the square root of ' + str(x) + ' is ' + str(y) + '.')

print('Work saved (I think).')
```

- The code introduces several new things:
    - The first is the `with` statement which we will not discuss
    - The second is the `open()` function
    - The third is how the `with` statement begins a code block or compound statement, which is represented by the code being shifted to the right
- The `open()` function generally takes two arguments, the first being the file's name and the second being the mode
- The mode represents why you would like to open the file:
    - For reading ('r')?
    - For writing ('w')?
    - For appending ('a')?
- **There is a VERY IMPORTANT DIFFERENCE between writing and appending**; writing means that if the file exists, it will be erased first whereas appending means that it will just be modified
- The code block implies that everything from `with` to the end of the code block is tied together and will (usually) only run together
- We will discuss other aspects of code blocks when we discuss control flow and functions
- To check whether we have written the file properly, we can use the `open()` function's reading mode:

```python
with open('work.txt', 'r') as file:
    print(file.read())
```

## Control Flow

- Why might not need to run all code in our program
- Some code might only be run in certain situations
- This is basically what control flow is about
- At a basic level, control flow in programming languages usually concerns conditional statements and loops

## Conditional Statements

- Conditional statements let you run different code depending on (conditional on) the situation
- One of the basic conditional statements is the `if` statement, which runs a code block if a condition gives the `True` boolean value:

```python
if True:
    print('It's True!')
    print('Yes it's True!')
    print('Believe it!')
```
 
- It helps to go through Session 2 again to see how to generate a `True` boolean value
- Try these examples and see which ones cause the code block to run:

```python
if 3 > 2:
    print('It's True!')
    print('Yes it's True!')
    print('Believe it!')

if True or False:
    print('It's True!')
    print('Yes it's True!')
    print('Believe it!')

if not False:
    print('It's True!')
    print('Yes it's True!')
    print('Believe it!')

if not 0 and []:
    print('It's True!')
    print('Yes it's True!')
    print('Believe it!')
```

- Why doesn't the last example run?
- The basic `if` statement can be augmented with the `elif` and `else` statements
- A typical example is the ['FizzBuzz'][https://en.m.wikipedia.org/wiki/Fizz_buzz] test, where someone is asked to write a program which prints:
    - "Fizz" if it receives a multiple of 3
    - "Buzz" if it receives a multiple of 5
    - "FizzBuzz" if it receives a multiple of 15
    - the number itself if none of the above are true (optional)

```python
x = 2

if x%3==0:
    print('Fizz')
    if x%5==0:
        print('FizzBuzz')
elif x%5==0:
    print('Buzz')
else:
    print(str(x))
```

- The first line in the code above is us manually storing our input data into the variable `x`
- The next line of code begins the `if` statement, where the condition will be true if the number stored in `x` is completely divisible by 3
- The next `if` statement begins a nested code block, which just means a code block inside of a code block
- The idea is that after checking whether the number in `x` is divisible by 3, it should be checked whether or not the number is also divisible by 5
- Then comes the `elif` statement which provides an alternative flow in case the condition in the very first `if` statement is not true
- Last is the `else` statement which provides the final alternative flow of code if all previous conditions turn out to be false

## Loops

- Loops allow you to run the same lines of code repeatedly until certain conditions are fulfilled (iteration)
- We will focus on the two main loops, which are `for` loops and `while` loops
- `for` loops are usually an example of definite loops because the number of repeats or iterations is usually fixed
- Containers in Python are an example of iterables, which implies (among other things) that a `for` loop can be used to run code on each of the container's elements:

```python
x = (True, False, False, True)

for i in x:
    if i==True:
        print('It's True! Believe it!')

x = ('good morning', 'yes sir', 'yes madam')

for i in x:
    print(i.toUpper())
```

- `while` loops are an example of indefinite loops because the number of repeats or iterations is not usually known; the loop keeps running until a condition is met:

```python
wealth = work_months = 0
monthly_income = 10000000
monthly_expenses = 8000000

while wealth < 1000000000000:
    wealth += monthly_income - monthly_expenses
    work_months += 1

print('After working for ' + str(work_months) + ' months you have finally become rich!')
```

## Functions

- We have used several functions which have been well-written such as `print()`, `len()`, and `open()`
- We consider them good functions because like good programs, we do not need to know exactly how they work besides what inputs they take and what outputs they give
- While we will not examine specific functions, it helps to have a general understanding of how functions work
- Functions are one implementation of the DRY principle, short for 'Don't Repeat Yourself'
- If you use the same code several times and they all have a mistake or to be modified, you have to modify all of them
- Functions allow you to give a name to some code so that you can reuse it easily
- In Python, a typical function is defined like this:

```python
def magic(first, second):
    x = first+second
    x = x*10
    x = x - first - second
    x = x/(first+second)
    return x
```

- There are five main components to this function:
    1. The `def` keyword, which tells Python that we wish to define or declare a function
    2. The name of the function, in this case 'magic'
    3. The function arguments or parameters which are in brackets
    4. The set of instructions the function contains, which are in a code block
    5. The `return` statement, which defines the output of a function
- Now we can use this function `magic()` wherever we want
- If we want to change it, we only need to do it once and it will be changed no matter where it is
- Functions are objects too, so what happens when you use the `dir()` function on the `magic()` function? How about the `len()` function? How about the `int()` function? 

## Function Scope

- Code blocks are related to scope, which is whether or not certain variables are 'hidden' from the rest of the program
- The variable `x` was declared inside the `magic()` function and so it is hidden from the rest of the program unless certain things are done

## Function Parameters

- In the `magic()` function, the order of the arguments does not really matter
- `magic(2,3)` and `magic(3,2)` both give the same result
- But if the order does matter, then it helps to make sure that the function uses the inputs properly

```python
def math_stuff(first, second):
    return first ** second
```

- The first is to make sure that the people using the function type the arguments in the right order
- The second is to explain the keywords used in your function arguments:

```python
def math_stuff(first, second):
    return first ** second

print(mathstuff(2,3))
print(mathstuff(second=3, first=2))
```

- With keywords, the order does not matter and the function should receive the inputs properly

## Modules

- Modules are files which contain variables, functions, and other things to be reused
- This means that if you use the same variables, functions, etc over and over again, all you need to do is put them in a module once and use them instead of defining them each time you start a project
- In other languages, modules are called libraries, packages, or have other names (e.g. the Ruby language has 'gems')
- We will only discuss how to import modules so that we can start doing the first assignment
- The first assignment requires us to first "load" the data in our `.csv` file
- The command required to do this is contained in the `csv` module which have to import first:

```python
import csv
```

- Inside this module is something called `reader` which we need
- How do we tell Python to use `reader` which is in the `csv` module?
- Here's how:

```python
the_data=[]

with open('data_kki.cav', 'r') as file:
    for i in csv.reader(file, delimiter=';'):
        the_data.append(i)

print(the_data)
```

- Using `csv.reader()` on the csv file 'data_kki.csv' results in a list of lists (nested list) which we store in the variable `the_data`
- To access a row we use one index:

```python
print(the_data[0])
```

- To access a column along that row we use a second index:

```python
print(the_data[3][4])
```

- This is a very painful way of doing the first assignment
- We will learn how to do the second assignment using more convenient approaches
- Remember that using Python is about making programming fun!

## List Comprehensions

- We end this session with comprehensions, which is yet another way Python helps make programming (and data analysis) easier
- Comprehensions combine the convenience of for loops, conditionals, and functions in order to affect all elements from certain container types
- There are three main comprehensions named after the containers they work with
- We will focus on list comprehensions
- A simple use for list comprehensions is taking a list of numbers and doing simple operations with them

```python
numbers = [1,2,3,4]
squared = [x**2 for x in numbers]
print(squared)
```

- How about doing sonething similar for strings?

```python
cities = ['tokyo','penang','amsterdam','oslo']
proper_cities = [x.capitalize() for x in cities]
print(proper_cities)
```

- How about for 'FizzBuzz'?

```python
fizzbuzz = ['FizzBuzz' if (x%3==0 and x%5==0) else 'Fizz' if x%3==0 else 'Buzz' if x%5==0 else x for x in (10,11,12,13,14,15,16,17,18)]
print(fizzbuzz)
```

## Summary

- Files can be used for data persistence, which is to keep the data after the program has finished
- Not all code in a program will be used; some will only be run during certain situations depending on the control flow set by the programmer
- The main forms of control flow we cover in this session are `if` statements, `for` loops, and `while` loops
- Functions can help simplify programs especially if the same code is to be used many times
- Modules are just files containing code that will be re-used so they also help simplify programs
- List comprehensions are a convenient way to perform operations on all elements of a list

## References

- https://realpython.com/read-write-files-python/
- https://realpython.com/python-conditional-statements/
- https://realpython.com/python-for-loop/
- https://realpython.com/python-while-loop/
- https://realpython.com/defining-your-own-python-function/
- https://realpython.com/python-modules-packages/
- https://realpython.com/list-comprehension-python/
- https://docs.python.org/3/library/stdtypes.html

## Next Session

- Matplotlib