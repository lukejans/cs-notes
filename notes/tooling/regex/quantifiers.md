# Regex: Quantifiers

<!--TODO
link this note to globbing once that note is created.

why: globbing is a pattern matching technique used in shell scripting
     to match filenames based on patterns. The "?" and "*" come from
     the Unix shell and are used to match any single character and any
     sequence of characters, respectively.
-->

Quantifiers specify how many times the preceding element (character literal, [character class](./character-classes.md)... ) is allowed to repeat.

| Quantifier  | Meaning                 |
| ----------- | ----------------------- |
| `?`         | Zero or one             |
| `*`         | Zero or more            |
| `+`         | One or more             |
| `{n}`       | Exactly `n`             |
| `{min,}`    | `min` or more           |
| `{,max}`    | Zero up to `max`        |
| `{min,max}` | Between `min` and `max` |

Due to quantifiers being relatively simple there isn't much to talk about here but below are some example regex patterns just to familiarize yourself with the syntax.

```regex
/#?\d/g      # digit possibly preceded with "#"
/cat\w+/g    # words that start with "cat"
/\w{3}/g     # three letter words
/\w{3,}/g    # three or more letter words
/\d{0,9}/g   # numbers 0 to 9 digits long
```
