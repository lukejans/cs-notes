# Regex: Lookaround Assertions

Lookaround assertions allow you to match patterns based on the presence or absence of other patterns around it without consuming that text.

| Assertion | Lookahead     | Lookbehind     |
| --------- | ------------- | -------------- |
| Positive  | `(?=pattern)` | `(?<=pattern)` |
| Negative  | `(?!pattern)` | `(?<!pattern)` |

Below are some examples of lookaround assertions:

## Example: Positive Lookahead

The pattern matches digits that are followed by `px` but not `px` itself. Using the string `"9 32px 4 px"` see below how it works:

```regex
/\d+(?=px)/
```

```text
32
```

## Example: Negative Lookahead

Here the pattern matches digits that are not followed by `px`. Using the string `"9 32px 4 px"` see below how it works:

```regex
/\d+(?!px)/
```

```text
9
3
4
```

## Example: Positive Lookbehind

Here the pattern matches digits that are preceded by `#`. Using the string `"# 74 #1 #203"` see below how it works:

```regex
/(?<=#)\d+/
```

```text
1
203
```

## Example: Negative Lookbehind

Here the pattern matches digits that are not preceded by `#`. Using the string `"# 74 #1 #203"` see below how it works:

```regex
/(?<!#)\d+/
```

```text
74
03
```
