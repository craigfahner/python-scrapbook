---
layout: page
title: Part 4
permalink: /part4/
---

## Part 4: Loops

### The for loop

A `for` loop runs a block of code once for each item in a collection —
like the `daily_routine` list from [Part 3](../part3/). Each time through
the loop, the loop variable (here, `i`) is set to the next item in the
list, until the list runs out.

**Indentation is how Python knows what belongs to the loop.** The line
`for i in daily_routine:` ends with a colon, and every line meant to run
*inside* the loop must be indented (by convention, 4 spaces) below it —
`print(i)` runs once per item because it's indented under the `for` line.
As soon as a line goes back to the original indentation level, Python
treats it as outside the loop. Many other languages mark a block of code
with curly braces `{ }`; Python uses indentation instead — there's no
brace to leave out or forget to close, but getting the indentation wrong
(or mixing tabs and spaces) will cause an error, or silently change which
lines run inside the loop:

```python
daily_routine = ["wake up", "eat breakfast", "go to work", "eat lunch",
                  "go home", "exercise", "eat dinner", "watch tv"]

for i in daily_routine:
    print(i)
```

<script type="py-editor">
daily_routine = ["wake up", "eat breakfast", "go to work", "eat lunch",
                  "go home", "exercise", "eat dinner", "watch tv"]

for i in daily_routine:
    print(i)
</script>

`i` is an extremely common name for a loop variable — short for "index",
even though here it's holding each *item* itself, not a numeric position.
It's just a convention (any name would work, like `task` or `item`), but
you'll see `i` used this way constantly in other people's Python code.

### Looping over a list of dictionaries

The `beatles_albums` list from [Part 3](../part3/) is a list of
dictionaries — one dict per album. Looping over it works exactly the same
as looping over any other list; the loop variable is just a whole
dictionary each time through, so `[ ]` still reaches into it by key:

```python
for album in beatles_albums:
    print(album["album_title"], album["running_time_in_seconds"])
```

<script type="py-editor">
beatles_albums = [
    {
        "album_title": "Please Please Me",
        "release_date": "22 March 1963",
        "running_time": "31:59",
        "running_time_in_seconds": 1919,
        "tracks": ["I Saw Her Standing There", "Misery", "Anna (Go to Him)",
                   "Chains", "Boys", "Ask Me Why", "Please Please Me",
                   "Love Me Do", "P.S. I Love You", "Baby It's You",
                   "Do You Want to Know a Secret", "A Taste of Honey",
                   "There's a Place", "Twist and Shout"],
    },
    {
        "album_title": "With the Beatles",
        "release_date": "22 November 1963",
        "running_time": "33:07",
        "running_time_in_seconds": 1987,
        "tracks": ["It Won't Be Long", "All I've Got to Do", "All My Loving",
                   "Don't Bother Me", "Little Child", "Till There Was You",
                   "Please Mister Postman", "Roll Over Beethoven", "Hold Me Tight",
                   "You Really Got a Hold on Me", "I Wanna Be Your Man",
                   "Devil in Her Heart", "Not a Second Time",
                   "Money (That's What I Want)"],
    },
    {
        "album_title": "A Hard Day's Night",
        "release_date": "10 July 1964",
        "running_time": "30:09",
        "running_time_in_seconds": 1809,
        "tracks": ["A Hard Day's Night", "I Should Have Known Better", "If I Fell",
                   "I'm Happy Just to Dance with You", "And I Love Her", "Tell Me Why",
                   "Can't Buy Me Love", "Any Time at All", "I'll Cry Instead",
                   "Things We Said Today", "When I Get Home", "You Can't Do That",
                   "I'll Be Back"],
    },
]

for album in beatles_albums:
    print(album["album_title"], album["running_time_in_seconds"])
</script>
