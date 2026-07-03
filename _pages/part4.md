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
list, until the list runs out:

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

### Filtering tracks into a new list

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
