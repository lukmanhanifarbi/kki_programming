# Session 5

- Matplotlib

## Overview

- The focus of this session is on using the Matplotlib module
- The module's home page is at https://matplotlib.org

## An Example

- In the ["Quick Start Guide"][https://matplotlib.org/stable/tutorials/introductory/quick_start.html#coding-styles] we find that here are several style of using Matplotlib
- In this workshop we will focus on the "pyplot style" as in the [Pyplot Tutorial][https://matplotlib.org/stable/tutorials/introductory/pyplot.html] page: 

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4])
plt.ylabel('some numbers')
plt.show()
```

- Consider the following based on the code above:
    - As we have discussed in session 4, Matplotlib is not part of base Python and so the program needs to be told it is using an extra file(s) which contains the code we need
    - The `plot()` function Pyplot provides (note that it is `plt.plot()` and not just `plot()`) was given one list as its argument even though a plot has two axes, namely the x-axis and the y-axis
    - The plot can be modified by calling another Pyplot function, in this case `ylabel()`to change the title of the y-axis
    - The plot will appear in JupyterLab after using `plt.show()` but it is not saved to a file
- Pyplot has many functions that can be used to customize various parts of the diagram
- Here are some examples which build on the code above:

```python
import matplotlib.pyplot as plt

plt.plot(x=(0.5, 1.0, 1.5, 2,0),y=[1, 2, 3, 4])
plt.title('Example Plot)
plt.xlabel('some numbers')
plt.ylabel('some other numbers')
plt.axis(xmin=0, xmax, ymin=0, ymax)
plt.show()
```

- Other general customizations can be found at the [`matplotlib.pyplot`][https://matplotlib.org/stable/api/pyplot_summary.html] page; feel free to experiment
- There are more specific customizations which depend on the diagram to be produced
- We will discuss how Matplotlib can be used to generate the following basic diagrams:
    - Line graphs
    - Scatter diagrams
    - Pie charts
    - Bar charts

## Line Graphs

- Line graphs are diagrams in which x and y coordinates are connected by lines
- Line graphs are made using the `plot()` as before
- The x and y coordinates are specified in their own containers
- For example, if there are three data points (1,5), (3,0), and (5,3) then they should be organized as two separate containers with one for the x-axis (1,3,5) and another for the y-axis (5,0,3)

```python
import matplotlib.pyplot as plt

plt.plot(x=(1, 3, 5), y=[5,0,3])
plt.show()
```

- Note that this time we used keyword arguments to make sure pyplot receives our data correctly
- Technically, the `plot()` function takes in "NumPy arrays" which we will briefly discuss later
- The short version is that normal tuples and lists work just fine; Matplotlib takes care of the rest
- More information about the `plot()` function can be found at its [documentation page][https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html]
- This includes keyword arguments which allow you to customize the line graphs you make, for example:

```python
import matplotlib.pyplot as plt

plt.plot(x=(1, 3, 5), y=[5,0,3], color='', marker='', linestyle='', linewidth=, markersize=)
plt.show()
```

- This is similar to how line graphs are made in R
- The `plot()` function's documentation also recommends you go through [this page][https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html] for more keyword arguments related to customizing line graphs

## Scatter Plots

- Pyplot allows you to make scatter plots using the `scatter()` function
- It's basically the same as the `plot()` function except that it doesn't connect the points with lines
- Scatter plots are usually part of basic statistical analysis, especially correlation analysis

```python
import matplotlib.pyplot as plt

plt.scatter(x=(1, 3, 5), y=[5,0,3], color='', marker='', markersize=)
plt.show()
```

- More information about the `scatter()` function can be found at its [documentation page][https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html]

## Pie Charts and Bar Charts

 - Line graphs and scatter diagrams are useful for examining quantitative data
 - Different techniques are required for analyzing qualitative/categorical data
 - Pie charts and bar charts are two examples of diagrams which can be help
 - Bar charts help compare frequencies whereas pie charts help compare proportions
 - Let's say you surveyed 30 people asking whether or not people have programming experience and 20 replied 'Yes' whereas the rest replied 'No'
 - The following code generates bar and pie charts which reflect these results

```python
import matplotlib.pyplot as plt

plt.bar(x=['Yes', 'No'], height=[20,10])
plt.pie(x=[20,10], labels=['Yes','No'])
plt.show()
```

- More information about both functions can be found at their documentation pages, including how to better customize the diagrams; [this one][https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html] covers bar charts whereas [this one][https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html] covers pie charts

## Saving Diagrams

- Using `plt.show()` allows you to present your diagrams but you might lose them when you close JupyterLab
- Using `plt.savefig()` allows you to save your diagrams to a file for later use

```python
import matplotlib.pyplot as plt

plt.bar(x=['Yes', 'No'], height=[20,10])
plt.savefig(fname='barchart.png')
```

- Diagrams are saved as `.png` files by default but can be changed using the `format` keyword:

```python
import matplotlib.pyplot as plt

plt.bar(x=['Yes', 'No'], height=[20,10])
plt.savefig(fname='barchart.pdf', format='pdf')
```

- More information about the `savefig()` function can be found at its [documentation page][https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html]

## Summary

- We have learned the Pyplot style of using Matplotlib for generating diagrams
- Using Matplotlib begins with including it in your program through the following code `import matplotlib.pyplot as plt`
- We have used Matplotlib to generate line graphs, scatter plots, bar charts, and pie charts
- Matplotlib usually takes in NumPy arrays but regular tuples and lists should work as well

## References

- https://matplotlib.org/stable/tutorials/introductory/quick_start.html
- https://matplotlib.org/stable/tutorials/introductory/pyplot.html
- https://matplotlib.org/stable/api/pyplot_summary.html
- https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html
- https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html
- https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html
- https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html
- https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html

## Next Session

- Pandas Part 1