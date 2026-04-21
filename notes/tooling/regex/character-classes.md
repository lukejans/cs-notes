# Regex: Character Classes

The character class is similar to literal matches, but it allows you to match a set of characters in a more efficient way. You can either use predefined classes or create your own custom classes from a set of characters. In

## Predefined Classes

| Character Class | Description                                 | POSIX Equivalent |
| --------------- | ------------------------------------------- | ---------------- |
| `\d`            | Digit (0-9).                                | `[:digit:]`      |
| `\D`            | Non-digit.                                  |                  |
| `\w`            | Word character (alphanumeric + underscore). | `[:alnum:]`      |
| `\W`            | Non-word character.                         |                  |
| `\s`            | Whitespace (spaces, tabs, etc.).            | `[:space:]`      |
| `\S`            | Non-whitespace.                             |                  |

> POSIX character classes can be more portable across different regex implementations, especially in POSIX-compliant systems. There are also more POSIX character classes available such as `[:alpha:]`, `[:lower:]`, `[:upper:]`, and `[:punct:]`. Note that these can only appear in a [custom class](character-classes.md#custom-classes) so must be used like so: `/[[:digit:]]/`.

### Digit Character Classes

The _digit character classes_ will simply match digit or non-digit characters. For example see how the below regex patterns behave when matching the string: `"0x E4"`.

**match digits:**

```regex
/\d/g
```

```text
0
4
```

**match non-digit characters:**

```regex
/\D/g
```

```text
x

E
```

### Word Character Classes

The _word character classes_ will simply match word or non-word characters. For example see how the below regex patterns behave when matching the string: `"h_9 -"`. Something to note here is that an underscore `_` is considered a word character.

**match word characters:**

```regex
/\w/g
```

```text
h
_
```

**match non-word characters:**

```regex
/\W/g
```

```text
9

-
```

## Custom Classes

_Custom classes_ allow you to define your own character classes. This is a set of characters or even predefined character classes to match using the [square bracket metacharacter `[]`](metacharacters.md). Think of anything inside the custom class as being part of an or statement to which only one will be matched (depending on the [quantifier](quantifiers.md) being used). Below are the different ways to define a custom class:

### Custom Class Character Literals

Custom classes can be as simple as listing a set of **character literal** like so `[aeiou]`. See below how that pattern will behave with the string `"hello"`.

```regex
/[aeiou]/g
```

```text
e
o
```

### Custom Class Range

To specify a **range** in a custom class a dash `-` is used such as `[a-z]`, `[A-Z]`, `[0-9]`. The ranges can be modified such as `[0-4]`, or combined like so `[a-zA-Z0-9]`. See how the regex below behaves with the string: `"bad foo"`.

```regex
/[f-z]+/g
```

```text
foo
```

> ![IMPORTANT]
> It is also possible to specify `[a-Z]` for any uppercase or lowercase letters but this is not recommended as some systems may include digits in the match.

### Custom Class Negation

It is also possible to **negate** everything that is inside the square brackets. This can be done using the [hat metacharacter `^`](metacharacters.md) like so `[^pattern]`. This is similar to how character classes have a negated version (word: `\w` & non-word: `\W`). See how the regex below behaves with the string: `he!1o`.

```regex
/[^a-z\d]/g
```

```text
!
```

<!--TODO
determine if Dot Wildcard should go here

why: it's not a character class but it also is good to learn
     alongside other character classes because it functions
     like them.
-->

## The Dot Wildcard

Although the dot wildcard (`.`) is not technically a character class, it has been placed here as it behaves in similar ways to the other character classes. This wildcard will match anything except newlines. However it can also match newlines by using the [dotall flag](flags.md) (`s`).The regex below will match any character in the string except newlines: `"%100 - 6\n hello"`.

```regex
/.+/g
```

```text
%100 - 6
 hello
```
