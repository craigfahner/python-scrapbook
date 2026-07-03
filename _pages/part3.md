---
layout: page
title: Part 3
permalink: /part3/
---

## Part 3: Collections

### Lists

A list is an ordered collection of values, written with square brackets
and commas: `[value1, value2, ...]`. We already ran into lists back in
[Part 2](../part2/) as the result of `.split()` — a list is that same
type, just built directly instead of coming from splitting a string.

A list can hold strings, numbers, or even other lists:

```python
birds = ["Robin", "Sparrow", "Blue Jay", "Cardinal", "Crow",
         "Finch", "Owl", "Hawk", "Hummingbird", "Woodpecker"]

leap_years = [2000, 2004, 2008, 2012, 2016, 2020, 2024]

bands = [
    ["John Lennon", "Paul McCartney", "George Harrison", "Ringo Starr"],
    ["Mick Jagger", "Keith Richards", "Charlie Watts", "Ronnie Wood", "Bill Wyman"],
    ["John Phillips", "Michelle Phillips", "Cass Elliot", "Denny Doherty"],
]

print(birds)
print(leap_years)
print(bands)
```

`birds` is a list of `str`, `leap_years` is a list of `int`, and `bands`
is a **list of lists** — each item in `bands` is itself a whole list (The
Beatles, then The Rolling Stones, then The Mamas & the Papas).

<script type="py-editor">
birds = ["Robin", "Sparrow", "Blue Jay", "Cardinal", "Crow",
         "Finch", "Owl", "Hawk", "Hummingbird", "Woodpecker"]

leap_years = [2000, 2004, 2008, 2012, 2016, 2020, 2024]

bands = [
    ["John Lennon", "Paul McCartney", "George Harrison", "Ringo Starr"],
    ["Mick Jagger", "Keith Richards", "Charlie Watts", "Ronnie Wood", "Bill Wyman"],
    ["John Phillips", "Michelle Phillips", "Cass Elliot", "Denny Doherty"],
]

print(birds)
print(leap_years)
print(bands)
</script>
