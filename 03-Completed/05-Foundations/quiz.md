# 📝 Quiz: 05 - Foundations

45 questions covering all 8 Foundations notebooks, in order: magic commands, Jupyter workflow, getting help, Markdown, files and paths, data I/O, plotting with NumPy, and timing. Mix of multiple choice, true/false, code-tracing, and short answer.

This is a conceptual self-check. For hands-on practice writing and running real code, see `Foundations_Quiz.ipynb` in this folder.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Magic Commands (01)

**1.** (Multiple Choice) Which magic command shows your current working directory?
A) `%pwd`  B) `%cd`  C) `%ls`  D) `%dir`

A

**2.** (Short Answer) What's the difference between a line magic (`%pwd`), a cell magic (`%%writefile`), and a shell command (`!ls`)?

A line magic runs a command on a single line.
A cell magic applies a comand to a whole cell.
A shell command runs a command in the system shell.

**3.** (Code Tracing) A folder contains only `a.csv` and `b.txt`. What kind of value is stored in `files`, and what does it contain?
```python
files = !ls
```
'files' stores a kind of list IPython result containing two strings a.csv and b.txt.

**4.** (True/False) `%cd ..  # go up one folder` moves you to the parent folder.

True

**5.** (Short Answer) Inside a notebook, why should you install packages with `%pip install` instead of `!pip install`?

%pip install only installs packages into the python environment used by the current notebook kernel.

**6.** (True/False) `%who` only shows variable *names*, while `%whos` also shows their types and a value summary.

True

---

## Section B — Jupyter Workflow (02)

**7.** (Multiple Choice) In Command mode, which keyboard shortcut inserts a new cell *below* the current one?
A) `A`  B) `B`  C) `D D`  D) `M`

B

**8.** (Short Answer) What's the practical difference between Command mode and Edit mode? You press `B` and the letter "b" appears in your code. What happened, and what should you press?

Command mode is used for editing the notebook, while edit mode is used to edit specific cells.

**9.** (Code Tracing) What does this cell display when it runs?
```python
x = 5
x * 2
x * 3
```

15

**10.** (Short Answer) A cell near the bottom of a notebook shows `[7]`, and the cell above it shows `[9]`. What does that tell you?

The cells have been executed out of order with the bottom cell being executed before the cell above it.

**11.** (True/False) If you delete the cell that created the variable `message`, `message` is removed from memory immediately.

False

**12.** (Short Answer) Why should you **Restart & Run All** before submitting a notebook?

You should restart and run all because it ensures that the notebook works correctly from beginning to end. 
It also verifies that the cells aren't just working because they have been run in a specific order.

---

## Section C — Getting Help (03)

**13.** (Short Answer) `?` shows a docstring. What does `??` sometimes show that `?` doesn't, and why doesn't it always work?

?? sometimes displays the source code of an object or function. It doesn't always work because some functions are built-in or implemented in compiled code.

**14.** (Multiple Choice) The signature is `sorted(iterable, /, *, key=None, reverse=False)`. Which call is valid?
A) `sorted(iterable=nums)`  B) `sorted(nums, None, True)`  C) `sorted(nums, reverse=True)`  D) `sorted()`

C

**15.** (Code Tracing) What error does this raise, and what does it mean?
```python
numbers = [1, 2, 3]
numbers.mean()
```

This raises an attribute error because python lists do not have a built-in mean() function.

**16.** (Short Answer) A long traceback fills the screen. Which line should you read first, and why?

You should read the last line of the traceback first. It identifies the error type and usually explains what went wrong.

**17.** (Short Answer) What does `dir(obj)` give you that Tab completion doesn't?

dir(obj) displays a complete list of available attributes and methods, while tab completion is useful to complete names that you don't fully remember.

---

## Section D — Markdown (04)

**18.** (Short Answer) What's the Markdown syntax for a level-2 heading (like `## Section 2`)?

Use two has symbols followed by a space: 
## Section 2

**19.** (Short Answer) How do you write **inline** LaTeX math in a Markdown cell, versus a **block** equation on its own line(s)?

Use the dollar sign, $, on both ends of latex expression to write inline latex math in a markdown cell.
Use two dollar signs on both ends of an expression to write a block equation.

**20.** (Short Answer) The Markdown text `The item costs $5 and the tax is $2.` renders strangely. Why, and how do you fix it?

Markdown interprets dollar signs as delimiters for latex math. Use escape sequences on the dollar signs to fix it.

**21.** (Short Answer) You typed two lines directly under each other in a Markdown cell, but they render as **one** line. Name two ways to fix it.

Add two spaces at the end of the first line to create a line break.
Insert a blank line between the two lines to create separate paragraphs.

**22.** (Short Answer) Why might you add narrative Markdown cells between code cells instead of just writing code comments?

Narrative markdown cells explain the purpose, results, and conclusions of the code. They are also easier to read than comments.

---

## Section E — Files and Paths (05)

**23.** (Code Tracing) What does this print?
```python
with open('x.txt', 'w', encoding='utf-8') as f:
    f.write('hi')

with open('x.txt', 'r', encoding='utf-8') as f:
    print(f.read())
```

hi

**24.** (Multiple Choice) Which file mode adds to the end of an existing file **without** erasing it?
A) `'r'`  B) `'w'`  C) `'a'`  D) `'x'`

C

**25.** (Code Tracing) What does this print?
```python
from pathlib import Path
p = Path('data') / 'sales_2026.csv'
print(p.name, p.stem, p.suffix)
```

sales_2026.csv sales_2026 .csv

**26.** (Short Answer) Why is it good practice to use a relative path (like `'data/file.csv'`) instead of an absolute path (like `'C:/Users/yourname/...'`) in a notebook you'll share or submit?

Relative paths make notebooks more portable because they don't depend on a specific user's computer, username, or folder structure.

**27.** (Code Tracing) `scores.csv` contains the two lines `Name,Score` and `Alice,90`. What does this print, and why might that cause a problem?
```python
import csv
with open('scores.csv', newline='', encoding='utf-8') as f:
    rows = list(csv.reader(f))
print(rows[1])
```

['Alice', '90']

This can cause problems because the values, such as '90', are strings and not numerical values. The score needs to be converted to a number before it can be used in calculations.

**28.** (True/False) After saving `{'point': (3, 4)}` with `json.dump` and reading it back with `json.load`, you get back exactly the same dictionary.

False

---

## Section F — Data Input and Output (06)

**29.** (Short Answer) What does `pd.read_csv('file.csv')` return?

It returns pandas dataframe containg the data from the csv file.

**30.** (Multiple Choice) Which DataFrame method shows summary statistics (mean, standard deviation, min/max, etc.)?
A) `.head()`  B) `.info()`  C) `.describe()`  D) `.columns()`

C

**31.** (Short Answer) You save a DataFrame with `df.to_csv('out.csv')`, read it back, and find an extra `Unnamed: 0` column. What caused it, and how do you prevent it?

The extra column is caused by pandas saving the dataframe index by default. Prevent it by adding index=false.

**32.** (Short Answer) What does JSON written with `orient='records'` look like, and why is it usually the layout you want?

It looks like a list of dictionaries. It is usually desired because it is easy to read and work with in Python and other applications.

**33.** (Short Answer) After `pd.read_csv`, the ZIP code `02108` shows up as `2108`. Why, and how do you fix it?

Pandas interprets the ZIP code as a number and removes the leading zero. Fix it by specifying the column as a string.

**34.** (Short Answer) What does `pd.read_excel('file.xlsx', sheet_name=None)` return?

It returns a dictionary of DataFrames, with each worksheet name as a key and its corresponding DataFrame as the value.

---

## Section G — Plotting with NumPy and Matplotlib (07)

**35.** (Code Tracing) What do these two lines print?
```python
print([1, 2] * 2)
print(np.array([1, 2]) * 2)
```

[1, 2, 1, 2]
[2 4]

**36.** (Matching) Choose the best chart (line, bar, scatter, or histogram) for each question:
a) Which department sold the most?
b) How did daily website visits change over a month?
c) Is there a relationship between price and units sold?
d) What is the distribution of customer order values?

a) Bar chart
b) Line chart
c) Scatter plot
d) Histogram

**37.** (Short Answer) A histogram and a bar chart both draw rectangles. What's the difference in what they show?

A histogram displays the distribution of numerical data grouped into intervals (bins). A bar chart compares separate categories.

**38.** (Short Answer) You call `plt.show()` and then `plt.savefig('chart.png')`, and the saved image is blank. Why?

If you call plt.show() first, it may display and close or clear the figure. To fix it, save the figure before plt.show().

**39.** (Short Answer) On a box plot, what does the line **inside** the box represent, and what do the dots **beyond** the whiskers represent?

The line inside the box represents the median. The dots beyond the whiskers represent potential outliers.

---

## Section H — Timing and Performance (08)

**40.** (Short Answer) What's the difference between `%time` and `%timeit`, and why is `%timeit` more trustworthy for comparisons?

%time measures how long one execution takes, while %timeit runs the code multiple times and calculates an average. %timeit is more trustworthy because repeated measurements reduce the effect of random variations and temporary slowdowns.

**41.** (Short Answer) Why is a NumPy vectorized operation like `arr ** 2` usually much faster than a Python `for` loop doing the same calculation element by element?

NumPy uses optimized, compiled code to perform operations on entire arrays rather than processing each element individually through Python. This reduces Python-level overhead and makes calculations faster.

**42.** (True/False) A variable created inside a `%%timeit` cell is available in the cells after it.

False

**43.** (Short Answer) What's unfair about comparing `%timeit np.array(my_list) ** 2` against `%timeit arr ** 2` to decide whether squaring is fast?

The first expression includes the time required to convert the list into a NumPy array. The second only measures the squaring operation. This makes the comparison unfair.

**44.** (Short Answer) Why is `[s / max(scores) for s in scores]` slow for large lists? How would you fix it, and roughly what happens to its runtime when the list doubles in size?

The expression repeatedly calculates max(scores) for every element which causes unnecessary repeated work. Calculate the maximum once and use NumPy or a list comprehension.

**45.** (Multiple Choice) What does `%prun` show you?
A) Only the total time of the cell  B) How much time was spent in each function called  C) How much memory each variable uses  D) The source code of a function

B