# Regex-Tutorial

Regular Expression, or regex or regexp in short, is extremely and amazingly powerful in searching and manipulating text strings, particularly in processing text files. One line of regex can easily replace several dozen lines of programming codes.

Regex is supported in all the scripting languages (such as Perl, Python, PHP, and JavaScript); as well as general purpose programming languages such as Java; and even word processors such as Word for searching texts. Getting started with regex may not be easy due to its geeky syntax, but it is certainly worth the investment of your time.

## Summary

We will be walking through the following regex, explaining what each component does.

^([a-z0-9_\.\+-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$

This regex makes sure that the given string matches the template for an email address.

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

var emailRegex = ^([a-z0-9_\.\+-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$

### Anchors
Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:
^ – The caret anchor matches the beginning of the text.
$ – The dollar anchor matches the end of the text.
m - The m letter flag to enable the multiline mode that instructs the ^ and $ anchors to match the beginning and end of the text as well as the beginning and end of the line.
### Quantifiers

Quantifiers are used to specify how many times a given character is expected to appear.

Our regex uses two quantifiers, + and {2,6}.

In our expression, [a-z0-9_.-]+ means that any character matching the characters inside the brackets is expected to appear at least once, with no upper limit.

The same is true of [\da-z.-]+

[a-z.]{2,6} means that 2 to 6 characters matching those inside the brackets are expected. The numbers inside the curly braces specify the lower and upper limit of the number of characters expected.


### OR Operator

[] Matches a character that is contained within the brackets.

e.g. in our section of code:

[a-z] Matches the range of lower case letters from "a" to "z".
### Character Classes

Regex has special character classes that match types of characters.

In our expression, 

\d is used to match any digit character.

The backslash is necessary in order to differentiate the digit class from a plain letter d.

Although we only have one character class in the expression, the behavior-changing function of a backslash is helpful in understanding another frequently used part of the expression, ".".

Unlike the other character classes, \d, \w (matching a word character) and \s (matching a whitespace character), the character class ".", which matches any character, does not require a backslash.

Because of the unique behavior of ".", the backslash must be used to negate its use as a character class and interpret it as the character ".".
### Flags

When writing Regex the search parameters are delimeted by two slash characters /.../ . At the end i.e. after the second slash character is where we specify theflags.

g (global) It allows for the search to continue after the first match and to continue until no more matches can be found.
i  With this flag the search is case-insensitive: no difference between A and a
m Multiline mode (covered in the chapter Multiline mode of anchors ^ $, flag "m")
s Enables “dotall” mode, that allows a dot . to match newline character \n (covered in the chapter Character classes).
u Enables full Unicode support. The flag enables correct processing of surrogate pairs. More about that in the chapter Unicode: flag "u" and class \p{...}
y “Sticky” mode: searching at the exact position in the text (covered in the chapter Sticky flag "y", searching at position)


### Grouping and Capturing

Grouping and capturing is done with ( ) in regex.

Anything within a set of parentheses is taken as a single group, which allows all the information inside to be treated as a single unit.

Look at the entire expression, paying special attention to the parentheses.

/^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/

Between /^ and $/, there are three distinct character groups, ([a-z0-9_.-]+), ([\da-z.-]+), and ([a-z.]{2,6}).

If we remove the internal logic, the regex can be expressed this way: (1)@(2).(3). This is much easier to read, and corresponds to what we know about email addresses, which always follow the (string)@(website).(com/edu/etc) template.

### Bracket Expressions

Bracket expressions can be used to match a single character or collating element.
The following lines describes how to use bracket expressions.

[abcd]	Matches any character in the square brackets.
[a-d]	Matches any character in the range of characters separated by a hyphen (-).
[^abcd] or [^a-d] Matches any character except those in the square brackets or in the range of characters separated by a hyphen (-).
[.ab.]	Matches a multi-character collating element.
[=a=]	Matches all collating elements with the same primary sort order as that element, including the element itself.

Note the following points:
The caret character (^) only has a special meaning when included as the first character after the open bracket ([). Otherwise, it is treated as a normal character.
The hyphen character (-) is treated as a normal character only under either of the following conditions:
The hyphen character is the first or last character within the square brackets, for example, [ab-] or [-xy].
The hyphen character is the only (both first and last) character; that is, [-].
To match a closing square bracket within a bracketed expression, the closing bracket must be the first character within the enclosing brackets; for example, [][xy] matches ], [, x, and y.
Other metacharacters are treated as normal characters within square brackets, and do not need to be escaped; for example, [ca$] will match c, a, or $.
### Greedy and Lazy Match

Regular expressions have 2 ways of matching

Greedy
Lazy

Greedy search — will try to match the longest possible string.
Lazy Search — will try to match the smallest possible string.

### Boundaries

The \b is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.

Characters that are matched by the short-hand character class \w are the characters that are treated as word characters by word boundaries.

Since digits are considered to be word characters, \b4\b can be used to match a 4 that is not part of a larger number. So saying \b matches before and after an alphanumeric sequence is more exact than saying “before and after a word”.

\B is the negated version of \b. \B matches at every position where \b does not. Effectively, \B matches at any position between two word characters as well as at any position between two non-word characters.

There are more boundries with the Regex Engine. Some examples include Tcl, GNU, and POSIX.
### Back-references

Backreferences match the same text as previously matched by a capturing group. Suppose you want to match a pair of opening and closing HTML tags, and the text in between. By putting the opening tag into a backreference, we can reuse the name of the tag for the closing tag.

For Example: <([A-Z][0-9]*)\b[^>]*>.*?</\1> This regex contains only one pair of parentheses, which capture the string matched by [A-Z][0-9]*. This is the opening HTML tag. The backreference \1 references the first capturing group. \1 matches the exact same text that was matched by the first capturing group. The / before it is a literal character. It is simply the forward slash in the closing HTML tag that we are trying to match.
### Look-ahead and Look-behind

(?=ABC) is a postive lookahead and it matches a group after the main expression without including it in the result.

(?!ABC) is a negitive lookahead and it specifies a group that can not match after the main expression (if it matches, the result is discarded)

(?<=ABC>) is a postive lookbehind and matches a group before the main expression without including it in the result.

(?<!ABC) is a negitive lookbehind and Specifies a group that can not match before the main expression (if it matches, the result is discarded).

Lookaheads and lookbehinds forces the main expressions to be what you have defined it as. Without it being exactly what it is it will not be accepted as a valid input.
## Author

Zehra Dastan - UOB coding student
 
My Github [github] https://github.com/ZDastan

