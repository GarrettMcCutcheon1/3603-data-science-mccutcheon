# 📝 Worksheet: 04 - More Functions & Loops

Do this worksheet **on paper, without a computer**. Each section ends with an **🤖 Explain It** prompt: write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Defaults and Keywords

```python
def price(amount, tax=0.0825, discount=0):
    return round(amount * (1 + tax) - discount, 2)
```

What does each call return?

1. `price(100)` → ____________________________
2. `price(100, discount=10)` → ____________________________
3. `price(100, 0)` → ____________________________
4. `price(discount=5, amount=20)` → ____________________________

> 🤖 **Explain It:** Why are keyword arguments easier to read than positional ones in a call like `price(100, 0, 10)`?
Keyword arguments are easier to read because they make it clear what each value represents without having to remember the order of the parameters. 
In the example 'price(100, 0, 10), one can achieve the same result with 'price(discount=10, amount=100, tax=0).

---

## 🧠 Section 2: Scope

What prints? Explain why.

```python
count = 0

def add_one(count):
    count = count + 1
    return count

result = add_one(count)
print(count, result)
```

`Answer:` ____________________________

> 🤖 **Explain It:** Describe the "room with two doors" model of a function in your own words.
A function is like a room with its own variables seperate from global variables. Parameters let information enter through one 'door', while return 
statements let information leave through another 'door'.

---

## 🧠 Section 3: Trace a While Loop

```python
balance = 100
years = 0
while balance < 150:
    balance = balance + 20
    years += 1
```

| pass | `balance` at the start | `balance < 150`? | `balance` after | `years` after |
|------|------------------------|------------------|-----------------|---------------|
| 1 | 100 | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

Final `years`: ____________  Final `balance`: ____________

What single change would make this an **infinite** loop?  
`Answer:` ____________________________

---

## 🧠 Section 4: `for` or `while`?

| Task | `for` or `while`? | Why? |
|------|-------------------|------|
| Print each line of a file | | |
| Keep asking for a password until it's correct | | |
| Find the average of a list of prices | | |
| Double a number until it's over one million | | |

---

## 🧠 Section 5: Files

Given the file `pets.txt`:

```text
name,species
Rex,dog

# rescued in May
Tom,cat
```

1. How many times does `for line in f:` run? ____________
2. Which lines should your code skip, and how would you detect each one?  
   `Answer:` ____________________________
3. Write the list of dictionaries a `read_pets` function should return:  
   `Answer:` ____________________________

> 🤖 **Explain It:** When is `try` / `except` a good idea, and when does it just hide bugs?
'try' / 'except' is useful when an error is possible, but it is not detrimental to the rest of the program. It just hides bugs when
unexpected errors are concealed without the underlying problem being known.