# Regex My Email

A Regular Expression (Regex) tutorial for matching an email

## Summary

In this tutorial, we'll be covering the regex components used to verify a user's provided email. The following regex is a simple and common one used for matching an email to ensure its validity:
<br><code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code></br>
Depending on how strict you want your email validation process to be, the regex needed for matching an email will differ. We'll go over what each character and symbol does with a quick and simple description.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components
A regex is considered a literal, so the pattern must be wrapped in forward facing slash characters `/`. As you'll notice, our regex example that matches an email has an opening and closing forward `/` for this very reason.
<br><code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code></br>

### Anchors
Anchors are unique in that they match a position within a string, not a character.
In our 'Matching an Email' regex: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the characters `^` and `$` are both considered to be anchors. `^` signifies the beginning of the string while `$` signifies the end. </br>
For your reference, here is a table depicting anchors with their description:</br>

| Anchor | Description |
| ------ | ----------- |
| ^ | `Beginning` Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled. |
| $ | `End` Matches the end of the string, or the end of a line if the multiline flag (m) is enabled. |
| \b | `Word Boundary` Matches a word boundary position between a word character and non-word character or position (start / end of string). |
| \B | `Not Word Boundary` Matches any position that is not a word boundary. This matches a position, not a character. |

### Quantifiers
Quantifiers indicate that the preceding token must be matched a certain number of times. By default, quantifiers are greedy and will match as many characters as possible! In our 'Matching an Email' regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the `{2,6}` portion of our regex is a quantifier and it matches 2 to 6 lowercase letters or dots for the TLD part of a web address.</br>
For example, let's say we have email addresses named `email@example.com` or `email@example.co`. Both email addresses would be accepted as a match and validated since `.com` and `.co` fall within the 2-6 character range. An email such as `email@example.c` or `email@example.coooooom` would not pass email validation.</br>
For your reference, here is a table depicting quantifiers with their description:</br>

| Quantifiers | Description |
| ----------- | ----------- |
| + | `Plus` Matches 1 or more of the preceding item. |
| * | `Star` Matches 0 or more of the preceding item. |
| ? | `Optional` Matches 0 or 1 of the preceding item, effectively making it optional. |
| {n,m} | `Quantifier`: `{n,m}` matches between `n` and `m`. For example, `{2,6}` will match 2 to 6 like in our example above. | 
| {n} | `Quantifier`: `{n}` matches exactly `n` occurences. For example example, `{6}` will match exactly 6. |
| {n,} | `Quantifier`: `{n,}`matches at least `n` occurences. For for example, `{6,}`, will match 6 or more. |

### OR Operator

### Character Classes

### Flags

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

This tutorial was created by [Brittany Brimley](https://github.com/Git-BritHub). As a software developer, I am always 'nerdy happy' when I come across a nice and straightforward tutorial or cheat-sheet for quick references. Whether you are new to software development or a more experienced developer looking for a quick reference tool, my hope is that this tutorial will provide that 'nerdy joy' and give you more time to focus on other aspects of your project. Please don't hesitate to reach out through GitHub if you have any questions or suggestions that could help further improve this tutorial. 