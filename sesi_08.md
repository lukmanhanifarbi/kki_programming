# Session 8

## Overview

- We have covered at least two ways of using the Python programming language for data analysis, namely using basic Python and using the Pandas module
- There are still many more Python modules useful for data analysis such as scikit-learn, statsmodels, and linearmodels
- Now we shall look at another programming language commonly used for data analysis, namely R
- We shall briefly compare R to Python and go through how to use R at a basic level

## Python VS R

- [Wes McKinney](https://wesmckinney.com/book/preliminaries.html) and [Prof. Norman Matloff](https://github.com/matloff/R-vs.-Python-for-Data-Science) offer comparisons of Python (especially Pandas) with R
- Python is a general purpose programming language whereas R was designed for data analysis from the start
- Python by itself can be used with basic programming ideas whereas R was designed to take advantage of advanced features such as vectorization; the Pandas module (and the NumPy module it is built upon) are ways of making Python "like R"
- Because Python has a more general purpose, it has modules/packages for a wider variety of applications instead of just statistics; this means it is not always a good idea to use R "like Python"

## Base R VS The Tidyverse

- Two "styles" of R have emerged, namely "base R" and the "Tidyverse"
- [Hadley Wickham](https://r4ds.hadley.nz/whole-game.html) explains the data analysis workflow behind the "Tidyverse" packages
- [Prof. Norman Matloff](https://github.com/matloff/TidyverseSkeptic) thinks it is better to go with base R and [makes several comparisons on how both styles achieve the same thing](https://github.com/matloff/TidyverseSkeptic/blob/master/RDesign.pdf)
- This workshop will teach base R

## Data Types

### R Objects

- Like Python, data types in R are mostly based on objects
- A given R object can be inspected in the following ways:
    - The `typeof()` function will give its type
    - The `length()` function will give how many elements it contains
    - The `attributes()` function will give all if its attributes and the `attr()` will give a specific attribute
    - The `str()` function will give its structure
- However, R was designed to use functions more than methods; methods still exist but they are mostly used in the background
- This design style is called _generic function object oriented programming_

### Atomic Vectors

- Atomic vectors are the basic data container
- According to the [official documentation](https://cran.r-project.org/doc/manuals/r-release/R-lang.html#Vector-objects), there are six atomic vector types:
    1. Logical
    2. Integer
    3. Real
    4. Complex
    5. Character (also called _strings_)
    6. Raw

- This implies that the elements of an atomic vector all have the same type
- An atomic vector is put together using the `c()` function, short for "concatenate" or "combine":

```r
c(1,2,3)
```

- Type coercion applies for atomic vectors to help make sure all elements are the same type

```r
print(typeof(c(1,2,3,'a')))
```

- Single numbers, letters, Boolean values, etc are actually vectors with one element in them
- Unlike containers in Python, atomic vectors cannot be nested
- Combining vectors results "flattens" the contents in all of them inside a new vector

```r
c(c(1,2,3),c(3,8,2))
```

- Vector elements can have names (indices in Pandas containers) which can be set in several ways
- Here are two examples:

```r
c(a=1, b=2, c=3)
x <- c(1,2,3)
names(x) <- c('a','b','c')
```

- Note that the first method is very similar to how dictionaries are assigned in Python
- Note also for the second method that unlike Pandas, a function is used to change vector names instead of a method
- This reflects how R was designed so that functions are used instead of methods (except in the background)
- Like in Pandas containers, names do not have to be unique
- Also like Pandas containers, having unique names helps when subsetting elements of a container (as we shall discuss later)

### Lists

- Lists or _generic_ vectors allow for different types among its elements
- A list can be created using the `list()` function:

```r
list(1,"a")
```

- This means that unlike atomic vectors, lists can be nested:

```r
list(list(1,"a"),list(1,"a"))
```

- Creating a vector from lists flattens the lists:

```r
c(list(1,"a"),list(1,"a"))
```

### Working with Strings
 
- When working with strings in Python, we mostly depend on string methods
- Again, R expects that [string functions](https://jozef.io/r007-string-manipulation/) will be used

```r
...
```

### Factors

- Factors are a special type of vector used to store categorical data
- One of their attributes is `.levels` which contains all values permitted in the vector
- They can be ordered e.g. child, teenager, adult or unordered e.g. red, blue, yellow
- Unordered factors are created by using the `factor()` function on an atomic vector:

```r
    factor(c("iOS","Android","iOS","Android"))
```

- Ordered factors are created by using the `ordered()` function and giving an atomic vector to the `levels` argument:

```r
   ordered(c("teenager","adult","adult","child"), levels = c("child", "teenager", "adult"))
```

- Using these types of vectors makes it easier to perform categorical data analysis in R
- One example is that the vector can only be modified using values defined in the `.levels` attribute, which helps prevent data entry errors

### Matrices and Arrays

- Matrices and arrays are also treated as special atomic vectors
- What makes them different is that they have the `dim` attribute referring to the size of their dimensions
- For example, 9 numbers can be perceived as:
    - an atomic vector with 9 elements
    - a 3x3 matrix
    - a 3x3x3 array
- Therefore a vector with dimensions is generally called an array in R, whereas a matrix is an array with two dimensions
- Matrices and vectors can be created using their associated functions or by changing their dimensions using the `dim()` function:

```r
matrix(1:9, ncol=3, nrow=3)
array(1:9, dim=c(1,3,3))

x <- c(1:9)
dim(x) <- c(3,3)
dim(x) <- c(1,3,3)
```

### Data Frames

- R data frames are created as follows:

```r
data.frame(a=1:3,b=c('a','b','c'))
```

- Where the argument names become the column names
- Hadley Wickham [notes](http://adv-r.had.co.nz/Data-structures.html#data-frames) that strings are converted to factors by default
- This can be changed using the `stringsAsFactors` argument

```r
data.frame(a=1:3,name=c('Dono','Indro','Kasino'), stringsAsFactors=FALSE)
```

### On "Growing" Containers

- Copies VS Views
- R Inferno

### Functions

- Functions in R are created as follows:

```r
y <- function(x) x^2

y <- function(x) {x^2}

y <- function(x) {
        x^2
}
```

- Several things to note are:
    - The code block containing the actual function code is surrounded by curly brackets, whereas code blocks in Python are represented by identing the code
    - The function is "saved in a variable" whereas in Python, the function is just created using `def`
    - We have presented functions as an object instead of giving it its own section
- Again, R was designed to make heavy use of functions which we shall not discuss in this course
- If you are interested, you can read the [first edition of Hadley Wickham's book](http://adv-r.had.co.nz/Functions.html) on advanced R programming

## Loading and Storing Data

- As with Python, we shall focus on importing from and saving to `.csv` files
- The relevant functions are the `read.csv()` and `write.csv()` functions
- When using `read.csv()` remember to check the `.csv` file and note the separator/delimiter to make sure the data is imported
- Another option that R offers is to save multiple objects in the current session to a file
- This is done using the `save()` function, and results in a file with the ".Rdata" extension
- To reuse the saved objects, use the `load()` function

## Control Flow, Operations, and Applying Functions

- The two main control flow concepts we have discussed, conditionals and loops, are also in R:

```r
if ( x > 5 ) print('yes') else print('no')
if ( x > 5 ) {
    print('yes')
    print('definitely')
} else {
    print('no')
    print('not really')
}

for (i in c(1,2,3)) print(i)
for (i in c(1,2,3)) {
    print('The number is')
    print(i)
}
```

- The first examples of both are "one liner" examples or how the code looks if it fits on one line
- The second examples are when many instructions are involved and require the code to be written over multiple lines
- Note that like in Python, `for` loops in R go through the elements of containers such as atomic vectors, lists, and data frames
- However, conditional statements are available in functional form and operations are already vectorized
- Let's say we wanted to generate a sequence of numbers and output a value based on whether they are greater or smaller than 5
- Using basic programming concepts, it could be written like this in R: 

```r
for (i in 1:10) {
    if (i > 5) {
        print(0)
    } else {
        print(1)
    }
}
```

- A more appropriate way to express this in R is:

```r
ifelse(1:10 > 5, print(0), print(1))
```

- Note the colon operator `:` which simply creates a sequence of numbers from 1 to 10
- R also offers the `apply()` family of functions which helps maximize the benefits of vectorization
- The `apply()` function itself is used to apply a function to every row or column (or both) of a matrix/array/data frame

```r
apply(matrix(1:9, nrow=3, ncol=3), mean)
```

- The `lapply()` function is used to apply a function to every element of a list

```r
lapply(list(1:3,4:6,7:9), mean)
```

## Subsetting

- There are three main subsetting ("extraction" according to the [official documentation](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Extract.html)) operators in R:
    - Single square brackets `[]`
    - Double square brackets `[[]]`
    - The dollar sign `$` 
- The single square brackets are the main way of subset/index containers in R
- There are several ways to use single square brackets but we shall only discuss four:
    - Using positive integers
    - Using negative integers
    - Using Boolean values
    - Using names
- We will discuss subsetting for the four main container types, namely atomic vectors, lists, matrices/arrays, and data frames

### Subsetting Atomic Vectors

- Using single square brackets with positive integers simply selects the elements based on their order, where *indexing in R begins at 1 instead of 0*:

```r
print((1:10)[c(1,3,5)])
```

- Using single square brackets with negative integers gives the container *without the elements selected*:

```r
print((1:10)[-c(1,3,5)])
```

- Using single square brackets with a vector of Boolean values works like in Pandas:

```r
print((1:10)[(1:10) > 5])
```

- Using character/string-based vectors also works like in Pandas:

```r
x <- 1:10
names(x) <- letters[1:10]
print(x['a','f','c'])
```

- It is also possible to repeat indices:

```r
x <- 1:10
names(x) <- letters[1:10]
print(x['a','a','a'])
print(x[1,1,1])
```

### Subsetting Matrices/Arrays

- We discuss matrices/arrays first because they are more similar to atomic vectors than lists and therefore the ways they are subset are also similar
- The main difference between matrices/arrays and atomic vectors is that matrices/arrays have dimensions
- Therefore a matrix/array can be subset by giving one atomic vector per dimension containing the positions of the elements you want:

```r
print(matrix(1:9,nrow=3)[1:3,2:3])
print(matrix(1:9,nrow=3)[1:3,])
```

### Subsetting Lists

- Subsetting lists with the single bracket operator will return another list

```r
print(list(c(1:3),c(letters[1:3]))[2])
```

- For programming purposes, this is not always ideal
- Subsetting lists with the double bracket operator will return an element from a list and can be more appropriate

```r
print(list(c(1:3),c(letters[1:3]))[[1]])
```

- If each element in the list is named, using the names also works:

```r
print(a=list(c(1:3),b=c(letters[1:3]))[['b']])
```

- As explained in the official documentation, the difference between the dollar sign operator and the double square brackets operator is that the dollar sign operator does not allow a "computed" index but does automatically allow partial matching:

```r
x <- list(apples=c(1:3),bananas=c(4:6))

print(x)

print(x[[3-1]])
print(x$(3-1))

print(x[['app']])
print(x$app)
```

- One may conclude that if computations are required to obtain the element positions in a list or similar container, the double square brackets operator is preferred
- On the other hand, if the intention is to select list elements by name - especially when some element names are very long or tedious to type in - the dollar sign operator is preferred

### Subsetting Data Frames

- Data frames are basically matrices organized like lists because data frame columns might contain various types of data
- Using the single square bracket operator with two vectors will subset the data frame as if it were a matrix
- Using the single square bracket operator with two vectors will subset the data frame as if it were a list
- Remember that using the single square brackets operator returns a list
- The double square brackets or dollar sign operators are usually used to select a column from a data frame

## Libraries

- A fresh installation of R already offers a powerful toolset for working with data
- However, R is used by many people around the world who have helped extend its functionality to new techniques, such as machine learning algorithms, to specialized fields, such as biostatistics
- These extensions are preserved as libraries which can be uploaded and downloaded to your local system
- A library can be installed with the `install.packages()` function

```r
install.packages('tidyverse')
```

- After a library has been installed, they must then be loaded into the current session using the `library()` function

```r
library(tidyverse)
```

- Note that the name of the library must be surrounded in quotes when installing but not when loading

## Plotting

- The `plot()` function is used for plotting line graphs

## Summary

- 

## References

- Chapter 1 of Wes McKinney's Book
- Norm Matloff's comparison
- Hadley Wickham's Advanced R
- R language reference

## Next Session

- Closing Remarks
