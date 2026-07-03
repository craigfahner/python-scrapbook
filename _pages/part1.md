---
layout: page
title: Part 1
permalink: /part1/
---

## Part 1: Data types, arithmetic operators, variables

### Hello, World!

The classic first program. In Python, printing text to the screen is done
with the built-in `print()` function.

```python
print("Hello, world!")
```

Try it yourself below — the code box is editable, so change the message and
hit **Run** to see the result:

<script type="py-editor">
print("Hello, world!")
</script>

### Python is case-sensitive

Python treats uppercase and lowercase letters as different characters, even
in names of built-in functions. `print` is not the same as `Print` — only
the lowercase spelling refers to the actual built-in function.

```python
print("Hello, world!")   # works: this is the real built-in function

Print("Hello, world!")   # NameError: 'Print' is not defined
```

Run the box below to see the error Python raises when the case doesn't
match:

<script type="py-editor">
Print("Hello, world!")
</script>

### Data types and arithmetic operators

Every value in Python has a data type. The basics you'll run into constantly:

| Type    | Example       | Description            |
|---------|---------------|-------------------------|
| `int`   | `5`           | whole numbers           |
| `float` | `5.0`         | decimal numbers         |
| `str`   | `"hello"`     | text                    |
| `bool`  | `True`        | `True` or `False`       |

You can check a value's type with the built-in `type()` function:

```python
print(type(5))       # <class 'int'>
print(type(5.0))     # <class 'float'>
print(type("hello")) # <class 'str'>
print(type(True))    # <class 'bool'>
```

<script type="py-editor">
print(type(5))
print(type(5.0))
print(type("hello"))
print(type(True))
</script>

Python's arithmetic operators:

| Operator | Meaning            | Example  | Result |
|----------|--------------------|----------|--------|
| `+`      | addition           | `7 + 2`  | `9`    |
| `-`      | subtraction        | `7 - 2`  | `5`    |
| `*`      | multiplication     | `7 * 2`  | `14`   |
| `/`      | true division      | `7 / 2`  | `3.5`  |
| `//`     | floor division     | `7 // 2` | `3`    |
| `%`      | modulo (remainder) | `7 % 2`  | `1`    |
| `**`     | exponent           | `7 ** 2` | `49`   |

Notice that `/` (true division) always returns a `float`, even if the numbers
divide evenly. `//` (floor division) instead divides and then **rounds down**
to the nearest whole number, returning an `int` when both operands are ints:

```python
print(7 / 2)    # 3.5  -- true division, keeps the remainder as a decimal
print(7 // 2)   # 3    -- floor division, drops the remainder entirely

print(-7 / 2)   # -3.5
print(-7 // 2)  # -4   -- rounds down (toward negative infinity), not toward zero!
```

<script type="py-editor">
print(7 / 2)
print(7 // 2)

print(-7 / 2)
print(-7 // 2)
</script>

### Comparison operators

Comparison operators compare two values and always evaluate to a `bool`:
`True` or `False`.

| Operator | Meaning               |
|----------|-----------------------|
| `==`     | equal to              |
| `!=`     | not equal to          |
| `<`      | less than             |
| `>`      | greater than          |
| `<=`     | less than or equal    |
| `>=`     | greater than or equal |

**With `int` and `float`** — Python compares by numeric value, so an `int`
and a `float` can be equal even though they're different types:

```python
print(5 > 3)      # True
print(5 == 5.0)   # True  -- same value, different types
print(5.5 <= 5)   # False
```

**With `str`** — strings are compared character by character using each
character's underlying code point, which sorts uppercase letters before
lowercase ones (and means comparisons are case-sensitive, just like the
`print` / `Print` example earlier):

```python
print("apple" == "apple")   # True
print("apple" == "Apple")   # False -- case-sensitive
print("apple" < "banana")   # True  -- 'a' comes before 'b'
print("Zebra" < "apple")    # True  -- 'Z' (90) comes before 'a' (97) in ASCII
```

<script type="py-editor">
print(5 > 3)
print(5 == 5.0)
print(5.5 <= 5)

print("apple" == "apple")
print("apple" == "Apple")
print("apple" < "banana")
print("Zebra" < "apple")
</script>

### Variables and naming rules

A variable is created by assigning it a value with `=`. The name on the
left is created (or updated) to point to the value on the right:

```python
age = 25
temperature = 98.6
name = "Ada"
```

Variable names must follow a few rules:

- Can contain letters, digits, and underscores (`_`)
- Cannot start with a digit
- Cannot contain hyphens, spaces, or most other punctuation
- Cannot be a reserved keyword (like `for`, `if`, or `class`)
- Are case-sensitive, just like everything else in Python

**Valid names** — underscores are allowed at the start of a name or
anywhere inside it, and digits are fine as long as they aren't first:

```python
_count = 0                 # leading underscore -- valid
my_variable_name = "hi"    # inline underscores -- valid, the standard style (snake_case)
variable2 = 5               # trailing digit -- valid
```

<script type="py-editor">
_count = 0
my_variable_name = "hi"
variable2 = 5

print(_count)
print(my_variable_name)
print(variable2)
</script>

**Invalid: starting with a digit.** Python tries to read `2cool` as a
number followed by a name and can't parse it:

```python
2cool = 5
# SyntaxError: invalid decimal literal
```

<script type="py-editor">
2cool = 5
</script>

**Invalid: hyphens.** Python reads `-` as the subtraction operator, not
part of a name, so this looks like `my - variable = 5` — an expression,
not something you can assign to:

```python
my-variable = 5
# SyntaxError: cannot assign to expression here. Maybe you meant '==' instead of '='?
```

<script type="py-editor">
my-variable = 5
</script>

### Naming conventions: variables vs. constants

Python doesn't enforce a "constant" type — any name can be reassigned at
any time. Instead, Python relies on **naming convention** to signal intent:

- **Variables** use `snake_case` — all lowercase, words separated by
  underscores. This is what we've used so far (`my_variable_name`,
  `variable2`).
- **Constants** — values that shouldn't change after they're set — use
  `SCREAMING_SNAKE_CASE`: all uppercase, words separated by underscores.
  This is a signal to other programmers ("don't reassign this"), not a
  rule Python enforces.

```python
# variable -- expected to change while the program runs
score = 0
score = score + 10

# constant -- a fixed value, by convention never reassigned
MAX_SCORE = 100
```

<script type="py-editor">
score = 0
score = score + 10
print(score)

MAX_SCORE = 100
print(MAX_SCORE)
</script>

### Compound assignment operators

`score = score + 10` — reassigning a variable based on its own current
value — is common enough that Python has a shorthand for it: compound
assignment operators. `score += 10` does exactly the same thing as
`score = score + 10`, just shorter.

There's a compound version of every arithmetic operator:

| Operator | Equivalent to    |
|----------|------------------|
| `+=`     | `score = score + x` |
| `-=`     | `score = score - x` |
| `*=`     | `score = score * x` |
| `/=`     | `score = score / x` |
| `//=`    | `score = score // x` |
| `%=`     | `score = score % x` |
| `**=`    | `score = score ** x` |

```python
score = 0
score += 10   # same as: score = score + 10
score += 5    # same as: score = score + 5
print(score)  # 15

score *= 2    # same as: score = score * 2
print(score)  # 30

score //= 4   # same as: score = score // 4
print(score)  # 7
```

<script type="py-editor">
score = 0
score += 10
score += 5
print(score)

score *= 2
print(score)

score //= 4
print(score)
</script>

### Type conversion functions

Python provides built-in functions to convert a value from one type to
another. The most common ones share their name with the type they produce:

| Function  | Converts to |
|-----------|-------------|
| `str()`   | `str`       |
| `int()`   | `int`       |
| `float()` | `float`     |
| `bool()`  | `bool`      |

Here's a `float` converted to a `str` and then back to a `float`:

```python
pi = 3.14
print(type(pi))        # <class 'float'>

pi_as_text = str(pi)   # float -> str
print(pi_as_text)
print(type(pi_as_text))  # <class 'str'>

pi_again = float(pi_as_text)   # str -> float
print(pi_again)
print(type(pi_again))    # <class 'float'>
```

<script type="py-editor">
pi = 3.14
print(type(pi))

pi_as_text = str(pi)
print(pi_as_text)
print(type(pi_as_text))

pi_again = float(pi_as_text)
print(pi_again)
print(type(pi_again))
</script>
