# Session 2

## Things to Think About

- What is data?
- How do I talk to the computer?

## Programming as a Data Pipeline

1. Get data
2. Do stuff, usually transform data
3. Maybe present it

## Data Types

- Data come in many forms
- Some languages are very strict about what type of data is being used:
	- What is a number? What is a letter?
	- Can letters be converted into numbers or vice-versa?
	- Can letters be added? How about words?

## Data Types - Numbers

- Most computers today are based on binary digits or bits
- Some of the easiest types of data to work with based on these digits are integers or whole numbers
- From there it's also possible to represent floating point numbers or floats, with some limitations
- Consider the following examples, which use the `type()` function to check 

```python
type(2)
type(2.0)
```

## Data Types - Boolean

- The boolean type is either "True" or "False"
- In Python it is considered a type of number
- All values are considered "True" except for:
	- The value "None"
	- The value "False"
	- Any number 0 whether as an integer, float, or any of the other numeric types
	- Empty sequences and collections (next session)
- We will see how this can be useful later on 

```python
type(True)
type(False)
```

## Data Types - Strings

- Character-based data are called strings
- There is another aspect of strings we will discuss later
- For now consider the following examples:

```python
type(2)
type(2.0)
type(True)
type(False)
type('2')
type('2.0')
type('True')
type('False')
```

## Operators

- Operators are simple things you can do with your data
- For now we shall consider the following types of operators:
	1. Arithmetic Operators
	2. Comparison Operators
	3. Logical Operators
	4. Assignment Operators

## (Lack of) Type Conversion/Coercion

- Consider that some operators (and functions, methods, etc) only accept certain types
- Try the following to see what happens when you mix the types we've used so far:

```python
type(2.0+3)
type(False+3)
type('a'+3)
type('a'+'a')
```

- We mentioned how some languages are very strict on making sure that only the correct types can be used with certain operators
- Some languages also automatically convert (or "coerce") data into the correct type
- Python does not allow us to add a string and a number
- However, it does allow us to add a boolean and a number
- But what type is the result? Why was Python designed this way?
- The `int()`, `float()`, `bool()`, and `str()` functions can be used to force data to be a certain type

```python
int(2.0)
float(2)
bool(2)
str(2)
```

- What happens when you convert string into a number?
- What can make the `bool()` function result in "False"?

## Arithmetic Operators

- Several Python tutorials encourage you to at least use Python as a calculator:

```python
2/3
2**3
2%3
1/0
```

- Note that adding a float to an integer results in a float
- Note that dividing an integer by another integer results in an integer
- To "properly" divide a number by another, either the numerator or denominator must be manually written as or converted into a float

```python
2.0/3
float(2)/3
```

## Comparison Operators

- The main comparison operators we will use are `==`, `!=`, `<`, `<=`, `>`, `>=` 
- They compare at least two values
- We will focus on using comparison operators with numbers even though they also work with other types
- They generally result in either Boolean value, True or False

```python
2.0 == 2
-0.5 > 2
```

## Logical Operators

- The main logical operators we will use are `not`, `or`, and `and`
- They compare two boolean values even though they also work with other types
- The `not` operator simply returns the negative (opposite) of a boolean value
- The `and` operator will result in "True" only if all values are "True"
- The `or` operator will result in "True" only if at least one value is "True" (inclusive "or")

```python
not True
True or False
True and False
'a' or 'b'
3 and 'c'
```

## Assignment Operators

- Assignment operators basically link data to a name that can be called as needed
- This is done by storing data in a variable

```python
a = 2
b = 1
a + b
```

- This is called creating (if it didn't exist before) and initializing (giving new variables a value) variables 
- Assignment is also used to update variables

```python
a = 2
a = 2 + 5
a = a + 2
```

- In the above code, the last row is understood as "take whatever is in the variable 'a', add 2, then use the result as the new value of 'a'"
- This can be shortened to `a += 2` which is an example of augmented assignment and can be used with other operators:

```python
a = 2
a += 2
a -= 2
a *= 2
a /= 2
```

- Python also allows multiple assignment

```python
a = b = c = 0
```

## Operator Precedence

- Different languages might process operations in different orders
- Basic arithmetic for example, follws the BODMAS (Brackets Order Division Multiplication Addition Subtraction) rule
- Compare the following:

```python
a = 2 + 3 * 5
a = (2 + 3) * 5
a = 2 + (3 * 5)
```

- This also applies to types and operations that apply to data which aren't numbers:

```python
a = 'a'*5 or 'b'*3
a = not 'c' + 1 and False**2
```

- The way certain programming languages are designed can result in "tricks" programmers can use to write shorter code
- While Python also has such tricks, it was mainly designed to be easily readable
- Compare with languages such as C and Perl

## Summary

- Programming as processing data
- Several different types of data, such as numbers, letters, and boolean values 
- Data can be processed by performing operations on them, but operations might not accept all types of data
- Brackets can be used to change the order of operations

## References

- https://realpython.com/python-data-types
- https://realpython.com/python-operators-expressions
- https://realpython.com/python-assignment-operator
- https://docs.python.org/3/library/stdtypes.html
- https://docs.python.org/3/reference/expressions.html

## Next Session

- Containers
- Objects
