# Regex My Email

A Regular Expression (Regex) tutorial for matching an email

## Summary

In this tutorial, we'll be covering the regex components used to verify a user's provided email. The following regex is a simple and common one used for matching an email to ensure its validity:
<br><code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code></br>
Depending on how strict you'd like your email validation process to be, the regex needed for matching an email will differ. We'll go over what each character and symbol does with a detailed description of each type.

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
Quantifiers indicate that the preceding token must be matched a certain number of times. By default, quantifiers are greedy and will match as many characters as possible! In our 'Matching an Email' regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the `{2,6}` portion of our regex is a quantifier and it matches 2 to 6 lowercase letters or dots for the TLD part of a web address (.com, .net, .uk, etc). </br>
For example, let's say we have email addresses named `email@example.com` or `email@example.co`. Both email addresses would be accepted as a match and validated since `.com` and `.co` fall within the 2-6 character range. An email such as `email@example.c` or `email@example.coooooom` would not pass email validation.</br>
For your reference, here is a table depicting quantifiers with their description:</br>

| Quantifiers | Description |
| ----------- | ----------- |
| * | `Star` Matches 0 or more of the preceding item. |
| + | `Plus` Matches 1 or more of the preceding item. |
| ? | `Optional` Matches 0 or 1 of the preceding item, effectively making it optional. |
| {n,m} | `Quantifier`: `{n,m}` matches between `n` and `m`. For example, `{2,6}` will match 2 to 6 like in our example above. | 
| {n} | `Quantifier`: `{n}` matches exactly `n` occurences. For example example, `{6}` will match exactly 6. |
| {n,} | `Quantifier`: `{n,}`matches at least `n` occurences. For for example, `{6,}`, will match 6 or more. |

### OR Operator
An OR Operator is a logical operator used in programming and various other contexts to perform a choice between two or more alternatives. In a regex, the symbol `|` acts as an OR Operator. How is this useful to our regex `^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$` you may ask? In this instance, you could use this alternation `|` to match email addresses from different email providers like Gmail, Yahoo, Outlook, etc. For example:</br>
`^([a-z0-9_\.-]+)@(gmail\.com|yahoo\.com|outlook\.com)$`</br>
In this regex that inputs `|` after each TDL, it proceeds to match email address with the local part followed by one of the specified domain names such as the email providers I mentioned above.</br>
You can also use an OR Operator to match email domains with or without subdomains like in the following example:</br>
`^([a-z0-9_\.-]+)@(([\da-z\.-]+\.[a-z\.]{2,6})|([a-z\.-]+\.[a-z\.]{2,6}))$`</br>
This regex example allows for domain names like 'example.com' or 'sub.example.com' to be used.</br></br>
In short, the OR Operator `|` allows you to specify multiple alternative patterns! 

### Character Classes
A character class in a regex defines a set of characters. There are a number of predefined character classes and you can also define your own sets!</br>
So in regards to our regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` for matching an email, the implimentation of character classes are vital in quickly and effeciently ensuring that an email address provided by the user is valid. For example, the portion enclosed with brackets `[]` in our regex that displays `a-z` (referred to as `Range`) is telling us that a valid email can inlcude letters that range all the way from `"a"` to `"z"`.  Below is a table of more character classes for your reference:</br>

| Character Classes | Description | Example |
| ----------------- | ----------- | ------- |
| [ABC] | `Character Set` matches any character in the set. | If desiring to find/match the letters "b" or "d" you'd use `[bd]` |
| [^ABC] | `Negated Set` matches any character that is not in the set. | If desiring to find/match all letters besides `"h"` or `"o"` in the word `"hello"`, only the letters `"ell"` would match or be considered valid. |
| [A-Z] | `Range` matches a character having a character code between the two specified characters inclusive. | If wanting to match or validate all letters of the alphabet, including `a-z` in brackets `[]` like `[a-z]` would allow this. If you did `[c-f]`, only the letters "c", "d", "e" |
| . | `Dot` matches any character except the newline characters/linebreakes. `.` is equivalent to `[^\n\r]`. | If you have the regex pattern `a.b`, it could match "aab", "axb", "a1b" "a@b" and so on. |
| \s | `Match Any: Whitespace` matches a single whitespace character, including spaces, tabs, and line breaks. | If using `\s` in a phrase or sentence that has spaces inbetween words, those spaces would be matched. | 
| \S | `Match Any: Not Whitespace` matches any character that is NOT a whitespace character | If using `\S`, everything but spaces, tabs or linebreaks would match. |
| \w | `Word` matches any word character (alphanumeric & underscore). Only matches low-ascii characters (no accented or non-roman characters). | Equivalent to [A-Za-z0-9_]. |
| \W | `Not Word` matches any character that is NOT a word character (alphanumeric & underscore). | Equivalent to [^A-Za-z0-9_]. |
| \d | `Digit` matches any digit character (0-9). | Equivalent to [0-9]. |
| \D | `Not Digit` matches any character that is not a digit character (0-9). | Equivalent to [^0-9]. |

### Flags

| Flags | Description | Example |
| ----- | ----------- | ------- |
| i | `Ignore Case` makes the whole expression case-insensitive. | / aBc/i would match AbC |
| g | `Global Search` retains the index of the last match, allowing subsequent searches to start from the end of the previous match. | Without the global flag `g`, subsequent searches will return the same match. |
| m | `Multiline` will match the start and end of a line with beginning and end anchors `^` and `$` when the multiline flag is enabled. | Something to note: Patterns such as `/^[\s\S]+$/m` may return matches that span multiple lines because the anchors will match the start/end of any line | 
| u | `Unicode` can use extended unicode escapes in the form `\x{FFFFF}` when enabled. | Something to note: It also makes other escapes stricter, causing unrecognized escapes, for example: `\j` to throw an error. |
| y | `Sticky` will only match from its lastIndex position and ignores the global `g` flag if set. |  |
| s | `Dotall` or `Dot` `.` will match any character, including newline. |  |

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

This tutorial was created by [Brittany Brimley](https://github.com/Git-BritHub). As a software developer, I am always 'nerdy happy' when I come across a nice and straightforward tutorial or cheat-sheet for quick references. Whether you are new to software development or a more experienced developer looking for a quick reference tool, my hope is that this tutorial will provide that 'nerdy joy' and give you more time to focus on other aspects of your project. Please don't hesitate to reach out through GitHub if you have any questions or suggestions that could help further improve this tutorial. 