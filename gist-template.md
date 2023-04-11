# Regex Tutorial on MAtching an email

Regular expressions can be used to find certain patterns of characters within a string. You can also find and replace a character or sequence of characters within a string. They are also frequently used to validate input. This regex matches character information for valid e-mail addresses.

## Summary

This is the regex code that we will be anaylizing today is: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Table of Contents

- [Anchors](#anchors) `^` `$`
- [Quantifiers](#quantifiers) `+` `{}`
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)`[a-z\d]`
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing) `([a-z0-9_.-]+)`
- [Bracket Expressions](#bracket-expressions) `[]`
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)


## Regex Components

### Anchors
- `^` You can use the caret symbol `(^)` at the end of a regular expression to indicate that a match must occur at the beginning of the searched text 

matches at the beginning of the target string
- `$` You can use the dollar symbol `($)` at the start of a regular expression to indicate that a match must occur at the
text ending of content or text searched

`/^[content]$/`


^abc$	start / end of the string

The caret `^` matches the position before the first character in the string. Applying `^a` to `abcd` matches `a`. ^b and ^c does not match `abcd` at all, because the b and c cannot be matched right after the start of the string, matched by `^`. See below for the inside view of the regex engine.
Similarly, `$` matches right after the last character in the string. `d$` matches `d` in abc, while a$ does not match at all.

In regular expressions, anchors mark the beginning and end of a string, line, or word. The beginning of the email string is marked by `^` and the end is marked by `$`.
/^[content]$/
A start of a new line of string would be marked by `^` and ended with a `$`


### Quantifiers
/`^`([a-z0-9_\.-]`+`)@([\da-z\.-]`+`)\.([a-z\.]{2,6})`$`/  <br>
 - `*`   representing `0` or more occurrences of the atom,
 - `+`   representing `1` or more occurrence of the atom,
 - `?`   representing `0` or `1` occurrences of the atom,
 - the bound `{n}`   representing exactly n occurrences of the atom,
 - the bound `{m,n}`   representing between m and n occurrences of the atom.

When we used `+` to communicate there should be another sequence to be matched as a greedy quantifier.  Example `{n,m}` or `{3,9}` as another greedy quantifer to specify the input should be a minimum of `2` characrtors to a maximum of `9` characters.

This regex uses two different types of quantifiers. The first can be found in two places
`([a-z0-9_\.-]+)`
`([a-z\.]{2,6})`

### OR Operator
An OR operator is an indicator that splits characters which allows that the character could match one or the other. 
For example,
`a|b|c`  
in this expression, the matching character could be a, b, or c. Unfortunately, our email format expression does not contain an OR operators, but keep in mind that this operator is a great example to limit our matches to a much detailed amount, such as changing our expression to match only `.com` or `.org`. 

### Character Classes
/^([a-z0-9_\`.`-]+)@([`\d`a-z\`.`-]`+`)\.(`[a-z\`.`]`{2,6})$/  <br>
In this Regex, the charactor class `/d` is used which in Javasctipt classifies the use of any digit from `0` to `9`.

### Flags

Flags are optional components placed after a regex expression to further strict a search. Our email expression does not use a flag but here are some common examples of a flag,
- `g` - A global search that tests against all possible matches in the string.
- `i` - A case-insensitive search which ignores case-sensitivity while it tests for a match.
- `m` - A multi-line search where the input string is treated as multi-lines.

These flags would be more commonly used in a document or a string containing a large pool of information, rather than an email.

### Grouping and Capturing
/^`([a-z0-9_\.-]+)`@`([\da-z\.-]+)`\.`([a-z\.]{2,6})`$/ <br>
There are 3 groups being captured in this example. The charactor class `/d` in 1st Group is the username of the email account `[A-Za-z0-9_\.-]` ~ "McNoor2022". The 2nd group captures the domain name or e-mail service being used `[\da-z\.-]` ~"@.gmail" Lastly, the 3rd group captures the domain extention (i.e .com or .net and .usabcd) `[a-z\.]{2,6}`

### Bracket Expressions
/^(`[a-z0-9_\.-]`+)@(`[\da-z\.-]`+)\.(`[a-z\.]`{2,6})$/
Similar to groups in this example, there are also 3 bracket expressions. The information in the bracket expressions is opened and closed between brackets like this `[]`. This indentifies which information is allowed to be matched.

For example 	`[Me]`+`[eE]` matches `me`, `mE`, `Me`, and `ME`.
`gr[ae]y` matches both spellings of the word `'grey'`; that is, `gray` and `grey`.

Bracket Expression first: `[A-Za-z0-9_\.-]` - includes non-case sensitive characters from a-z, numbers from 0-9 an underscore, periods and hyphens.

Bracket Expression second: `[\da-z\.-]`   - includes all digits, case sensitive characters from a-z, periods and hyphens

Bracket Expression third: `[a-z\.]`      - includes case sensitive characters from a-z and periods.

### Greedy and Lazy Match
/^(`[a-z0-9_\.-]`+)@(`[\da-z\.-]`+)\.(`[a-z\.]`{2,6})$/  <br>
Here, we have only used greedy quantifiers `+` and `{}`, meaning that it will allow the match to expand as long as it neess to go. If these quantifiers were non-greedy quantifiers, they would appear as `+?` or `{}?`, this will direct the system to make the shortest match.

### Boundaries
Boundaries is an advance regex category where the meta-character `\b` acts as an anchor just as a `^` or `$`
The meta-character `\b` simply indicates and allows a search for a whole word. For example,

`\bEmail\b` will indicate a whole word search for `Email`.

### Back-references
Back-reference match is matching the same text previously matched by a capturing group. 
By adding a `\1` at the end of the expression captures one group, and whatever is placed within the expression previously, will be repeated for a search.

For example, 

`([a-c])x\1x\1`

will capture `axaxa` or `bxbxb` or `cxcxc`.

### Look-ahead and Look-behind
Look-ahead method is defined in positive and a negative method. A positive look-ahead defines a pattern that is followed by something else and a negative look-ahead defines a pattern that is not followed by something.

Look-behind method is also defined in a positive and a negative method. Look-behind method works backwards to the look-away method, so simply a positive look-behind method defines a pattern that is behind something else and negative look-behind defines a pattern that is not behind something else.

## Author
Name: Yasmein Yang

GitHub: <a href= https://github.com/GO4YAS/yasmein-regex-tutorial target=_blank>https://github.com/GO4YAS/yasmein-regex-tutorial</a>