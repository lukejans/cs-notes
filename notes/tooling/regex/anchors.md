# Regex: Anchors

Anchors match positions in the text instead of characters. This is useful for matching whole words because the word boundary anchor `\b` matches the position between a word character (`\w`) and a non-word character (`\W`). Something important to note about anchors is that they don't consume characters, they simply match bounds. This distinction is important and will be illustrated in the examples below.

| Anchor | Meaning                                  |
| ------ | ---------------------------------------- |
| `^`    | Start of a string or start of a line     |
| `$`    | End of a string or end of a line         |
| `\b`   | Word boundary                            |
| `\B`   | Non-word boundary (not standard in PCRE) |

## Hat Anchor

The hat anchor `^` will only match the beginning of a string. This is useful if you want to make sure a pattern is present at the beginning of a string. It can also do the same thing but for newlines. This will only activate when the [multiline `/pattern/m` flag](flags.md#multiline) is being used. For example imagine you want to match all the headings in the following markdown file:

```md
# Foo

Bar

## Baz
```

```regex
/^#{1,6}.*/gm
```

```text
# Foo
## Baz
```

## Dollar Sign Anchor

The dollar sign anchor `$` does the same thing as the hat anchor `^` but for the end of a string or line. It allows you to express patterns that must be at the end of content. See how the below regex matches this string: `"foobar bar"`.

```regex
/\w*bar$/g
```

```text
bar
```

## Word Boundary Anchor

The word boundary anchor `\b` matches the position between a word character (`\w`) and a non-word character (`\W`). Note that this is very different than just wrapping a match in the non-word character `\W`, because `\b` won't consume characters. See how the two regex patterns behave differently on this string: `"cat catalog"`.

```regex
/\bcat\b/g
/\Wcat\W/g
```

```text
// \b anchor regex
cat

// \W character class
<< NO MATCH >>
```

Both of the patterns successfully avoid matching "catalog", but notice how the `\W` non-word character class completely misses the first "cat" because there is no non-word character on to match on the front of the word.

## Non-word Boundary Anchor

The _non-word boundary anchor `\B`_ might be used less but still has its place. It is useful for if you want to check for the presence of something within a word or string of word characters. The example below illustrates this by matches words that end with "cat" without matching "cat" itself: `"hellcat bobcat cat"`.

```regex
/\Bcat/g
```

```text
hellcat
bobcat
```
