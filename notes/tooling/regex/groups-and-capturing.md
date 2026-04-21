# Regex: Groups and Capturing

Parentheses `()` are used to group parts of a regex pattern together. This allows you to apply [quantifiers](quantifiers.md) to multiple characters at once, use alternation, or capture matched text for later use.

## Basic Grouping

Groups allow you to treat multiple characters as a single unit. For example, see how the regex below behaves with the string `"ha haha hahaha"`.

```regex
/(ha)+/g
```

```text
ha
haha
hahaha
```

## Capture Groups

By default, groups capture the matched text and store it for later use. These captured values can be referenced within the same regex using backreferences (`\1`, `\2`, etc.) or accessed after the match in your programming language. Capture groups are good for matches a broader pattern but only needing specific parts of the match to be returned or split into different groups.

### Example: Multiple Capture Groups

You can use multiple capture groups and reference them by their order. See how the pattern below can easily parse this git data to retrieve the number of insertions: `"3 files changed, 105 insertions(+), 13 deletions(-)"`.

```regex
/(\d+) insertions/
```

```text
match:
105 insertions

capture groups:
\1 = 105
```

### Example: Backreferences

The pattern below matches repeated words using a backreference. See how it works with the string `"hello hello world hello world"`.

```regex
/(\w+) \1/g
```

```text
hello hello
```

## Non-Capturing Groups

Non-capturing groups use the syntax `(?:...)` to group patterns without storing the matched text. This is useful when you need grouping for quantifiers or alternation but don't want to capture the result. Note that this is unnecessary if you are doing no other captures. You should only use this if you don't want to clutter your other capture groups.

**Example:**

See how the pattern below matches repeated "abc" sequences without capturing them in the string `"abc abcabc foo"`.

```regex
/(?:abc)+/g
```

```text
abc
abcabc
```

## Named Capture Groups

Named capture groups use the syntax `(?<name>...)` to assign a descriptive name to a captured group. This makes code more readable and maintainable but is not available in all regex versions.

**Example:**

The pattern below captures a word with a descriptive name from the string `"Hello world"`.

```regex
/(?<greeting>\w+) (?<target>\w+)/
```

```text
match:
Hello world

capture groups:
groups.greeting = "Hello"
groups.target = "world"
```

## Alternation

The pipe character `|` allows you to match one pattern or another (logical OR). It can be used with or without groups depending on the scope you need.

### Example: Alternation without Groups

The pattern below matches either "cat" or "dog" in the string `"I have a cat and a dog"`.

```regex
/cat|dog/g
```

```text
cat
dog
```

### Example: Alternation with Groups

Using groups allows you to limit the scope of alternation. See how the pattern below matches file extensions in the string `"file.jpg image.png doc.pdf"`.

```regex
/\w+\.(jpg|png|gif)/g
```

```text
file.jpg
image.png
```
