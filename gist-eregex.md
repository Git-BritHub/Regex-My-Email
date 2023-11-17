# Regex My Email

A Regular Expression (Regex) tutorial for matching an email

## Summary

In this tutorial, we'll be covering the regex components used to verify a user's provided email. The following regex is a simple and common one used for matching an email to ensure its validity:
### <code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code>
Depending on how strict you'd like your email validation process to be, the regex needed for matching an email will differ. Whether it's a character used specifically in our 'Matching an Email' regex or not, I'll go over what each character, symbol and expression does in great detail.</br>
For a complete regex quick-reference table and a quick break-down of the Regex characters, symbols and expressions that go into this 'Matching an Email' Regex, feel free to skip ahead to my [Brief Break-Down and Regex Cheatsheet](#brief-break-down-and-regex-cheatsheet) section of this tutorial. 

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
- [Brief Break-Down and Regex Cheatsheet](#brief-break-down-and-regex-cheatsheet)
- [Author](#author)

## Regex Components
A regex is considered a literal, so the pattern must be wrapped in forward facing slash characters `/`. As you'll notice, our regex example that matches an email has an opening and closing forward `/` for this very reason.
### <code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code>

### Anchors
Anchors are unique in that they match a position within a string, not a character.
In our 'Matching an Email' regex: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the characters `^` and `$` are both considered to be anchors. `^` signifies the beginning of the string while `$` signifies the end. </br>
For your reference, here is a table depicting anchors with their description:</br>

| Anchor | Description | Example |
| ------ | ----------- | ------- |
| ^ | `Beginning` Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled. | In the example 'she sells seashells', `^\w+` matches the word 'she'. |
| $ | `End` Matches the end of the string, or the end of a line if the multiline flag (m) is enabled. | In the example 'she sells seashells', `\w+$` matches the word 'seashells'. |
| \b | `Word Boundary` Matches a word boundary position between a word character and non-word character or position (start / end of string). | In the example 'she sells seashells', `s\b` matches the letters 's' in 'she sells`s` seashell`s`'. |
| \B | `Not Word Boundary` Matches any position that is not a word boundary. This matches a position, not a character. | In the example 'she sells seashells', `s\B` matches the letters 's' in '`s`he `s`ells `s`ea`s`hells'. |

### Quantifiers
Quantifiers indicate that the preceding token must be matched a certain number of times. By default, quantifiers are greedy and will match as many characters as possible! In our 'Matching an Email' regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the `{2,6}` portion of our regex is a quantifier and it matches 2 to 6 lowercase letters or dots for the TLD part of a web address (.com, .net, .uk, etc). </br>
For example, let's say we have email addresses named `email@example.com` or `email@example.co`. Both email addresses would be accepted as a match and validated since `.com` and `.co` fall within the 2-6 character range. An email such as `email@example.c` or `email@example.coooooom` would not pass email validation.</br>
Another Quantifier being used is the `+` quantifier. The `+` ensures that there must be at least one character in the email/username and allows for the username portion to be one or more characters long.</br>
For your reference, here is a table depicting quantifiers with their description:</br>

| Quantifiers | Description | Example |
| ----------- | ----------- | ------- |
| * | `Star` Matches 0 or more of the preceding item. | In the example 'b be bee beer beers', `b\w*` matches '`b``be``bee``beer``beers`'. |
| + | `Plus` Matches 1 or more of the preceding item. | In the example 'b be bee beer beers', `b\w+` matches 'b `be` `bee` `beer` `beers`'. |
| ? | `Optional` Matches 0 or 1 of the preceding item, effectively making it optional. | In the example 'color colour', `coulou?r` matches both '`color` `colour`'. |
| {n,m} | `Quantifier`: `{n,m}` matches between `n` and `m`. | `{2,6}` will match 2 to 6 like in our example above. | 
| {n} | `Quantifier`: `{n}` matches exactly `n` occurences. | `{6}` will match exactly 6. |
| {n,} | `Quantifier`: `{n,}`matches at least `n` occurences. | `{6,}`, will match 6 or more. |
| {n,x} | `Quantifier`: `{n,x}` matches the pattern from a minimum of `n` number of times to a maximum of `x` number of times. |  |

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
So in regards to our regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` for matching an email, the implimentation of character classes are vital in quickly and effeciently ensuring that an email address provided by the user is valid. The character classes enclosed within the `[]` brackets, `[a-z0-9_\.-]`, are telling us that our email can have any letter from 'a' to 'z', any numbers from 0 to 9, as well as the option to include an underscore `_`, a dot `.`, or a hyphen `-`.</br>
The next character set `[\da-z\.-]`. While very similar to our previous mentioned character set, a new character class that we have not yet discussed is `\d`. `\d` is a shorthand character class that represents any digit from 0-9. Why use `\d` as opposed to `0-9` you may ask? Using `\d` is more concise and improves readability, especially when dealing with more complex regular expressions. </br>
Our final character set `[a-z\.]` uses characters classes that tell us what are email is allowed to have within its TLD (top-level domain) portion of the email address. Here, a-z is telling us again that any letter from 'a' to 'z' are allowed, as well as the dot `.`.</br>
Below is a table that includes additional character classes for your reference:

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
In our 'Matching an Email' Regex, there are no flags used in this regex. Flags modify how the regular expression is interpreted, but none are specified here. However, I have provided a table below of Flags for your reference:

| Flags | Description | Example |
| ----- | ----------- | ------- |
| i | `Ignore Case` makes the whole expression case-insensitive. | / aBc/i would match AbC |
| g | `Global Search` retains the index of the last match, allowing subsequent searches to start from the end of the previous match. | Without the global flag `g`, subsequent searches will return the same match. |
| m | `Multiline` will match the start and end of a line with beginning and end anchors `^` and `$` when the multiline flag is enabled. | Something to note: Patterns such as `/^[\s\S]+$/m` may return matches that span multiple lines because the anchors will match the start/end of any line | 
| u | `Unicode` can use extended unicode escapes in the form `\x{FFFFF}` when enabled. | Something to note: It also makes other escapes stricter, causing unrecognized escapes, for example: `\j` to throw an error. |
| y | `Sticky` will only match from its lastIndex position and ignores the global `g` flag if set. |  |
| s | `Dotall` or `Dot` `.` will match any character, including newline. |  |

### Grouping and Capturing
Groups allow you to combine a sequence of tokens to operate on them together. Capture groups can be referenced by a backreference and accessed separately in the results. In our 'Matching an Email' Regex, `([a-z0-9_\.-]+)` is the capturing group for the username part of the email. The parenthesis `()` are used to define it, the content matched by this group will be captured for further use or extraction. Our next capturing group, `([\da-z\.-]+)` is for the domain name part of the email. Similar to our first capture group that is also enclosed in `()`, it contains the character classes enclosed in `[]`brackets. The final Capture Group in our 'Matching an Email' Regex involves `([a-z\.]{2,6})`; which is used for the top-level domain (TLD) part of the email.
For reference, I've included a table of Groups and Capturing below:

| Groups & Capturing | Description | Example |
| ------------------- | ----------- | ------- |
| (ABC) | `Capturing Group` groups multiple tokens together and creates a capture group for extracting a substring or using a backreference. | Using `(ha)+` for 'hahaha haa hah!' will capture the `ha``ha``ha` `ha`a `ha`h! portion of it |
| (?<name>ABC) | `Named Capturing Group` creates a capturing group that can be referenced via the specified name. |  |
| \1 | `Numeric Reference` matches the results of a capture group. | \1 matches the results of the first capture group & \3 matches the third. In the example `(\w)a\1`, `hah` `dad` bad dab `gag` gab would be matched in 'hah dad bad dab gag gab'. |
| (?:ABC) | `Non-Capturing Group` groups multiple tokens together without creating a capture group. | In 'hahaha haa hah!', `(?:ha)+` would match `hahaha` `ha`a `ha`h!. |

### Bracket Expressions
Anything inside a set of square brackets `[]` represents a range of characters that we want to match. Thes patterns are known as bracket expressions, but they are also known as a positive character group because they outline the characters we want to include. It's important to note that a bracket expression can be turned into a `negative character group` by adding the `^` symbol to the beginning of the expression inside the brackets. For reference, I've included a table of Bracket Expressions below:

| Bracket Expressions | Description | Example |
| ------------------- | ----------- | ------- |
| [a-z] | The string can contain any lowercase letter between letters a-z | `[a-d]` would include and match the lowercase letters 'a', 'b', 'c', and 'd'. |
| [A-Z] | The string can contain any uppercase letter between letters A-Z | `[D-H]` would include and match the uppercase letters 'D', 'E', 'F', 'G', and 'H'. |
| [0-9] | The string can contain any number between 0-9. | `[1-4]` would only include or match numbers '1', '2', '3', and '4'. |
| [_-] | The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. In this case, we only want t astring that includes `_` or `-`. | Important to note: the hyphen `-` is NOT the same hyphen that we used in our aplhanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric charcter ranges within the brackets. |

### Greedy and Lazy Match
As mentioned above in the [Quantifiers](#quantifiers) section, `Quantifiers` are inherently `greedy`. They match as many occurences of particular patterns as possible. Each of these quantifierrs can be made `lazy` by adding the `?` symbol after it, meaning it will match as few occurences as possible. For example, in the lazy quantifier `b\w+?` the following charcters would be matched: 'b `be` `be`e `be`er `be`ers'. In our 'Matchin an Email' Regex, the greedy quantifier `+` is used in a couple of Capturing groups to allow for the username portion and domain name portion to be one or more characters long.</br>
Feel free to take another look at the table provided in the [Quantifiers](#quantifiers) section to view these `greedy` quantifiers and remember that adding the `?` symbol to any of those quantifiers will make them `lazy`.

### Boundaries
Boundaries indicate the beginnings and endings of lines and words, and other patters indicating in some way that a match is possible. These inlcude `look-ahead`, `look-behind` (of which we'll cover in a couple of sections), along with conditional expressions. These boundaries include the characters `^`, `$`, `\b`, and `\B` that we covered in the [Anchors](#anchors) section above. As well as `x(?=y)`, `x(?!y)`, `(?<=y)x`, and `(?<!y)x` that we will cover in the [Look-ahead and Look-behind](#look-ahead-and-look-behind) section. 

### Back-references
Groups group multiple patterns as a whole, and capturing groups provide extra submatch information when using a regular expression pattern to match against a string. Backreferences refer to a previously captured group in the same regular expression. For reference, I've included a table of Back-References below:

| Back-Reference | Description | Example |
| -------------- | ----------- | ------- |
| \n | Where `n` is a positive integer, a back-reference to the last substring matching the `n` parenthetical in the regular expression. | `/apple(,)\sorange\1/` matches 'apple, orange' in 'apple, orange, cherry, peach'. |
| \k<Name> | A back-reference to the last substring matching the 'Named Capture Group' specified by `<Name>`. | `/(?<title>\w+)`, yes `\k<title>/` matches 'Sir, yes Sir' in 'Do you copy? Sir, yes Sir!'. In this example, `\k` is used literally to indicate the beginning of a back reference to a Named capture group. |

### Look-ahead and Look-behind
`Lookaround` lets you match a group before (`Lookbehind`) or after (`Lookahead`) your main pattern withough including it in the result. Negative lookarounds specify a group that can NOT match before or after the pattern. For reference, I've included a table of Lookaheads and Lookbehinds below:

| Lookahead & Lookbehind | Description | Example |
| ---------------------- | ----------- | ------- |
| (?=ABC) | `Positive Lookahead` matches a group after the main expression without including it in the result. | In the example of '1pt 2px 3em 4px', `\d(?=px)` matches '1pt `2`px 3em `4`px'. |
| (?!ABC) | `Negative Lookahead` specifies a group that cannot match after the main expression. If it matches, the result is discarded. | In the example of '1pt 2px 3em 4px', `\d(?!px)` matches '`1`pt 2px `3`em 4px'. |
| (?<=ABC) | `Positive Lookbehind` matches a group before the main expression without including it in the result. |  |
| (?<!ABC) | `Negative Lookbehind` specifies a group that cannot match before the main expression. If it matches, the result is discarded. |  |
| x(?=y) | `Lookahead Assertion` matches `x` only if `x` is followed by `y`. | `/Jack(?=Sprat)/` matches 'Jack' only if it is followed by 'Sprat'. `/Jack(?=Sprat|Frost)/` matches 'Jack' only if it is followed by 'Sprat' or 'Frost'. However, neither 'Sprat' nor 'Frost' is part of the match results. |
| x(?!y) | `Negative Lookahead Assertion` matches `x` only if `x` is not followed by `y`. | `/\d+(?!\.)/` matches a number only if it is not followed by a decimal point. `/\d+(?!\.)/.exec('3.141')` matches '141' but not '3'. |
| (?<=y)x | `Lookbehind Assertion` matches `x` only if `x` is preceded by `y`. | `/(?<=Jack)Sprat/` matches 'Sprat' only if it is preceded by 'Jack'. `/(?<=Jack|Tom)Sprat/` matches 'Sprat' only if it is preceded by 'Jack' or 'Tom'. However, neither 'Jack' nor 'Tom' is part of the match results. |
| (?<!y>)x | `Negative Lookbehind Assertion` | `/(?<!-)\d+/` matches a number only if it is not preceded by a minus sign. `/(?<!-)\d+/.exec('3')` matches "3". `/(?<!-)\d+/.exec('-3')` match is not found because the number is preceded by the minus sign. |

## Brief Break-Down and Regex Cheatsheet
### <code> /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ </code>
1. Anchors:
    * `^`: Asserts the start of the string.
    * `$`: Asserts the end of the string.
2. Quantifiers:
    * `+`: Matches one or more occurrences of the preceding element.
    * `{2,6}`: Specifies a range; in this case, it matches between 2 and 6 occurrences.
3. Character Classes:
    * `[a-z0-9_\.-]`: Matches any lowercase letter, digit, underscore, dot, or hyphen.
    * `[\da-z\.-]`: Matches any digit, lowercase letter, dot, or hyphen.
    * `[a-z\.]`: Matches any lowercase letter or dot.
4. Flags:
    * There are no flags used in this regex. Flags modify how the regular expression is interpreted, but none are specified here.
5. Grouping and Capturing:
    * ([a-z0-9_\.-]+): Capturing group for the username part of the email.
    * ([\da-z\.-]+): Capturing group for the domain name part of the email.
    * ([a-z\.]{2,6}): Capturing group for the top-level domain (TLD) part of the email.
6. Bracket Expressions:
    * [a-z0-9_\.-]: Defines a character class for the username.
    * [\da-z\.-]: Defines a character class for the domain name.
    * [a-z\.]: Defines a character class for the TLD.
7. Greedy and Lazy Match:
    * Greedy matching is the default behavior where the quantifier matches as much as possible. In our email regex, `+` is greedy.
8. Boundaries:
    * The `^` and `$` anchors mark the boundaries of the entire string.
9. Back References:
    * There are no back references in this regex. Back references are used to match the same text as previously matched by a capturing group.
10. Look Ahead and Look Behind:
    * There are no look-ahead or look-behind assertions used in this regex. Look-ahead and look-behind assertions are used to ensure that a certain condition is (or is not) met without including it in the match.</br>
In short, this regex is designed to validate an email address by breaking it into three main parts: the username, the domain name, and the top-level domain (TLD). It enforces specific character classes for each part and ensures proper structure and length for the email address.



| Characters | Description | Example |
| ---------- | ----------- | ------- |
| `Anchors` |
| ^ | `Beginning` Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled. | In the example 'she sells seashells', `^\w+` matches the word 'she'. |
| $ | `End` Matches the end of the string, or the end of a line if the multiline flag (m) is enabled. | In the example 'she sells seashells', `\w+$` matches the word 'seashells'. |
| \b | `Word Boundary` Matches a word boundary position between a word character and non-word character or position (start / end of string). | In the example 'she sells seashells', `s\b` matches the letters 's' in 'she sells`s` seashell`s`'. |
| \B | `Not Word Boundary` Matches any position that is not a word boundary. This matches a position, not a character. | In the example 'she sells seashells', `s\B` matches the letters 's' in '`s`he `s`ells `s`ea`s`hells'. |
| `Quantifiers` |
| * | `Star` Matches 0 or more of the preceding item. | In the example 'b be bee beer beers', `b\w*` matches '`b``be``bee``beer``beers`'. |
| + | `Plus` Matches 1 or more of the preceding item. | In the example 'b be bee beer beers', `b\w+` matches 'b `be` `bee` `beer` `beers`'. |
| ? | `Optional` Matches 0 or 1 of the preceding item, effectively making it optional. | In the example 'color colour', `coulou?r` matches both '`color` `colour`'. |
| {n,m} | `Quantifier`: `{n,m}` matches between `n` and `m`. | `{2,6}` will match 2 to 6 like in our example above. | 
| {n} | `Quantifier`: `{n}` matches exactly `n` occurences. | `{6}` will match exactly 6. |
| {n,} | `Quantifier`: `{n,}`matches at least `n` occurences. | `{6,}`, will match 6 or more. |
| {n,x} | `Quantifier`: `{n,x}` matches the pattern from a minimum of `n` number of times to a maximum of `x` number of times. |  |
| `OR Operator` |
| I | `Alternation` acts like a boolean OR. Matches the expression before or after this alternation. It can operate within a group or on a whole expression. The patterns will be tested in order. |  |
| `Character Classes` |
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
| `Flags` |
| i | `Ignore Case` makes the whole expression case-insensitive. | / aBc/i would match AbC |
| g | `Global Search` retains the index of the last match, allowing subsequent searches to start from the end of the previous match. | Without the global flag `g`, subsequent searches will return the same match. |
| m | `Multiline` will match the start and end of a line with beginning and end anchors `^` and `$` when the multiline flag is enabled. | Something to note: Patterns such as `/^[\s\S]+$/m` may return matches that span multiple lines because the anchors will match the start/end of any line | 
| u | `Unicode` can use extended unicode escapes in the form `\x{FFFFF}` when enabled. | Something to note: It also makes other escapes stricter, causing unrecognized escapes, for example: `\j` to throw an error. |
| y | `Sticky` will only match from its lastIndex position and ignores the global `g` flag if set. |  |
| s | `Dotall` or `Dot` `.` will match any character, including newline. |  |
| `Groups & Capturing` |
| (ABC) | `Capturing Group` groups multiple tokens together and creates a capture group for extracting a substring or using a backreference. | Using `(ha)+` for 'hahaha haa hah!' will capture the `ha``ha``ha` `ha`a `ha`h! portion of it |
| (?<name>ABC) | `Named Capturing Group` creates a capturing group that can be referenced via the specified name. |  |
| \1 | `Numeric Reference` matches the results of a capture group. | \1 matches the results of the first capture group & \3 matches the third. In the example `(\w)a\1`, `hah` `dad` bad dab `gag` gab would be matched in 'hah dad bad dab gag gab'. |
| (?:ABC) | `Non-Capturing Group` groups multiple tokens together without creating a capture group. | In 'hahaha haa hah!', `(?:ha)+` would match `hahaha` `ha`a `ha`h!. |
| `Bracket Expressions` |
| [a-z] | The string can contain any lowercase letter between letters a-z | `[a-d]` would include and match the lowercase letters 'a', 'b', 'c', and 'd'. |
| [A-Z] | The string can contain any uppercase letter between letters A-Z | `[D-H]` would include and match the uppercase letters 'D', 'E', 'F', 'G', and 'H'. |
| [0-9] | The string can contain any number between 0-9. | `[1-4]` would only include or match numbers '1', '2', '3', and '4'. |
| [_-] | The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. In this case, we only want t astring that includes `_` or `-`. | Important to note: the hyphen `-` is NOT the same hyphen that we used in our aplhanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric charcter ranges within the brackets. |
| `Back-Reference` |
| \n | Where `n` is a positive integer, a back-reference to the last substring matching the `n` parenthetical in the regular expression. | `/apple(,)\sorange\1/` matches 'apple, orange' in 'apple, orange, cherry, peach'. |
| \k<Name> | A back-reference to the last substring matching the 'Named Capture Group' specified by `<Name>`. | `/(?<title>\w+)`, yes `\k<title>/` matches 'Sir, yes Sir' in 'Do you copy? Sir, yes Sir!'. In this example, `\k` is used literally to indicate the beginning of a back reference to a Named capture group. |
| `Lookahead & Lookbehind` |
| (?=ABC) | `Positive Lookahead` matches a group after the main expression without including it in the result. | In the example of '1pt 2px 3em 4px', `\d(?=px)` matches '1pt `2`px 3em `4`px'. |
| (?!ABC) | `Negative Lookahead` specifies a group that cannot match after the main expression. If it matches, the result is discarded. | In the example of '1pt 2px 3em 4px', `\d(?!px)` matches '`1`pt 2px `3`em 4px'. |
| (?<=ABC) | `Positive Lookbehind` matches a group before the main expression without including it in the result. |  |
| (?<!ABC) | `Negative Lookbehind` specifies a group that cannot match before the main expression. If it matches, the result is discarded. |  |
| x(?=y) | `Lookahead Assertion` matches `x` only if `x` is followed by `y`. | `/Jack(?=Sprat)/` matches 'Jack' only if it is followed by 'Sprat'. `/Jack(?=Sprat|Frost)/` matches 'Jack' only if it is followed by 'Sprat' or 'Frost'. However, neither 'Sprat' nor 'Frost' is part of the match results. |
| x(?!y) | `Negative Lookahead Assertion` matches `x` only if `x` is not followed by `y`. | `/\d+(?!\.)/` matches a number only if it is not followed by a decimal point. `/\d+(?!\.)/.exec('3.141')` matches '141' but not '3'. |
| (?<=y)x | `Lookbehind Assertion` matches `x` only if `x` is preceded by `y`. | `/(?<=Jack)Sprat/` matches 'Sprat' only if it is preceded by 'Jack'. `/(?<=Jack|Tom)Sprat/` matches 'Sprat' only if it is preceded by 'Jack' or 'Tom'. However, neither 'Jack' nor 'Tom' is part of the match results. |
| (?<!y>)x | `Negative Lookbehind Assertion` | `/(?<!-)\d+/` matches a number only if it is not preceded by a minus sign. `/(?<!-)\d+/.exec('3')` matches "3". `/(?<!-)\d+/.exec('-3')` match is not found because the number is preceded by the minus sign. |

## Author
This tutorial was created by [Brittany Brimley](https://github.com/Git-BritHub). As a software developer, I am always 'nerdy happy' when I come across a nice and straightforward tutorial or cheatsheet for quick references. Whether you are new to software development or a more experienced developer looking for a quick reference tool, my hope is that this tutorial will provide that 'nerdy joy' and give you more time to focus on other aspects of your project. Please don't hesitate to reach out through GitHub if you have any questions or suggestions that could help further improve this tutorial. 