# Session 3

## Containers

- So far we have only discussed data types that only take in one piece of data (kind of) such as one number or one letter
- Programming languages usually also have container data types which can have more than one value inside them
- In this session, we will focus on the following container types:
	- Tuples
	- Lists
	- Strings
	- Dictionaries
- We will also discuss objects and how they play in important role in Python

## Tuples

- Tuples look like this:

```python
(1,2,3)
```

- It contains several pieces of data seperated by commas and surrounded by normal brackets
- They can also be made by giving the `tuple()` function a container:

```python
tuple((1,2,3))
```


- Tuples are ordered, so index notation can be used to retrieve a piece of data in the tuple (called an element):

```python
(1,2,3)[1]
```

- Note that indices in Python start from zero, so in the above example the code retrieves the second value from the tuple
- Negative indices start from the end of the tuple

```python
(1,2,3)[-1]
```

- You can also define starting and stopping indices as well as step size, which is called subsetting or slicing:

```python
(1,2,3,4,5)[1:4]
(1,2,3,4,5)[1:4:2]
```

- The size of tuple can be checked using the `len()` function:

```python
len((1,2,3,4,5))
```

- There are also other operators and functions which useful when working with tuples:

```python
2 in (1,2,3,4)
2 not in (1,2,3,4)
min((1,2,3,4))
max((1,2,3,4))
```

- There are also operators we have used before but act differently when used on tuples:

```python
(1,2,3) + (3,4,5)
(1,2,3)*3
```

- One special feature of tuples is that their contents cannot be changed (immutable)

```python
a=(1,2,3)
a[0]=10
```

- Tuples can be assigned to variables like the simpler data types we discussed before, which is called packing:

```python
a=(1,2,3)
```

- In fact, containers allow for a special type of assignment called unpacking which allows multiple variables to be assigned different values

```python
(name,age,height)=("Bambang",22,"167cm")
a=("Tyrannosaurus Rex","Very VERY old","Very VERY tall")
(name,age,height)=a
```

- Tuples support nesting, meaning that they can contain other containers:

```python
a=((1,2,3),[1,2,3],'a','b','c')
```

- To retrieve an element in a container that is inside another container, an additional index is used:

```python
((1,2,3),[1,2,3],'a','b','c')[1][1]
```

- The tuple above contains another tuple as well as a list, which we will discuss later in this session

## Strings

- While we have discussed strings before, they are not as simple as numbers
- Strings are actually like tuples

```python
'Python4life\m/'[1]
'Python4life\m/'[-1]
'Python4life\m/'[1:4:2]
len('Python4life\m/')
't' in 'Python4life\m/'
'x' not in 'Python4life\m/'
'Python' + 4 + 'Life'
'Python' + '4' + 'Life'
'Python4life\m/'*3
'Python4life\m/'[3]='a'
(x,y,z)=('set')
```

## Lists

- Lists look like this:

```python
[1,2,3]
```

- They are also like tuples but have square brackets instead of normal brackets and their contents can be changed (mutable):

```python
x=[1,2,3]
x[1]='a'
print(x)
```

- They can also be made by giving the `list()` function a container:

```python
list((1,2,3))
```

- Operations and functions that work on tuples should also work on lists:

```python
[1,2,3]
[1,2,3][-1]
[1,2,3][1:4:2]
len([1,2,3])
1 in [1,2,3]
4 not in [1,2,3]
[1,2,3] + [4,5,6]
[1,2,3]*3
(x,y,z)=[1,2,3]
min([1,2,3,4])
max([1,2,3,4])
[(1,2,3),[1,2,3],'a','b','c'][1][1]
```

- There are also operators which work on lists but not tuples:

```python
x=[1,2,3,4,5,6,7,8,9]
x[1:3]=(4,5)
print(x)
del x[1:3]
print(x)
x[0:7:2]=('a','b','c','d')
print(x)
del x[1:3]
print(x)
x+=(2,4)
print(x)
x*=3
print(x)
```

## Dictionaries

- Dictionaries look like this:

```python
ibukota = {'Perancis': 'Paris', 'Mesir': 'Cairo', 'Malaysia': 'Kuala Lumpur', 'Indonesia': 'Jakarta'}
```

- Dictionaries are not ordered in the same way as the containers we have discussed so far
- Their elements are linked or 'mapped' to keys

```python
ibukota = {'Perancis': 'Paris', 'Mesir': 'Cairo', 'Malaysia': 'Kuala Lumpur', 'Indonesia': 'Jakarta'}
print(ibukota['Perancis'])
print(ibukota[0])
```

- We therefore say that they are made by using curly brackets and filling them with 'key-value pairs' separated by commas
- In other programming languages, sometimes dictionaries are called associative arrays
- They can also be made using the `dict()` function in several ways:

```python
ibukota = dict([('Perancis','Paris'), ('Mesir','Cairo'), ('Malaysia','Kuala Lumpur'), ('Indonesia','Jakarta')])
ibukota = dict(Perancis='Paris', Mesir='Cairo', Malaysia='Kuala Lumpur', Indonesia='Jakarta')
ibukota = dict(zip(('Perancis','Mesir','Malaysia','Indonesia'),('Paris','Kairo','Kuala Lumpur','Jakarta')))
```

- It is also possible to start with an empty dictionary and grow it as needed

```python
ibukota = {}
ibukota['Perancis']='Paris'
ibukota['Mesir']='Cairo'
print(ibukota)
```

- Feel free to choose the easiest way when you need to use a dictionary
- We cannot subset/slice dictionaries in the same way as the previous container types
- We shall discuss how to do this in the next session
- Dictionary values can be replaced like in lists as long as the correct key is used

```python
ibukota = {'Perancis': 'Paris', 'Mesir': 'Cairo', 'Malaysia': 'Kuala Lumpur', 'Indonesia': 'Jakarta'}
ibukota['Indonesia'] = 'IKN'
print(ibukota['Indonesia'])
```

- The following operations and functions can be used with dictionaries:

```python
ibukota = {'Perancis': 'Paris', 'Mesir': 'Cairo', 'Malaysia': 'Kuala Lumpur', 'Indonesia': 'Jakarta'}
list(ibukota)
len(ibukota)
del ibukota['Perancis']
'Perancis' in ibukota
'Australia' not in ibukota
```

- It is also possible to include containers such as other dictionaries (nesting):

```python
Bambang = {}
Bambang['fisik']=dict(mata='coklat', rambut='lurus', tinggi='172cm', kacamata=False, nama_lengkap=['Bambang','Wicaksono'])
print(Bambang['fisik']['nama_lengkap'])
```

## Objects

- Python is built on objects, which means that the data can have values and functions attached to them
- In Python, values attached to an object are called attributes whereas functions attached to an object are called methods
- We have used the `type()` function to check the type or class of any data
- We use the `dir()` function to check what attributes and methods that type has

```python
dir(2)
dir(2.0)
dir(True)
dir('True')
dir((1,2,3))
dir([1,2,3])
dir(dict(a=1, b=2, c=3))
```

- An object's attribute or method can be as follows:

```python
'abc'.__class__
'abc'.upper()
x=[1,2,3]
x.append(5)
print(x)
```

- Note that methods have brackets while attributes don't
- One benefit to designing Python this way is that it makes code cleaner and prevents programmers (or at least tries to) from using functions on the wrong types
- Because almost everything in Python is an object or class, you should be able to use `dir()` on almost everything to find out what attributes and methods it has
- We've covered a lot of material so feel free to take a breath before exploring the attributes and methods of the types we have discussed so far
- The references at the end give summaries of these attributes and methods

## Summary

- Python has container data types which can contain other data types 
- Containers can include other containers which is called nesting
- Tuples cannot be changed (immutable) while lists can (mutable)
- Strings are basically a special kind of tuple
- Dictionaries can be changed but have keys to access their elements instead of ordered indices
- In Python, almost everything is an object which means that almost everything has attributes and methods

## References

- https://realpython.com/python-lists-tuples/
- https://realpython.com/python-strings/
- https://realpython.com/python-dicts/
- https://docs.python.org/3/library/stdtypes.html

## Next Session

- I/O
- Functions
- Modules
- Matplotlib
- Control Flow