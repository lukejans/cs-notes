# Regex: Metacharacters

Metacharacters are characters with special meanings in regex. To match them literally they must be escaped them with a backslash (`\`).

| Character | Meaning                                                      | POSIX (BRE) |
| --------- | ------------------------------------------------------------ | ----------- |
| `.`       | [Matches any character except newline](character-classes.md) |             |
| `^`       | [Matches the start](anchors.md)                              |             |
| `$`       | [Matches the end](anchors.md)                                |             |
| `?`       | [Matches Zero or one](quantifiers.md)                        | `\\?`       |
| `*`       | [Matches Zero or more](quantifiers.md)                       |             |
| `+`       | [Matches One or more](quantifiers.md)                        | `\\+`       |
| `\|`      | [Alternation or set union (OR)](groups-and-capturing.md)     | `\\\|`      |
| `()`      | [Grouping](groups-and-capturing.md)                          | `\\(...\\)` |
| `[]`      | [Character class to match](character-classes.md)             |             |
| `[^]`     | [Character class to **NOT** match](character-classes.md)     |             |
| `{m,n}`   | [Matches between m and n times](quantifiers.md)              | `\\{m,n\\}` |
| `\\`      | Escape character                                             |             |
| `\1`...   | [Backreference to captured group](groups-and-capturing.md)   | `\\1`       |

## Matching an Escape Sequence

When some non-metacharacters (character literals) are paired with the escape character (`\`) they are used to match escape sequences. This includes things like `\t` for tab and `\n` for newline, and `\r` for carriage return. The pattern would look like so to match a tab character: `/\\t/`.

## POSIX Metacharacters

In _POSIX Basic Regular Expression (BRE)_, _Metacharacters_ have no meaning unless they are escaped. This is the opposite of _Perl Compatible Regular Expressions (PCRE)_ and _POSIX Extended Regular Expression (ERE)_, where metacharacters have special meanings by default unless escaped to match a literal.
