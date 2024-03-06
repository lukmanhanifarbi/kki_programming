# Session 7

## Overview

- In the previous session, we discussed how to create an initial Pandas container as well as how to subset data inside it
- In this session we will go through some useful things that can be done with existing Pandas containers related to modifying Pandas containers, actual "data crunching", and finally visualization
- Understanding the topics in this session will help with understanding how R works

## Pandas Containers VS Basic Python Containers

- We have seen in the previous session that Pandas containers can be converted from basic Python containers, e.g. Pandas Series from basic lists and Pandas DataFrames from basic dicts
- Some of the operators, functions, and methods which apply to basic Python containers also apply to Pandas containers such as the `del` operator, the `len()` function, and the `.pop()` method
- However because Pandas containers were designed for a very specific purpose, it is recommended to use the methods which come with them instead of those normally associated with basic Python containers

## Modifying Pandas Containers

- Sometimes our initial data isn't good enough and we need to do some manual cleaning or sculpting
- We will go through the following ways of manipulating an existing Pandas container:
	- Appending
	- Deleting
	- Reindexing
	- Sorting

### Appending to Pandas Containers

- We can append or add to existing Pandas Series using the `.concat()` method:

```python
import pandas as pd

phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

extra_phone_os = pd.Series(data=['iOS', 'iOS'], index=['Clint','Hank'])

print(pd.concat([phone_os,extra_phone_os]))
```

- The `.concat()` method also works for DataFrames:

```python
import pandas as pd

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

extra_survey_results = {'phone_os': ['iOS', 'iOS'], 'tiktok_ig': ['TikTok','Instagram']}

extra_survey_data = pd.DataFrame(data=extra_survey_results, index=['Clint','Hank'])

survey_data = pd.concat([survey_data,extra_survey_data])

print(survey_data)
```

- The above is an example of extending a Pandas DataFrame by adding more rows
- There are many ways to extend a Pandas DataFrame including adding an extra column or merging two Pandas DataFrames with a common index but different columns
- Adding an extra column can be done by assigning data to a column that doesn't exist yet: 

```python
survey_data['SHIELD'] = 'Not Sure'
print(survey_data)

survey_data['SHIELD'] = [True,True,True,False,False,True,True]
print(survey_data)
```

- The [official documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html) offers more complicated examples of extending and combining Pandas containers

### Deleting from Pandas Containers

- The `drop()` method is used to remove elements from Pandas containers
- On a basic level, it is used by providing the indices (for Series or if deleting rows from DataFrames) or columns to be removed:

```python
import pandas as pd

phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os.drop(labels=['Pepper','Thanos']))

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data.drop(labels=['Pepper','Thanos']))
print(survey_data.drop(labels='phone_os', axis=1))
```

### Reindexing

- Reindexing simply means to reorder the data based on which labels are used
- Both Series and DataFrames have the `.reindex()` method for this purpose

```python
import pandas as pd

phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os.reindex(index=['Hank','Tony','Natasha']))

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data.reindex(index=['Hank','Tony','Natasha'], columns=['phone_os','SHIELD']))
``` 
- Note that when reindexing DataFrames, both row and column labels can specified
- Also note that including new labels when reindexing Series and DataFrames results in a row or column filled with `NaN`, which indicates that the data does not exist
- As usual, the [official documentation](https://pandas.pydata.org/docs/user_guide/basics.html#reindexing-and-altering-labels) has more comprehensive information

## "Data Crunching" in Pandas

- Thus far we have explored several techniques for cleaning and shaping data which is arguably the most time-consuming part of data analysis
- Now we shall go through some "data-crunching" features of Pandas which allow us to actually process the data to obtain potentially useful results
- We shall focus on vectorization and alignment as well as some statistics-related features of Pandas

### Vectorization and Alignment

- In the early sessions, we used loops to do the same thing for each element of a container
- The Pandas module is built on the NumPy module, which was designed for array-based programming
- This basically means that instructions that run for simple data types such as numbers should also work for entire containers
- So this does not work for basic Python containers:

```python
print([1,2,3] + 2)
print((1,2,3) + 2)
```

- But it does work for Pandas containers:

```python
import pandas as pd

print(pd.Series([1,2,3]) + 2)
print(pd.DataFrame([1,2,3]) + 2)
```

- The actual programming implementation that allows this to work is called vectorization (the concept is called array-based programming, the programming construct is called vectorization)
- This is similar to working with vectors and matrices in mathematics; when a number is added to a vector or a matrix, it is assumed to be added to all elements of the vector or matrix
- So when basic operators are used with Pandas containers, they are generally applied to each element of the Pandas container
- This also applies to Boolean operators:

```python
import pandas as pd

print(pd.Series([1,2,3]) > 1)
print(pd.DataFrame([1,2,3]) > 1)
```

- Things can be more complex when functions are involved
- Operators usually take two inputs, with some operators like `not` taking only one and the one line `if ... else ...` taking three inputs
- Functions can in theory take as many inputs as required
- As programmers we then have to think about what the function is going to be applied to: Every element? Every row? Every column?
- Consider these examples using the basic `pow()` function, which takes raises the first argument to the power of the second argument:

```python
import pandas as pd

print(pow(pd.Series([1,2,3]),2))
print(pow(2,pd.DataFrame([1,2,3])))
```

- In the first example, all numbers in the Series were squares
- In the second example, the number two was raised to the power of each number in the DataFrame
- A more complicated example involves using the DataFrame's `apply()` method together with a function that takes any number of inputs:

```python
import pandas as pd

x = pd.DataFrame({'a': [1,2,3], 'b': [5,2,0]})

print(x.apply(sum, axis=0))
print(x.apply(sum, axis=1))
```

- The `apply()` method takes a function and applies it to every column or every row
- Together with the `sum()` function, it results in the sum of each row or column depending on the value of the `axis` function argument
- Try other functions like `max()` and `min()`
- Another aspect of vectorization in Pandas is alignment
- Pandas implements data alignment which basically means that an operation involving many different Pandas containers will involve elements that have the same labels
- Here is an example involving only Series:

```python
import pandas as pd

x = pd.Series([1,2,3], index=["a","b","c"])
y = pd.Series([3,2,1], index=["a","b","c"])
z = pd.Series([1,2,3], index=["d","b","c"])

print(x+x)
print(x+y)
print(x+z)
```

- Note that `x` does not have a "d" index and `z` does not have an "a" index
- The result of adding `x` and `z` is a Series with all indices from both but numbers only for indices that exist in both `x` and `z`

- We get a similar result when using only DataFrames:

```python
import pandas as pd

x = pd.DataFrame({'a': [1,2,3], 'b': [5,3,2], 'c': [7,8,9]})

print(x + x.iloc[0:2,0:2])
```

- As for operations involving both Series and DataFrames, by default the Series index is aligned with the DataFrame columns:

```python
import pandas as pd

x = pd.DataFrame({'a': [1,2,3], 'b': [5,3,2], 'c': [7,8,9]})
y = pd.Series([2,4,6], index=['a','b','c'])

print(x)
print(y)
print(x + y)
```

- More information on this can be found in the [official documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/dsintro.html#vectorized-operations-and-label-alignment-with-series)

### Statistics

- There is a very convenient `.describe()` method which provides summary statistics of a given Pandas container
- The [book](https://wesmckinney.com/book/pandas-basics.html#pandas_summarize) and [official documentation](https://pandas.pydata.org/docs/user_guide/basics.html#descriptive-statistics) give very readable summaries of what statistical or statistics-related information can be produced through Pandas
- One example of possible interest is the `.value_counts()` method, which lists all the unique values in a Pandas container as well as their respective frequencies:

```python
import pandas as pd

phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os.value_counts())

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data.value_counts())
```

- Note that when used directly with a DataFrame, the `.value_counts()` method will present frequencies based on the whole DataFrame
- To obtain a frequency table for each column in the DataFrame, the `.apply()` method can be used with the function version of `.value_counts()`:

```
import pandas as pd

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data.apply(pd.value_counts))
```

## Plotting with Pandas

- Pandas containers have the `.plot()` method which by default creates a line plot using the matplotlib module:

```python

```

- A single line plot will be produced if used with a Series and a single graph with multiple line plots will be produced if used with a DataFrame
- For DataFrames, the `.plot()` method can be used to produce scatter plots by giving the `x` and `y` arguments the relevant column names
- The [official documentation](https://pandas.pydata.org/docs/user_guide/visualization.html) shows that bar charts, pie charts, and other data visualizations can be produced in a similar manner, either by calling more specific methods such as `.plot.bar()` or by changing the `kind` argument in the `.plot()` method
- However as with matplotlib, remember that frequency amounts and labels must be generated first when making bar charts and pie charts
- This is where `.value_counts()` can help

```python

```

## Summary

- While basic Python operators, functions, and methods can work on Pandas containers, it is better to use those that come with/were designed specifically for Pandas
- Pandas allows us to modify existing containers and can help us process the data for analysis
- It helps to read the documentation on the two main Pandas containers - namely [Series](https://pandas.pydata.org/docs/reference/api/pandas.Series.html) and [DataFrames](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) - to fully appreciate what Pandas offers

## References

- https://wesmckinney.com/book/
- https://pandas.pydata.org/docs/user_guide/index.html

## Next Session

- R VS Python
- R Part 1