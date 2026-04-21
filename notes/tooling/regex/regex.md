# Tooling: Regex

_Regular expressions (**regex**)_ are sequences of characters and flags that define a search pattern. They are extremely powerful and allow programs to match, search, and manipulate text in an incredibly concise but expressive manner. Note that there are three main regex implementations: _Perl Compatible Regular Expressions (**PCRE**)_, _POSIX Extended Regular Expressions (**ERE**)_, and _POSIX Basic Regular Expressions (**BRE**)_.

## Notes

- [metacharacters](metacharacters.md)
- [character classes](character-classes.md)
- [anchors](anchors.md)
- [quantifiers](quantifiers.md)
- [flags](flags.md)
- [groups and capturing](groups-and-capturing.md)
- [lookaround assertions](lookaround-assertions.md)

> [!NOTE]
> Modern programming languages typically use a variation of **PCRE** but for most unix tooling such as grep the default is **BRE**. These notes will focus more on the modern **PCRE**, and **ERE** implementations. For the most part it is safe to assume patterns described here will work in your programming language of choice.
>
> [RegExr](https://regexr.com), and [regex101](https://regex101.com/r/D5mUTo/1?utm_source=chatgpt.com) are good resources for testing regex patterns, visualizing matches, and learning about regex syntax for different implementations.
