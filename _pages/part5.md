---
layout: page
title: Part 5
permalink: /part5/
---

## Part 5: Conditionals

### Comparison operators

Conditionals depend on comparison operators (first introduced back in
[Part 1](../part1/)) to produce the `True`/`False` values that decide
which branch runs. Here's every one of them, comparing `x = 3` and
`y = 6`:

```python
x = 3
y = 6

print(x == y)   # equal to
print(x != y)   # not equal to
print(x < y)    # less than
print(x > y)    # greater than
print(x <= y)   # less than or equal to
print(x >= y)   # greater than or equal to
```

<script type="py-editor">
x = 3
y = 6

print(x == y)
print(x != y)
print(x < y)
print(x > y)
print(x <= y)
print(x >= y)
</script>

### if / else

An `if` statement runs a block of code only when a condition is `True`;
`else` gives a fallback block that runs when it's `False`. Here, whether
you need a jacket depends on the temperature.

Just like the `for` loop in [Part 4](../part4/), indentation is what
marks which lines belong to which branch. `if temperature < 60:` and
`else:` both end in a colon, and each is followed by an indented block —
Python runs the indented lines under whichever branch's condition
matched, and skips the other block entirely. Line up the indentation
wrong and Python either won't know which branch a line belongs to, or
will raise an `IndentationError`:

```python
temperature = 45

if temperature < 60:
    print("put on a jacket")
else:
    print("no jacket needed!")
```

<script type="py-editor">
temperature = 45

if temperature < 60:
    print("put on a jacket")
else:
    print("no jacket needed!")
</script>

Try changing `temperature` to something 60 or above and running it again
— the `else` branch takes over instead.

### elif: more than two outcomes

Plain `if` / `else` only covers two outcomes. `elif` ("else if") lets you
chain together as many conditions as you need — Python checks them in
order, top to bottom, and runs the first one that's `True`, skipping the
rest:

```python
temperature = 28

if temperature >= 80:
    print("wear shorts")
elif temperature >= 65:
    print("wear pants")
elif temperature >= 50:
    print("wear a sweater")
elif temperature >= 35:
    print("wear a jacket")
elif temperature >= 20:
    print("wear a wool jacket")
else:
    print("wear a wool jacket and gloves")
```

Each `elif` only gets checked if every condition above it was `False`, so
`temperature >= 50` only runs when we already know `temperature < 65`
(otherwise an earlier branch would have already matched and stopped the
chain). The final `else` catches anything left over — here, anything
colder than 20. Try changing `temperature` to see which branch fires:

<script type="py-editor">
temperature = 28

if temperature >= 80:
    print("wear shorts")
elif temperature >= 65:
    print("wear pants")
elif temperature >= 50:
    print("wear a sweater")
elif temperature >= 35:
    print("wear a jacket")
elif temperature >= 20:
    print("wear a wool jacket")
else:
    print("wear a wool jacket and gloves")
</script>

### Filtering a list using conditionals

This one nests a loop inside a loop, plus a condition. For each album, we
loop over that album's `tracks`; an `if` checks whether `"love"` shows up
in the (lowercased) track name, and if so, `.append()`s it onto a new
`love_songs` list. Once both loops finish, a final loop prints the
results:

```python
love_songs = []

for album in beatles_albums:
    for track in album["tracks"]:
        if "love" in track.lower():
            love_songs.append(track)

for song in love_songs:
    print(song)
```

`.lower()` (from [Part 2](../part2/)) makes the check
case-insensitive, so it catches "Love", "LOVE", or "love" wherever it
appears in a title — not just an exact match.

**Matching on a word boundary.** As written, `"love" in track.lower()`
only matches the exact letters `l-o-v-e` in a row, so it misses "All My
**Loving**" (`love` isn't a substring of `loving`, since the fourth
letter differs). Checking for `" lov"` — a space followed by `lov` —
instead matches the *start* of any word beginning with "lov", catching
both "Love" and "Loving." A track that's the very first word in its
title (like "Love Me Do") has no space in front of it, though, so we
glue on a leading space (`" " + track`) before checking, to treat the
start of the string the same as any other word boundary:

```python
love_songs = []

for album in beatles_albums:
    for track in album["tracks"]:
        if " lov" in (" " + track).lower():
            love_songs.append(track)

for song in love_songs:
    print(song)
```

<script type="py-editor">
beatles_albums = [
    {
        "album_title": "Please Please Me",
        "tracks": ["I Saw Her Standing There", "Misery", "Anna (Go to Him)",
                   "Chains", "Boys", "Ask Me Why", "Please Please Me",
                   "Love Me Do", "P.S. I Love You", "Baby It's You",
                   "Do You Want to Know a Secret", "A Taste of Honey",
                   "There's a Place", "Twist and Shout"],
    },
    {
        "album_title": "With the Beatles",
        "tracks": ["It Won't Be Long", "All I've Got to Do", "All My Loving",
                   "Don't Bother Me", "Little Child", "Till There Was You",
                   "Please Mister Postman", "Roll Over Beethoven", "Hold Me Tight",
                   "You Really Got a Hold on Me", "I Wanna Be Your Man",
                   "Devil in Her Heart", "Not a Second Time",
                   "Money (That's What I Want)"],
    },
    {
        "album_title": "A Hard Day's Night",
        "tracks": ["A Hard Day's Night", "I Should Have Known Better", "If I Fell",
                   "I'm Happy Just to Dance with You", "And I Love Her", "Tell Me Why",
                   "Can't Buy Me Love", "Any Time at All", "I'll Cry Instead",
                   "Things We Said Today", "When I Get Home", "You Can't Do That",
                   "I'll Be Back"],
    },
]

love_songs = []

for album in beatles_albums:
    for track in album["tracks"]:
        if " lov" in (" " + track).lower():
            love_songs.append(track)

for song in love_songs:
    print(song)
</script>
