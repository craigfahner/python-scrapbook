---
layout: page
title: Part 2
permalink: /part2/
---

## Part 2: All about strings

### Multi-line strings

Wrapping text in three quote marks (`"""` or `'''`) instead of one lets a
string span multiple lines. Line breaks typed inside the triple quotes
become part of the string itself:

```python
poem = """Robot walks into a bar
Orders a drink, lays down a bill
Bartender says, 'Hey, we don't serve robots'
And the robot says, 'Oh, but someday you will'"""

print(poem)
```

**Dealing with quotation marks inside a string.** This poem contains
dialogue in single quotes, and one of those lines even has an apostrophe
(`don't`). Python needs to know which quote marks belong to your text and
which ones close the string, so nested quotes take a little care:

- **Pick the quote character that doesn't appear in your text.** The
  whole poem is wrapped in triple *double* quotes (`"""`), so every single
  quote (`'`) inside it — including the apostrophe in `don't` — is just a
  regular character. There's no conflict because the opening and closing
  delimiter is a different character than what's nested inside.
- **If you can't avoid repeating the same quote character**, escape it
  with a backslash (`\"` or `\'`) so Python treats it as literal text
  instead of the end of the string. For example, `'Hey, we don\'t serve
  robots'` would work fine as a single-quoted string, because the `\'`
  tells Python "this apostrophe is part of the text, not the closing
  quote."

<script type="py-editor">
poem = """Robot walks into a bar
Orders a drink, lays down a bill
Bartender says, 'Hey, we don't serve robots'
And the robot says, 'Oh, but someday you will'"""

print(poem)
</script>

### String concatenation

The `+` operator joins strings together end to end — this is called
concatenation. It's a handy way to build a sentence out of variables:

```python
dog_name = "Rex"
dog_breed = "Labrador"
dog_age = 3

# dog_age is an int, and + can't mix str and int, so convert it with str() first
sentence = "My dog is named " + dog_name + " and he is a " + dog_breed + ". He is " + str(dog_age) + " years old."
print(sentence)
```

<script type="py-editor">
dog_name = "Rex"
dog_breed = "Labrador"
dog_age = 3

sentence = "My dog is named " + dog_name + " and he is a " + dog_breed + ". He is " + str(dog_age) + " years old."
print(sentence)
</script>

### f-strings

Building a sentence with `+` works, but it gets hard to read fast, and you
have to remember to wrap non-`str` values in `str()`. An f-string is an
easier way to drop variables directly into a string: put an `f` right
before the opening quote, then wrap each variable in `{ }` wherever it
should go. Python converts each value to a string automatically, so
`dog_age` doesn't need `str()` this time. The `{ }` can also hold a full
expression, not just a bare variable name — `{dog_age + 1}` does the math
and drops in the result:

```python
dog_name = "Rex"
dog_breed = "Labrador"
dog_age = 3

sentence = f"My dog is named {dog_name} and he is a {dog_breed}. He is {dog_age} years old. Next year, {dog_name} will be {dog_age + 1}."
print(sentence)
```

<script type="py-editor">
dog_name = "Rex"
dog_breed = "Labrador"
dog_age = 3

sentence = f"My dog is named {dog_name} and he is a {dog_breed}. He is {dog_age} years old. Next year, {dog_name} will be {dog_age + 1}."
print(sentence)
</script>

### String case conversion

Strings have built-in methods (called with a dot, like `dog_name.upper()`)
that return a new string converted to a different case. The original
string is left unchanged — these methods hand back a brand new string
rather than modifying `dog_name` in place.

| Method          | Effect                          | `"rex".method()` |
|-----------------|----------------------------------|-------------------|
| `.upper()`      | all uppercase                    | `"REX"`           |
| `.lower()`      | all lowercase                     | `"rex"`           |
| `.title()`      | capitalizes each word             | `"Rex"`           |
| `.capitalize()` | capitalizes only the first letter | `"Rex"`           |

```python
dog_name = "rex"

print(dog_name.upper())        # REX
print(dog_name.lower())        # rex
print(dog_name.title())        # Rex
print(dog_name.capitalize())   # Rex
```

<script type="py-editor">
dog_name = "rex"

print(dog_name.upper())
print(dog_name.lower())
print(dog_name.title())
print(dog_name.capitalize())
</script>

### Searching and extracting data from a string

Let's walk through a more involved example, starting with this string:

```python
dog_name = "Rex"
test_string = f"My dog {dog_name} has 6 fleas."
```

**Step 1: search for a word.** The `in` operator checks whether one string
appears anywhere inside another, and returns `True` or `False`:

```python
print("fleas" in test_string)   # True
```

<script type="py-editor">
dog_name = "Rex"
test_string = f"My dog {dog_name} has 6 fleas."

print("fleas" in test_string)
</script>

**Step 2: count how many times it shows up.** `.count()` returns the
number of (non-overlapping) times a substring appears:

```python
print(test_string.count("fleas"))   # 1
```

<script type="py-editor">
dog_name = "Rex"
test_string = f"My dog {dog_name} has 6 fleas."

print(test_string.count("fleas"))
</script>

**Step 3: find the number and store it in a new variable.** `.find()`
returns the *index* where a substring starts (or `-1` if it isn't
found) — that's different from `in`, which only tells you `True`/`False`.
We can use that index to slice out everything before `"fleas"`, split
that chunk into words, and grab the last one — the number itself. It
comes back as a `str`, so `int()` converts it to a usable number:

```python
fleas_index = test_string.find("fleas")     # index where "fleas" starts
before_fleas = test_string[:fleas_index]    # everything before "fleas"
number_text = before_fleas.split()[-1]      # the last word before "fleas", e.g. "6"

flea_count = int(number_text)
print(flea_count)   # 6
```

<script type="py-editor">
dog_name = "Rex"
test_string = f"My dog {dog_name} has 6 fleas."

fleas_index = test_string.find("fleas")
before_fleas = test_string[:fleas_index]
number_text = before_fleas.split()[-1]

flea_count = int(number_text)
print(flea_count)
</script>

### Splitting a string into parts

`.split()` breaks a string into a list wherever a separator appears. Given
a file name like this one, we can pull the band name, song title, and file
type into their own variables:

```python
file_name = "Nirvana - Smells Like Teen Spirit.mp3"

band_name, rest = file_name.split(" - ", 1)   # split once on " - "
song_title, file_type = rest.rsplit(".", 1)   # split once on the last "."

print(band_name)
print(song_title)
print(file_type)
```

The `1` in `.split(" - ", 1)` limits it to a single split, so only the
first `" - "` is used — this works no matter what band name comes before
it. `.rsplit(".", 1)` does the same thing from the *right* side, splitting
on the last `.` in the string — that keeps the file type correct even if
the song title itself contains a period.

<script type="py-editor">
file_name = "Nirvana - Smells Like Teen Spirit.mp3"

band_name, rest = file_name.split(" - ", 1)
song_title, file_type = rest.rsplit(".", 1)

print(band_name)
print(song_title)
print(file_type)
</script>

### A trickier file name

What about a messier case — a song title that itself contains hyphens,
*and* a second `" - "`?

```python
file_name = "Beastie Boys - B-Boy Bouillabaisse - 5-Piece Chicken Dinner.mp3"
```

Does the same parsing logic still hold up? Running it unchanged:

<script type="py-editor">
file_name = "Beastie Boys - B-Boy Bouillabaisse - 5-Piece Chicken Dinner.mp3"

band_name, rest = file_name.split(" - ", 1)
song_title, file_type = rest.rsplit(".", 1)

print(band_name)
print(song_title)
print(file_type)
</script>

It works, without changing a single line — for two reasons that were
already built into the original logic:

- **The separator is `" - "` (space, hyphen, space), not just `-`.** Bare
  hyphens with no surrounding spaces, like the ones in `B-Boy` and
  `5-Piece`, never match that pattern, so they're never mistaken for a
  band/song separator.
- **`maxsplit=1` means only the *first* match counts.** Even though
  `" - "` (with spaces) shows up twice in this file name, `.split(" - ", 1)`
  stops after the first one. Everything after it — including the second
  `" - "` — stays bundled into `rest`, and eventually becomes part of
  `song_title` once `.rsplit(".", 1)` peels off just the extension.

The logic isn't accidentally correct here — it was written to split only
once, from a known fixed point (the front for the band name, the back for
the file type), which is exactly what keeps it safe from extra hyphens or
extra `" - "`s anywhere in the middle.
