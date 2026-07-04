---
layout: page
title: Part 6
permalink: /part6/
---

## Part 6: Functions

### Defining a function: alternating case

A function is a named, reusable block of code. `def` starts the
definition, followed by a name and any **parameters** — inputs the
function needs — in parentheses. `return` sends a value back out to
whoever called the function.

Just like `for` loops and `if` statements, `def alternate_case(text):`
ends in a colon, and every line that's part of the function body has to
be indented underneath it — that includes the `return` at the end. This
example nests three levels deep: the `for` loop is indented once inside
the function, and the `if`/`else` is indented once more inside the loop.
Each level of indentation says "this code runs inside whatever line is
one indent level up" — so `result += letter.upper()` only runs as part of
the loop, which only runs as part of the function:

```python
def alternate_case(text):
    result = ""
    for index, letter in enumerate(text):
        if index % 2 == 0:
            result += letter.upper()
        else:
            result += letter.lower()
    return result

print(alternate_case("hello there"))
```

`enumerate(text)` loops over `text` like a normal `for` loop, but hands
back two values each time instead of one: the current `index` (0, 1, 2,
...) along with the `letter` at that position. Checking `index % 2 == 0`
(from [Part 1's arithmetic operators](../part1/)) tells us whether we're
on an even or odd position, so we know whether to `.upper()` or
`.lower()` that letter before adding it onto `result`.

<script type="py-editor">
def alternate_case(text):
    result = ""
    for index, letter in enumerate(text):
        if index % 2 == 0:
            result += letter.upper()
        else:
            result += letter.lower()
    return result

print(alternate_case("hello there"))
</script>

### Returning True or False: a strong password checker

A function can also return a `bool`, which makes it useful directly
inside an `if` condition elsewhere. This one checks a password for four
things: at least one uppercase letter, one lowercase letter, one digit,
and one symbol.

```python
def is_strong_password(password):
    has_upper = False
    has_lower = False
    has_digit = False
    has_symbol = False

    for char in password:
        if char.isupper():
            has_upper = True
        elif char.islower():
            has_lower = True
        elif char.isdigit():
            has_digit = True
        else:
            has_symbol = True

    return has_upper and has_lower and has_digit and has_symbol

print(is_strong_password("Password123!"))   # True
print(is_strong_password("password123"))    # False -- no uppercase or symbol
```

`.isupper()`, `.islower()`, and `.isdigit()` each check a single
character and return `True` or `False`. Any character that isn't a
letter or digit (like `!`) falls into the `else`, so `has_symbol` gets
set instead. `and` combines all four checks into one result — the whole
expression is only `True` if *every* one of them is `True`.

<script type="py-editor">
def is_strong_password(password):
    has_upper = False
    has_lower = False
    has_digit = False
    has_symbol = False

    for char in password:
        if char.isupper():
            has_upper = True
        elif char.islower():
            has_lower = True
        elif char.isdigit():
            has_digit = True
        else:
            has_symbol = True

    return has_upper and has_lower and has_digit and has_symbol

print(is_strong_password("Password123!"))
print(is_strong_password("password123"))
</script>
