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

### Cleaning up whitespace with strip()

`.strip()` returns a new string with any whitespace at the **start and
end** removed — it leaves whitespace in the middle of the string alone.
It's handy for cleaning up text that came from user input or a file,
where stray spaces tend to sneak in:

```python
messy_string = "  I can't stand this unnecessary white space!   "

print(repr(messy_string))
print(repr(messy_string.strip()))
```

`repr()` here just makes the whitespace and the string's quote marks
visible in the output, so it's easier to see exactly where the extra
spaces were.

<script type="py-editor">
messy_string = "  I can't stand this unnecessary white space!   "

print(repr(messy_string))
print(repr(messy_string.strip()))
</script>

### Replacing text with replace()

`.replace(old, new)` returns a new string with every occurrence of `old`
swapped out for `new`:

```python
mood_string = "I am having a terrible time coding in Python!"

print(mood_string.replace("terrible", "wonderful"))
```

<script type="py-editor">
mood_string = "I am having a terrible time coding in Python!"

print(mood_string.replace("terrible", "wonderful"))
</script>

### Parsing a CSV-style line

CSV ("comma-separated values") is a common plain-text format for tabular
data — one row per line, fields separated by commas. `.split(",")` with no
`maxsplit` splits on *every* comma, which is exactly what we want here
since we know each line has exactly four fields:

```python
csv_line = "Nirvana,Smells Like Teen Spirit,5:01,1991"

artist, song_title, length, release_date = csv_line.split(",")

print(artist)
print(song_title)
print(length)
print(release_date)
```

<script type="py-editor">
csv_line = "Nirvana,Smells Like Teen Spirit,5:01,1991"

artist, song_title, length, release_date = csv_line.split(",")

print(artist)
print(song_title)
print(length)
print(release_date)
</script>

### Converting minutes:seconds into total seconds

`length` is still a string, `"5:01"` — useful for display, but not
something we can do math on directly. Splitting on `:` gives us the
minutes and seconds separately; converting each to an `int` and combining
them (`minutes * 60 + seconds`) gives the song's length in total seconds:

```python
minutes_str, seconds_str = length.split(":")
total_seconds = int(minutes_str) * 60 + int(seconds_str)

print(total_seconds)   # 301
```

<script type="py-editor">
csv_line = "Nirvana,Smells Like Teen Spirit,5:01,1991"
artist, song_title, length, release_date = csv_line.split(",")

minutes_str, seconds_str = length.split(":")
total_seconds = int(minutes_str) * 60 + int(seconds_str)

print(total_seconds)
</script>

### Splitting into a list (array)

So far `.split()` has always split a string into exactly the number of
pieces we knew to expect, unpacked straight into separate variables. But
`.split()` actually always returns a **list** — an ordered collection that
can hold as many values as it needs to, all in one variable. (Other
languages often call this same kind of structure an "array".) Each item in
a list has a position, or *index*, starting at `0` for the first item —
and you grab an item out of a list with `[ ]`, the same square-bracket
syntax used for indexing strings.

```python
fruit_string = "banana, strawberry, apple, orange, mango, blueberry, pineapple"
fruits = fruit_string.split(", ")

print(fruits)
```

<script type="py-editor">
fruit_string = "banana, strawberry, apple, orange, mango, blueberry, pineapple"
fruits = fruit_string.split(", ")

print(fruits)
</script>

Once it's a list, grab any single item by its index. Lists are
zero-indexed, so the third item is at index `2`:

```python
print(fruits[2])   # "apple"
```

<script type="py-editor">
fruit_string = "banana, strawberry, apple, orange, mango, blueberry, pineapple"
fruits = fruit_string.split(", ")

print(fruits[2])
</script>

### Indexing and slicing a string

Strings support that same `[ ]` indexing, one character at a time, and
also **slicing** — `text[start:end]` — to pull out a whole range of
characters at once. Slicing grabs everything from `start` up to, but not
including, `end`.

```python
text = "saxophone"

print(text[2])      # "x"
print(text[4:9])    # "phone"
```

A quick way to check a slice's boundaries: count the characters.
`saxophone` has the letter `x` at index `2` (`s` is `0`, `a` is `1`), and
`phone` is 5 letters long starting at index `4` — so it runs through
index `8`, which means the slice has to end at `9` (`text[4:9]`), since
the ending index in a slice is always one past the last character you
want.

<script type="py-editor">
text = "saxophone"

print(text[2])
print(text[4:9])
</script>
