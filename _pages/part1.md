---
layout: page
title: Part 1
permalink: /part1/
---

## Part 1: Basics

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

