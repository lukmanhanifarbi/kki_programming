# Session 6

## Overview

- We have learned enough programming concepts to manually perform data analysis using Python
- However, the Python community has developed modules which make it easier to perform data analysis
- Pandas is one such module and it shall be the focus of this session
- We will be using the online, "Open Access" version of [Python for Data Analysis](https://wesmckinney.com/book/) as the main reference for this section as it was written by the main author of Pandas
- We shall also refer to the [official documentation](https://pandas.pydata.org/docs/user_guide/index.html) which is usually more comprehensive
- This topic has been split into two, with this first part focusing on creating and subsetting Pandas containers
- The second part will cover operations on Pandas containers

## Pandas Containers

- Pandas offers two data containers, Series and DataFrames
- Series are basically lists with customizable indices:

```
import pandas as pd

phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os[2:5])
print(phone_os['Bruce', 'Natasha', 'Tony'])
```

- If no custom indices are given, the normal numerical indices will be used like with normal Python lists e.g. `print(phone_os[2])`
- These indices can be accessed and modified later using the `index` attribute:

```
print(phone_os.index)
phone_os.index = ['Iron Man', 'Black Widow', 'The Hulk', 'Pepper Potts', 'Thanos']
print(phone_os.index)
```

- DataFrames are like data tables with column headers and row labels:

```
import pandas as pd

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data)
```

- Each column is a Pandas Series, therefore indexing a specific column will return it as a Pandas Series e.g. print(survey_data['phone_os'])
- The row indices can be listed using the `index` attribute while the column headers can be listed using the `column` attribute:

```
print(survey_data.index)
print(survey_data.columns)
```

## Creation of Pandas Containers

- We have seen above that the `Series()` function creates series and the `DataFrame()` function creates DataFrames
- As also shown in the code above, the `DataFrames()` function usually takes in a dictionary of lists or similar containers along with custom indices if necessary
- A special case is when a dictonary of dictionaries (or _nested_ dictionaries) are passed into the `DataFrames()` function
- The "inner" keys become the row indices and the "outer" keys become the column headers:

```
import pandas as pd

survey_results = {'phone_os': {'Tony': 'Android', 'Natasha': 'iOS', 'Bruce': 'iOS', 'Pepper': 'Android', 'Thanos': 'Android']}, 'tiktok_ig': {'Tony': 'Instagram', 'Natasha': 'Instagram', 'Bruce': 'TikTok', 'Pepper': 'Instagram', 'Thanos': 'TikTok'}}

survey_data = pd.DataFrame(data=survey_results)

print(survey_data)
```

- Go through [this](https://wesmckinney.com/book/pandas-basics.html#table_dataframe_constructor) and [this](https://pandas.pydata.org/docs/user_guide/dsintro.html) to see other ways of preparing Series and DataFrames
- Naturally, Pandas also has a way of importing data into a DataFrame:

```
survey_data = pd.read_csv('survey.csv', sep=';')
```

- Similarly, Pandas DataFrames can be saved to files:

```
survey_data.to_csv('data.csv')
```

- The [sixth chapter](https://wesmckinney.com/book/accessing-data.html) of the book covers topics related to loading and saving data using Pandas

## Subsetting Pandas Containers

- _Subsetting_ basically means to get a more specific amount of data from a dataset
- Examples we have covered including selecting data in lists and dictionaries
- The [official documentation](https://pandas.pydata.org/docs/user_guide/indexing.html) explains that there are three main approaches for selecting data in Pandas containers: 
1. Selection by Position
2. Selection by Label
3. Selection by Callable

- We will only cover the first two as well as some additional approaches explained in the official documentation

### Selection by Position

- Selection by position is very similar to how we select data in lists
- As we have seen, this is straightforward for Pandas Series:

```python
phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os[2:5])
```

- It is basically the same as selecting data in lists
- However, it is more complicated for DataFrames
- Consider the DataFrame we have previously used:

```
survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])
```

- Using only one number e.g. `print(survey_data[2])` is not accepted, but using a range or slice returns the related rows from a DataFrame e.g. `print(survey_data[0:5])` or `print(survey_data[0:5:2])`
- The main way of selecting by position is by using `.iloc[]` which can take up to two positional inputs:
1. If only one input is given, the relevant rows will be selected
2. If two inputs are given, the first input will be interpreted as the rows and the second will be interpreted as the columns
- Try the following examples:

```
print(survey_data.iloc[[3,4,1]])
print(survey_data.iloc[0:5:2,0])
print(survey_data.iloc[:,0])
print(survey_data.iloc[0:5:2,:])
```

### Selection by Label

- Selection by label is like selecting data in dictionaries
- This is also straightforward for Pandas Series:

```python
phone_os = pd.Series(data=['Android', 'iOS', 'iOS', 'Android', 'Android'], index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(phone_os['Tony', 'Thanos'])
```
- For Pandas DataFrames, this selects columns
- Selection by label can also be done using `.loc[]`
- Consider the following examples:

```
print(survey_data.loc[['Bruce','Natasha','Thanos']])
print(survey_data.loc['Bruce':'Thanos'])
print(survey_data.loc['Bruce':'Thanos','phone_os'])
print(survey_data.loc['Bruce':'Thanos',:])
```

### Boolean Indexing

- It can be useful to select data which match certain criteria
- This is done using Boolean operators in the following manner, called Boolean indexing:

```
print(survey_data[survey_data['phone_os'] =='Android'])
print(survey_data[~(survey_data['phone_os'] =='Android']))
print(survey_data[(survey_data['phone_os'] =='Android') & (survey_data['tiktok_ig'] == 'IG')])
print(survey_data[(survey_data['phone_os'] =='Android') | (survey_data['tiktok_ig'] == 'IG')])
```

- Note that each individual criterion is surrounded by brackets to prevent misinterpretation
- Also note that `~` is used for 'not', `&` is used for 'and', and `|` is used to for 'or'
- Note that the index itself is like a list of Boolean values
- This means that we can save this list of Boolean values and use it later with the Series or DataFrame to make our code easier to read:

```
custom_index = (survey_data['phone_os'] =='Android') | (survey_data['tiktok_ig'] == 'IG')

print(survey_data[custom_index])
```

- Pandas has many functions which "test" whether the data satisfies certain criteria aside from the basic comparison operators
- The `.isin()` method tests whether or not each element of a Pandas container is also included in another container:

```python
import pandas as pd

healthy_food = ['caesar salad','chicken steak','quinoa wrap', 'tomato soup']

todays_food = pd.Series(['ice cream','tomato_soup','popcorn'], index=['breakfast','lunch','dinner'])

print(todays_food.isin(healthy_food))
print(todays_food[todays_food.isin(healthy_food)])

food_diary = pd.DataFrame({'monday': ['fried chicken','cheese burger','pizza'], 'tuesday': ['instant noodles','caesar salad','ice cream'], 'wednesday': ['ice cream','tomato_soup','popcorn']}, index=['breakfast','lunch','dinner'])

print(food_diary.isin(healthy_food))
print(food_diary[food_diary.isin(healthy_food)])
```

- The `.query()` method only works for DataFrames and selects the rows that fulfil a certain criteria (instead of just returning a Pandas container filled with Boolean values):

```
import pandas as pd

survey_results = {'phone_os': ['Android', 'iOS', 'iOS', 'Android', 'Android'], 'tiktok_ig': ['Instagram','Instagram','TikTok','Instagram','TikTok']}

survey_data = pd.DataFrame(data=survey_results, index=['Tony','Natasha','Bruce','Pepper','Thanos'])

print(survey_data.query('(phone_os == "Android") & (tiktok_ig == "TikTok")'))
```

- Note that the `.query()` method accepts a string and so the words "Android" and "TikTok" have to use double quotes

### Sampling

- Sometimes we only wish to work with a random sample of our data
- The `.sample()` method can be used for this whether for Series or DataFrames:

```
print(survey_data.sample())
print(survey_data.sample(n=3))
print(survey_data.sample(n=3, replace=True))
print(survey_data.sample(n=3, axis=0))
print(survey_data.sample(n=3, axis=1))
print(survey_data.sample(n=3, replace=True, axis=1))
```

## Duplicate Labels

- Pandas allows duplicate labels even though this can cause problems
- It helps to check your data has no duplicates using `.is_unique`:

```python
import pandas as pd

todays_food = pd.Series(['ice cream','tomato_soup','popcorn'], index=['breakfast','lunch','dinner'])

print(todays_food.index.is_unique)

food_diary = pd.DataFrame({'monday': ['fried chicken','cheese burger','pizza'], 'tuesday': ['instant noodles','caesar salad','ice cream'], 'wednesday': ['ice cream','tomato_soup','popcorn']}, index=['breakfast','lunch','dinner'])

print(food_diary.index.is_unique)
print(food_diary.columns.is_unique)
```

## Views VS Copies

- We conclude this session with a warning
- Sometimes, subsetting a DataFrame and then storing it into a variable creates a **copy** and other times it is simply a **view**
- Working with a copy does not change the original DataFrame whereas working with a view does
- [This](https://stackoverflow.com/questions/23296282/what-rules-does-pandas-use-to-generate-a-view-vs-a-copy) and [this](https://realpython.com/pandas-settingwithcopywarning/) give ideas of when a copy is created and when a view is created
- Be safe and keep copies of your original DataFrame to make sure it isn't lost

## Summary

 - Pandas offers two main data containers, namely Series and DataFrames
 - These can be manually created or based on imported data
 - There are three main ways to subset data stored in Pandas containers, namely by position, by label, and by callable
 - We also discussed Boolean indexing and how we can take random samples from Pandas data containers
 - Keep copies of your original data so that it isn't lost

## References

- https://wesmckinney.com/book/
- https://pandas.pydata.org/docs/user_guide/index.html
- https://stackoverflow.com/questions/23296282/what-rules-does-pandas-use-to-generate-a-view-vs-a-copy
- https://realpython.com/pandas-settingwithcopywarning/

## Next Session

- Pandas Part 2