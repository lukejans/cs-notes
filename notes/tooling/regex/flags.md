# Regex: Flags

Flags modify regex behavior and are to be used at the closing slash of the regex.

| Flag | Meaning                       |
| ---- | ----------------------------- |
| `g`  | Global matching (all matches) |
| `i`  | Case-insensitive matching     |
| `m`  | Multiline mode (`^` and `$`)  |
| `s`  | Dot now matches newline (`.`) |

## Global

This is the most common regex flag and is likely what you will use with most of your regex patterns. The below regex finding all matches of the literal `"foo"` in the string `"foo foobar"`.

```regex
/foo/g
```

```text
foo
foobar
```

## Case-insensitive

This flag is used to match a pattern regardless of the case of the characters. So the below regex matches a literal `"foo"` of any case combination in the string `"Foo Foobar"`.

```regex
/foo/i
```

```text
Foo
```

## Multiline

This flag changes the behavior of the [start (`^`) and end (`$`) anchors](anchors.md) to match the start and end of each line in a string instead of the start and end of the string itself. So this regex matches words at the beginning of a line in the string literal `"foo\nfoobar foobaz"`. In this example, the `m` flag is paired with the global flag.

```regex
/^foo/mg
```

```text
foo
foobar
```

## Dotall

This flag is used to match the dot (`.`) character with newline characters. Finding matches of foo in the string `"foo\n"`.

```regex
/foo/s
```

```text
foo
\n
```
