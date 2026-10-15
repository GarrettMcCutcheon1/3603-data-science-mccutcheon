# 📝 Quiz: 02 - Strings and Text

20 questions covering string basics, string methods, formatted strings (f-strings), and the "going further" topics from the Challenge sections. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first — the Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — String Basics

**1.** (Multiple Choice) Which of these lets you write a string that spans multiple lines without using `\n`?
A) `'...'`  B) `"..."`  C) `'''...'''`  D) `f'...'`

My Answer: C

**2.** (Code Tracing) What prints?
```python
word = 'Python'
print(word[-1])
```

My Answer: 'n' 

**3.** (Code Tracing) What prints?
```python
word = 'Python'
print(word[::-1])
```

My Answer: 'nohtyP'

**4.** (True/False) Writing `'It's a test'` (an unescaped apostrophe inside single quotes) causes an error.

My Answer: True

**5.** (Short Answer) Why can't you run `word[0] = 'J'` if `word` is a string?

My Answer: Strings are immutable, and there individual characters cannot be changed after the string has been initialized.

**6.** (Code Tracing) What does this print (describe the spacing)?
```python
print('Hi\tThere')
```

My Answer: 'Hi  There' prints. \t creates a tab between 'Hi' and 'There'

---

## Section B — String Methods

**7.** (Code Tracing) What prints?
```python
print('  Ada  '.strip())
```

My Answer: 'Ada'

**8.** (Code Tracing) What prints?
```python
print('the quick brown fox'.split())
```

My Answer: ['the', 'quick', 'brown', 'fox']

**9.** (Short Answer) What's the difference between using `.find()` and using the `in` keyword to check whether a substring is present?

My Answer: .find() returns the index where the substring's first character apperars, while in returns True or False depending on if the substring is present.

**10.** (Multiple Choice) Which method checks whether a string contains only digit characters?
A) `.isdigit()`  B) `.isalpha()`  C) `.find()`  D) `.strip()`

My Answer: A

**11.** (Code Tracing) What prints?
```python
print('hello.py'.endswith('.py'))
```

My Answer: 'True'

**12.** (Short Answer) What does `'a,b,c'.split(',')` return?

My Answer: ['a', 'b', 'c']

---

## Section C — Formatted Strings

**13.** (Code Tracing) What prints?
```python
price = 9.5
print(f'{price:.2f}')
```

My Answer: '9.50'

**14.** (Code Tracing) What prints?
```python
print(f'{1234567:,}')
```

My Answer: '1,234,567'

**15.** (Short Answer) What does the `f` at the front of an f-string actually do?

My Answer: The 'f' tells python to evaluate expressions inside curly braces and insert their values into the string.

**16.** (Multiple Choice) Which format spec right-aligns a value in a 10-character field?
A) `:<10`  B) `:>10`  C) `:^10`  D) `:10>`

My Answer: B

**17.** (Code Tracing) What prints?
```python
x = 5
print(f'{x * 2}')
```

My Answer: '10'

**18.** (Short Answer) Name the two older string-formatting styles that predate f-strings (still seen in older code).

My Answer: .format() and % formatting

---

## Section D — Going Further (Bonus)

**19.** (Short Answer) What does prefixing a string with `r` (a raw string) do, and why is it especially useful for Windows file paths?

**20.** (Code Tracing) What prints?
```python
x = 7
print(f'{x=}')
```
