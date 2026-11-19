# 📝 Quiz: 07 - Describing Data

36 questions covering types of data, center and spread, shape and outliers, comparing groups, and relationships and correlation. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Types of Data

**1.** (Short Answer) What's the difference between a column's **dtype** and its **measurement scale**?

A column's dtype is how the data is stored in Python, while its measurement scale is what the data repreesnts and how it can be compared.

**2.** (Multiple Choice) Titanic's `Pclass` is stored as `1`, `2`, `3`. Its measurement scale is:
A) Nominal  B) Ordinal  C) Interval  D) Ratio

B

**3.** (Multiple Choice) Which scale has a true zero that means "none of it"?
A) Nominal  B) Ordinal  C) Interval  D) Ratio

D

**4.** (True/False) Temperature in °C is ratio data, because 20°C is twice 10°C.

False

**5.** (Short Answer) Is "number of siblings aboard" discrete or continuous? How can you tell?

Discrete; it is counted in whole numbers rather than measured along a range.

**6.** (Code Tracing) What prints?
```python
s = pd.Series([True, False, True, True])
print(s.mean())
```

0.75

**7.** (Short Answer) Why is `titanic['PassengerId'].mean()` meaningless, even though pandas computes it without complaint?

PassengerIDs are identifiers and not measurements. Finding their average does not provide any useful data.

**8.** (Short Answer) What does `ordered=True` in `pd.CategoricalDtype([...], ordered=True)` let you do that a plain `str` column can't?

It allows pandas to recognize and use the catory's natural ordering for comparisons and sorting.

---

## Section B — Center and Spread

**9.** (Short Answer) Which is more robust to outliers, the mean or the median? Why?

The median because it represents the middle value and is not significantly affected by extremely large or small values.

**10.** (Code Tracing) What prints?
```python
s = pd.Series([2, 4, 4, 6, 100])
print(s.median(), s.mode()[0])
```

4.0 4

**11.** (Short Answer) A column's mean is much larger than its median. What does that suggest?

That suggests that the data is strongly right-skewed. A few unusually large values are pulling the mean up.

**12.** (Multiple Choice) `pd.Series(data).std()` and `np.std(data)` give slightly different answers because:
A) NumPy rounds  B) pandas skips NaN  C) they use different default `ddof`  D) one is variance

C

**13.** (Short Answer) What's the IQR, and how do you compute it in pandas?

The interquartile range (IQR) measures the spread of the middle 50% of the data. 
IQR = df['column'].quantile(0.75) - df['column'].quantile(0.25)

**14.** (Short Answer) In `.describe()`, a column's `count` is 714 but the DataFrame has 891 rows. What does that tell you?

There are 177 missing values in that column because count only includes non-missing values.

**15.** (Short Answer) You fill 177 missing ages with the median age. What happens to the standard deviation, and why?

The standard deviation generally decreases because the missing values are replaced with the same middle value, reducing the overall spread of the data.

**16.** (Short Answer) Which spread statistic pairs naturally with the median, and which with the mean?

Median pairs with IQR.
Mean pairs with standard deviation.

---

## Section C — Shape and Outliers

**17.** (Multiple Choice) A column with `.skew()` of 4.8 is:
A) roughly symmetric  B) strongly left-skewed  C) strongly right-skewed  D) heavy-tailed but symmetric

C

**18.** (Short Answer) Write the formulas for the lower and upper fences of the 1.5 × IQR rule.

Lower = Q1 - 1.5(IQR)
Upper = Q3 + 1.5(IQR)

**19.** (Short Answer) On Titanic fares, the IQR rule flags 116 values but the |z| > 3 rule flags only 20. Why are z-scores less sensitive on a skewed column?

Z-scores use the mean and standard deviation, which are affected by extreme values. Large values increase the standard deviation, making other unusual values appear less extreme.

**20.** (True/False) Any value flagged as an outlier should be removed before analysis.

False

**21.** (Short Answer) Name two things you can do with a real-but-extreme value instead of deleting it.

Keep the value but use robust statistics, such as the median and IQR.
Apply a transformation, such as a logarithmic transformation, to reduce its influence.

**22.** (Short Answer) Why can a value be an outlier within its group but not in the whole dataset (or the other way around)?

Different groups can have different distributions, averages, and spreads. A value that is normal across the entire dataset might be unusual within a particular group.
---

## Section D — Comparing Groups

**23.** (Short Answer) More 3rd-class passengers survived than 2nd-class passengers, but 3rd class had the lower survival rate. How can both be true?

Both can be true because 3rd-class had more passengers overall. Even if fewer survived proportionally, the larger group still ended up with a greater total number of survivors.

**24.** (Code Tracing) What does this compute?
```python
titanic.groupby('Sex')['Survived'].mean()
```

It calculates the survival rate for each sex.

**25.** (Multiple Choice) In `pd.crosstab(df['class'], df['Sex'], normalize='index')`, what adds up to 100%?
A) each row  B) each column  C) the whole table  D) nothing; it's counts

A

**26.** (Short Answer) What's the difference between what `pd.crosstab()` and `pivot_table()` compute?

pd.crosstab() primarily creates frequency tables showing how often combinations of categories occur.
pd.pivot_table() summarizes numerical data using an aggregation function such as mean, sum, or count.

**27.** (Short Answer) Why should a group summary always include the group's size?

Because the sample size helps determine how reliable or representative the results are. A percentage based on 5 people is less reliable than one based on 500 people.

**28.** (Short Answer) Cherbourg passengers survived at a higher rate than other ports. Explain how ticket class could be a **confounder** here.

Ticket class could influence both the port passengers departed from and their chances of survival.
Cherbourg had a higher proportion of first-class passengers, who had higher survival rates. This artificially makes it look like passengers from Cherbourg have a higher survival rate.

**29.** (Short Answer) What does `observed=True` do in a `groupby` on a categorical column?

It tells pandas to include only categories that actually appear in the data rather than also including unused categorical levels.

---

## Section E — Relationships and Correlation

**30.** (Short Answer) Why is covariance hard to interpret on its own, and how does correlation fix that?

Covariance depends on the units and scales of the variables, making its magnitude difficult to interpret.
Correlation standardizes covariance into a value between -1 and +1, making relationships easier to compare.

**31.** (Multiple Choice) r = −0.85 means:
A) a weak negative linear relationship  B) a strong negative linear relationship  C) 85% of y is caused by x  D) no relationship

B

**32.** (Short Answer) Give two situations where Spearman is a better choice than Pearson.

When the relationship is monotonic but not necessarily linear.
When the data contains significant outliers or is ordinal/rank-based.

**33.** (True/False) If r = 0, the two columns have no relationship at all.

False

**34.** (Short Answer) Name three explanations for a correlation besides "A causes B."

Reverse causation: B causes A.
Counfounding variable: A third variable influences both A and B.
Coincidence: The correlation is random, and there is no meaninful relationship.

**35.** (Short Answer) What is Anscombe's quartet, and what lesson does it teach?

Anscombe's quartet is a collection of four datasets that have nearly identical statistical properties (mean, variance, correlation, and linear regression results) but look very different when graphed.

The lesson is that visualizing data is important because summary statistics alone can hide patterns, outliers, and nonlinear relationships.

**36.** (Short Answer) In the penguins data, bill length and depth correlate at −0.24 overall but +0.39 to +0.65 within each species. What's this called, and what causes it here?

This is an example of Simpson's paradox.
When all penguin species are combined, differences in average bill size between species create an overall negative correlation. 
However, within each individual species, bill length and depth have a positive correlation.