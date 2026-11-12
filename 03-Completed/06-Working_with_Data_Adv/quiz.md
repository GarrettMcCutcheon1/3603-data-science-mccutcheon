# 📝 Quiz: 06 - Working with Data (Advanced)

47 questions covering Pandas Series/DataFrames, loading/exploring data, indexing/selection, cleaning, column operations, sorting/filtering/searching, grouping and combining tables, and a "going further" bonus. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first — the Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Series and DataFrames

**1.** (Short Answer) What's the difference between a Pandas `Series` and a `DataFrame`?

A Series is a one-dimensional labeled array, while a DataFrame is a two-dimensional table containing rows and columns.

**2.** (Code Tracing) What prints?
```python
s = pd.Series({'a': 1, 'b': 2})
print(s['a'])
```

1

**3.** (Short Answer) What does `df.shape` return?

df.shape returns a tuple containing the number of rows and columns in df.

**4.** (Short Answer) If you add two `Series` together and one has a label the other doesn't, what happens at that label?

The result at that label becomes NaN because one Series is missing a value for that label.

**5.** (Short Answer) You have a list of dictionaries, one per student (the way you stored records in Module 03b). What does `pd.DataFrame(that_list)` turn each dictionary into?

Each dictionary becomes a row, and the dictionary keys become column names. Values become row data.

**6.** (Code Tracing) What prints?
```python
scores = pd.Series([70, 95, 88])
print(scores[scores > 80].tolist())
```

[95, 88]

---

## Section B — Loading and Exploring Data

**7.** (Multiple Choice) Which method shows summary statistics (mean, std, min/max) for numeric columns?
A) `.head()`  B) `.columns`  C) `.describe()`  D) `.shape`

C

**8.** (Short Answer) What's the difference between what `.head()` and `.info()` each tell you about a DataFrame?

.head() displays the first five rows. .info() displays column names, data types, non-null counts, and memory usage.

**9.** (Short Answer) How do you count how many missing values are in *each column* of a DataFrame?

Use df.isnull().sum()

**10.** (Short Answer) What do `df.duplicated().sum()` and `df['col'].value_counts(dropna=False)` each tell you?

df.duplicated().sum() counts rows that are duplicates of previous rows.
df['col'].value_counts(dropna=False) counts how often each unique value appears, which includes missing values.

**11.** (Short Answer) Titanic's `Age` column holds whole numbers, but its dtype is `float64`. Why?

Missing ages require a data type that supporsts decimals, so Pandas uses float64 even though the actual ages are integers.

---

## Section C — Indexing and Selection

**12.** (Short Answer) What's the difference between `.loc[]` and `.iloc[]`?

.loc[] selects rows/columns using labels.
.iloc[] selects rows/columns using integer positions.

**13.** (Short Answer) Is `df.loc[0:4]` inclusive or exclusive of row `4`? What about `df.iloc[0:4]` and position `4`?

df.loc[0:4] includes row 4, while df.iloc[0:4] excludes 4.

**14.** (Short Answer) What symbols does Pandas require for combining conditions when filtering a DataFrame (instead of the `and`/`or` keywords)?

Use & for AND, | for OR, and ~ for NOT. Each condition must be enclosed in parantheses.

**15.** (Short Answer) What does `df[df['Age'] < 10]` return?

It returns a dataframe containing only rows where the value in the Age column is less than 10.

**16.** (Short Answer) Rewrite `df[(df['Embarked'] == 'C') | (df['Embarked'] == 'Q')]` using `.isin()`. Does `df['Age'].between(13, 19)` include ages 13 and 19?

df[df['Embarked'].isin(['C', 'Q'])]
Yes; .between(13,19) includes both 13 and 19.

**17.** (Multiple Choice) Which one returns a `DataFrame` rather than a `Series`?
A) `df['Age']`  B) `df[['Age']]`  C) `df.Age`  D) `df.loc[0]`

B

**18.** (Short Answer) After `by_id = df.set_index('PassengerId')`, what does `by_id.loc[2]` select, and how is that different from `df.loc[2]`?

by_id.loc[2] selects the passenger whose PassengerId is 2. df.loc[2] selects the row with index label 2.

**19.** (Code Tracing) After `by_id = titanic.set_index('PassengerId')`, do `by_id.loc[3]` and `by_id.iloc[3]` select the same passenger? Why or why not?

No; by_id.loc[3] selects the passenger with ID 3, while by_id.iloc[3] selects the fourth row by position.

**20.** (Short Answer) Write a filter for passengers who did **not** board at Southampton (`'S'`), using `~` and `.isin()`.

df[~df['Embarked'].isin(['S'])]

**21.** (Short Answer) What's wrong with `df[df['Age'] < 10]['child'] = True`, and what should you write instead?

Chained assignment may not modify the original DataFrame reliably. Use:
df.loc[df['Age'] < 10, 'child'] = True

---

## Section D — Cleaning

**22.** (Short Answer) What's the difference between `.dropna()` and `.fillna()`?

.dropna() removes rows or columns containing missing values, while .fillna() replaces missing values with a specified value.

**23.** (Short Answer) What does `pd.to_numeric(col, errors='coerce')` do to a value like `'ninety'` in that column?

It converts 'ninety' into NaN because it cannot be converted into a number

**24.** (True/False) `NaN` and an empty string `""` are always treated identically by `.isnull()`.

False

**25.** (Short Answer) Two rows have the same `order_id` but different `amount`s. Does `df.drop_duplicates()` remove one of them? What would you write to keep only the last row for each `order_id`?

No; since the amount values differ, the entire rows are not duplicates. Use:
df.drop_duplicates(subset=['order_id'], keep='last')

**26.** (Short Answer) A survey stores missing ages as `-1`. Why is that a problem for `df['age'].mean()`, and how do you fix it?

The -1 values are included in the average and artificially lower it. Replace them with missing values first:
df['age'] = df['age'].replace(-1, np.nan)

**27.** (Short Answer) A date column holds `'2022-01-01'`, `'2022/03/01'`, and `'April 5, 2022'`. Why can `pd.to_datetime(col, errors='coerce')` turn two perfectly valid dates into `NaT`, and how do you fix it?

Pandas may infer a date format from the first values and reject other formats that don't match it. Specify the appropriate format for each group of dates or normalize the strings before converting them.

**28.** (Short Answer) Why does `.astype('int64')` fail on a column with missing values, while `.astype('Int64')` works?

Standard int64 cannot store missing values (NaN), while Pandas nullable Int64 can store integers and missing values (pd.NA).

**29.** (Short Answer) Before deleting rows with a repeated `order_id`, why would you look at `df[df.duplicated(subset=['order_id'], keep=False)]` first?

I would look at df[df.duplicated(subset=['order_id'], keep=False)] first to inspect all rows sharing a repeated order_id before deleting anything. This helps determine whether they are actual duplicates or legitimate records with different information.

---

## Section E — Column Operations, Sorting, Filtering, and Searching

**30.** (Short Answer) How do you create a new column that's the sum of two existing numeric columns?

df['total'] = df['col1'] + df['col2']

**31.** (Short Answer) What does `.apply()` do that you could also do with a `for` loop over rows — and why is `.apply()` usually preferred?

.apply() runs a function on rows or columns to perform calculations or transformations. It is more concise and integrates better with Pandas than manually looping through rows.

**32.** (Short Answer) What does `ascending=False` do inside `df.sort_values(by='score', ascending=False)`?

It sorts values from highest to lowest instead of lowest to highest.

**33.** (Short Answer) What's the main advantage of `.query()` over bracket-based boolean filtering (`df[df['col'] > 5]`)?

.query() is easier to read, especially for complex conditions.

**34.** (Code Tracing) `bonus` is a brand-new column. What value do the rows with `score >= 80` get in it?
```python
df.loc[df['score'] < 80, 'bonus'] = 5
```

Rows with score >= 80 receive no assigned value from this line. Since bonus is a new column, those rows will contain NaN.

**35.** (Short Answer) To compute `price * qty` for every row, why should you write `df['price'] * df['qty']` instead of looping with `.iterrows()`? When *is* a loop (preferably `.itertuples()`) the right tool?

Vectorized operations such as df['price'] * df['qty'] are faster and more efficient than iterating through individual rows. 
Loops are useful when performing complicated operations that cannot easily be expressed using vectorized Pandas operations.

**36.** (Short Answer) What do `case=False` and `na=False` each do in `df['name'].str.contains('an', case=False, na=False)`?

case=False makes the search case-insensitive.

na=False treats missing values as False instead of returning missing results.

**37.** (Code Tracing) A student has `math = 95` and `average = 91`. What is their `award` after these three lines, and what would it be if the last two lines were swapped?
```python
df['award'] = 'None'
df.loc[df['average'] >= 85, 'award'] = 'Honor Roll'
df.loc[df['math'] >= 90, 'award'] = 'Math Star'
```

The award is 'Math Star' because the last assignment overwrites the previous one.
If the last two lines are swapped, the award becomes 'Honor Roll' because that assignment happens last.

**38.** (Short Answer) What does `pd.cut(df['score'], bins=[0, 70, 90, 101], labels=['Low', 'Mid', 'High'], right=False)` do, and why is it usually better than `.apply()` with an `if`/`elif` function for the same job?

Divides scores into three categories: 0–69: Low, 70–89: Mid, 90–100: High
right=False makes the intervals left-inclusive and right-exclusive. .cut() is faster and more efficient because it uses vectorized operations instead of calling a Python function on each row.

**39.** (Short Answer) What's the difference between `df.query('math_score >= minimum')` and `df.query('math_score >= @minimum')`?

Without @, Pandas looks for a column named minimum.
With @, Pandas uses the Python variable named minimum.

**40.** (Code Tracing) What does each line return, and why are they different?
```python
books = pd.Series(['C++ Primer', 'C Programming'])
books.str.contains('C++').tolist()
books.str.contains('C++', regex=False).tolist()
```

[False, False]

[True, True]

The first uses regular expressions, where + has a special meaning (one or more repetitions). The second treats 'C++' as literal text because regex=False.

---

## Section F — Grouping and Combining

**41.** (Code Tracing) What does this return?
```python
df = pd.DataFrame({'team': ['A', 'B', 'A', 'B'], 'points': [10, 4, 20, 6]})
df.groupby('team')['points'].mean()
```

team
A    15.0
B     5.0

**42.** (Short Answer) Write a `groupby` with `.agg()` that gives, for each `team`, the number of rows and the total `points`, as columns named `games` and `total`.

df.groupby('team').agg(
    games=('points', 'count'),
    total=('points', 'sum')
)

**43.** (Short Answer) When would you use `pd.concat()` instead of `.merge()`? What does `ignore_index=True` do?

Use pd.concat() to stack DataFrames vertically or horizontally. Use .merge() to combine DataFrames based on matching columns or keys.

ignore_index=True creates a new sequential index instead of keeping the original indexes.

**44.** (Short Answer) In `orders.merge(prices, on='product_id', how='left')`, what happens to an order whose `product_id` isn't in `prices`? What would `how='inner'` do instead? And why does a merge on state codes fail when one table uses `'tx'` and the other uses `'TX'`?

how='left': Keeps the order, but unmatched products receive NaN for their price information.
how='inner': Keeps only orders with matching products in both tables.
'tx' and 'TX' don't match because string comparisons are case-sensitive.

**45.** (Short Answer) In Titanic, `groupby('Pclass').size()` gives 216 for 1st class, but `groupby('Pclass')['Age'].count()` gives 186. Why are they different?

.size() counts every row, while .count() counts only non-missing values in the Age column. The difference is caused by passengers with missing ages.

**46.** (Short Answer) `purchases` has 6 rows. After `purchases.merge(buyers, on='buyer_id', how='left')`, it has 8. What probably happened, and how can `validate=` protect you?

Some buyer_id values probably appear multiple times in the buyers DataFrame. This creates multiple matches for a single purchase. validate= checks that each buyer id matches at most one row in buyers.

---

## Section G — Going Further (Bonus)

**47.** (Short Answer) What do the `usecols` and `nrows` arguments to `pd.read_csv()` do, and when would you reach for them?

usecols selects only specific columns to load from a CSV.
nrows limits how many rows are loaded.
These are useful when working with large datasets, and you only need certain columns or a smaller sample of the data.