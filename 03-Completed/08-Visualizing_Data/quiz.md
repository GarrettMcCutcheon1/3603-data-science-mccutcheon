# 📝 Quiz: 08 - Visualizing Data

36 questions covering object-oriented Matplotlib, plotting with pandas, Seaborn distributions, Seaborn relationships and categories, and choosing and designing charts. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Matplotlib, Object-Oriented

**1.** (Short Answer) In `fig, ax = plt.subplots()`, what's the difference between `fig` and `ax`?

fig is the overall figure or canvas. ax is the individual axes where data, labels, titles and other chart elements are drawn.

**2.** (Short Answer) Why does the object-oriented style scale better than `plt.title()`/`plt.xlabel()` calls when a figure has several charts?

Object-oriented stle lets you customize each chart independently. With several charts, you can call methods on the specific ax you want instead of relying on pyplot's current active chart.

**3.** (Code Tracing) How many axes does this create, and how do you reach the bottom-right one?
```python
fig, axes = plt.subplots(2, 3)
```

It creates 6 axes, arranged in 2 rows and 3 columns. The bottom-right axes is axes[1, 2] because Python indexing starts at zero.

**4.** (Short Answer) What does `sharey=True` do, and why does it matter when comparing panels?

sharey=True makes the panels use the same y-axis scale. This matters because it lets you compare their heights and distributions fairly without different axis ranges making differences look larger or smaller.

**5.** (Short Answer) When is a log-scale axis a good idea? What value can't it show?

A log scale is useful when values span a very large range, especially when data is heavily skewed. It cannot dispaly zero or negative values.

**6.** (Multiple Choice) Which formatter displays `0.25` on an axis as `25%`?
A) `StrMethodFormatter('{x:.0%}')`  B) `PercentFormatter(xmax=1)`  C) `PercentFormatter(xmax=100)`  D) `ax.set(percent=True)`

B

**7.** (Short Answer) Why should you call `fig.savefig()` before `plt.show()`, and why `plt.close(fig)` inside a loop?

Save before plt.show() because some plotting environments may clear or close the figure when it is displayed. Inside a loop, plt.close(fig) releases the figure and its memory so many figures don't accumulate.

**8.** (Short Answer) In `ax.annotate('Peak', xy=(5, 10), xytext=(7, 12), arrowprops=...)`, what do `xy` and `xytext` each mean?

xy is the point being annotated. xytext is the position where the annotation text is placed.

---

## Section B — Plotting with Pandas

**9.** (Short Answer) When pandas plots a DataFrame, what becomes the x-axis, and what becomes each line or set of bars?

The DataFrame's index becomes the x-axis, and each column becomes a separate line or set of bars.

**10.** (Code Tracing) What kind of chart does this draw, and what are the bar labels?
```python
titanic['Embarked'].value_counts().plot.barh()
```

It draws a horizontal bar chart. The bar labels are the unique values in titanic['Embarked'] (typically C, Q, and S), and the bar lengths represent their passenger counts.

**11.** (Short Answer) You plot a `pivot_table` with classes as the index and sexes as the columns. How do you switch the chart to group by sex instead?

Transpose the pivot table using .T. This switches the index and columns, making sex the grouping on the x-axis.

**12.** (Short Answer) What does a 100% stacked bar chart show, and which `crosstab` argument produces the right table for it?

A 100% stacked bar chart shows the proportions of categories within each group, with each bar adding up to 100%. Use normalize='index' in pd.crosstab() to make each row add up to 1.

**13.** (Short Answer) What's the difference between wide and long data? Which does pandas `.plot` expect, and which does Seaborn expect?

Wide data has a separate column for each series or group. Long data has one column identifying the variable/group and another containing its values, with one row per observation. Pandas .plot works naturally with wide data; Seaborn expects long data.

**14.** (Short Answer) Should you sort the bars of an ordinal category (like ticket class) by value? Why or why not?

No. Ordinal categories have a meaningful natural order, such as 1st, 2nd, and 3rd class. Keep that order so the chart preserves the meaning of the categories. Sorting by value could hide that order.

---

## Section C — Seaborn: Distributions

**15.** (Short Answer) What's the difference between an axes-level and a figure-level Seaborn function? Give one example of each.

An axes-level function draws on one Matplotlib axes and can be placed into a specific subplot using ax=. Example: sns.histplot(). A figure-level function creates and manages an entire figure or grid of panels. Example: sns.displot().

**16.** (Short Answer) What does `hue='species'` do in `sns.histplot()`?

hue='species' separates the data by species and gives each species a different color, allowing you to compare their distributions on the same plot.

**17.** (Multiple Choice) Two groups have 500 and 50 rows. To compare the **shapes** of their distributions, use:
A) `stat='count'`  B) `multiple='stack'`  C) `stat='percent', common_norm=False`  D) `binwidth=1`

C

**18.** (Short Answer) Explain each part of a box plot: the box, the line inside it, the whiskers, and the dots.

Box: Represents the interquartile range (IQR), from the 25th percentile (Q1) to the 75th percentile (Q3).
Line inside: The median (50th percentile).
Whiskers: Extend to the most extreme data points still within the outlier fences (typically 1.5 × IQR beyond Q1 and Q3).
Dots: Individual outliers beyond those fences.

**19.** (Short Answer) Name one thing a violin plot shows that a box plot hides, and one thing a strip plot shows that a violin hides.

A violin plot shows the distribution's shape, including peaks and skewness, which a box plot hides. A strip plot shows every individual data point, which a violin plot does not.

**20.** (Short Answer) How do you read a group's median from an ECDF plot?

Find the point where the group's ECDF curve crosses 0.5 (50%) on the y-axis. The corresponding x-value is the median.

**21.** (True/False) A KDE curve always stays within the actual range of the data.

False

**22.** (Short Answer) Why does `showfliers=False` make sense when you draw a strip plot on top of a box plot?

showfliers=False prevents the box plot from drawing its own outlier dots. If a strip plot is placed on top, it already displays every individual point, so showing both would duplicate some dots.

---

## Section D — Seaborn: Relationships and Categories

**23.** (Short Answer) Name two ways to reduce overplotting in a scatter plot.

Two ways to reduce overplotting are:
Use transparency with alpha so overlapping points become visible.
Use smaller markers or add jitter so points are less likely to cover one another.

**24.** (Short Answer) In the penguins data, one `regplot` line through all the points slopes down, but one line per species slopes up. What's this called, and what's the lesson for fitting trend lines?

This is called Simpson's paradox. A trend seen in the combined data can reverse when the data is separated into groups. The lesson is to consider important grouping variables before interpreting or fitting a trend line.

**25.** (Short Answer) Why did the four Anscombe datasets get identical lines from `lmplot`?

The four Anscombe datasets were deliberately constructed to have nearly identical summary statistics, including means, variances, correlations, and linear regression results. Therefore, lmplot produces the same fitted line for each dataset, even though their actual point patterns are very different. This demonstrates why you should visualize data instead of relying only on summary statistics.

**26.** (Short Answer) What's the difference between `countplot` and `barplot`?

countplot counts how many observations belong to each category. barplot calculates and displays a numerical statistic (the mean by default) for each category, along with error bars.

**27.** (Multiple Choice) `sns.barplot(..., errorbar='sd')` draws error bars showing:
A) the 95% confidence interval  B) the standard error  C) one standard deviation of the individual values  D) the IQR

C

**28.** (Short Answer) What does Seaborn's default error bar on a `barplot` represent?

Seaborn's default barplot error bar represents a 95% confidence interval for the estimated mean, calculated using bootstrapping by default. It shows uncertainty in the estimated mean, not the spread of individual observations.

**29.** (Short Answer) What does a `pointplot` with crossing or diverging lines tell you?

Crossing or diverging lines suggest that the relationship between two variables changes depending on the group. This can indicate an interaction effect: the effect of one category or condition is different for different groups.

**30.** (Short Answer) Should a correlation heatmap use a diverging or a sequential color map? What about a heatmap of survival rates? Why?

A correlation heatmap should use a diverging color map because correlations range from -1 to +1, with zero as the meaningful midpoint. A survival-rate heatmap should generally use a sequential color map because survival rates go from low to high, without a meaningful negative direction.

---

## Section E — Choosing and Telling

**31.** (Short Answer) Why must bar charts start at zero, when line charts don't have to?

Bar charts represent values using the lengths of bars, so starting above zero can exaggerate differences. Line charts show changes and trends between points, so they can use a narrower y-axis range as long as the scale is clearly labeled.

**32.** (Short Answer) Name the chart you'd choose for each: (a) the distribution of one numeric column, (b) the mix of categories within each group, (c) the relationship between two numeric columns.

a) Histogram
b) 100% stacked bar chart
c) Scatter plot

**33.** (Short Answer) What's a palette dictionary, and why use one across a whole report?

A palette dictionary assigns a specific color to each category. Using the same dictionary throughout a report keeps each category's color consistent, making charts easier to compare.

**34.** (Short Answer) Rewrite this descriptive title as a finding title: "Mean Body Mass by Species."

One possible finding title is: "Gentoo Penguins Have the Highest Mean Body Mass."

**35.** (True/False) Every bar in a bar chart should have its own distinct color.

False

**36.** (Short Answer) Give two reasons to look at a chart **and** the matching numbers, rather than just one of them.

A chart makes patterns, trends, clusters, and outliers easier to recognize than a table of numbers.
The matching numbers provide exact values and help verify that the visual impression is accurate. A chart can make a difference look large or small depending on its scale.