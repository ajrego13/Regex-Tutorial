# Validating Email Addresses

A regex, (or regular expression), is a set of characters that defines a search pattern. A regex can be used within code and/or an algorithm to find (or find and replace) specific character patterns within a string. For example, one can identify phone numbers, email addresses, URLs, etc by using a regex. A regex can also be used to validate user input. 

## Summary

This tutorial will examine each character in the following regex in order to explain its overall function:

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

This regex matches an email. It can therefore be used to find email addresses within a string of text, verify that a user has entered a valid email address, etc. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
The `^` and `$` in the regex are Anchors, as seen in the beginning and end of the expression:

/<b>^</b>([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})<b>$</b>/<br>

The `^` beginning anchor is used to match any string that begins with the character(s) following it in the expression. For example, `^Hello` would match any string that begins with the word "Hello." 

The `$` ending anchor is used to match any string that ends with the character(s) proceeding it in the expression. For example, `Goodbye$` would match any string that ends with the word "Goodbye."

When a regex contains both beginning `^` and ending `$` anchors, a search using the regex will return an exact string match of the characters included between the anchors. For example, `^Hello and Goodbye$` will return any strings that include the exact words "Hello and Goodbye."

In our regex above, the beginning `^` and ending `$` anchors indicate that the search must match characters defined by the piece of the expression located between the anchors: `([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})` We will explain each of these components in their respective sections below. 
### Quantifiers
The curly brackets `{}` in the regex indicate quantifiers, as shown by `{2,6}` towards the end of the expression: <br>

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]<b>{2,6}</b>)$/ <br>

Quantifiers indicate <i>how many</i> of the proceeding character(s) must exist to return a match. For example, the expression `a{1,5}` would match all strings in which "a" occurs between 1 and 5 times. Similarly, `(ab){1,5}` would match all strings in which (ab) occurs between 1 and 5 times.

In our regex above, we can see that any characters represented by `([a-z\.]` must occur between 2 and 6 times return a match. We will define these components later in the tutorial, but in the meantime it is important to note that this quantifier indicates that the characters after the `.` are letters between 2 and 6 characters in length. When using this regex to search for email addresses, this part of the expression would indeed match standard email domains such as ".com" and "net." 
### Grouping Constructs
Parentheses `()` are used in regular expressions to group together pieces of the search. In our regex, our expression is grouped into 3 sections: <br>

/^<b>(</b>[a-z0-9_\.-]+<b>)</b>@<b>(</b>[\da-z\.-]+<b>)</b>\.<b>(</b>[a-z\.]{2,6}<b>)</b>$/ <br>

As defined in previous sections above, the first group `([a-z0-9_\.-]+)` consists of the characters before the @ sign in an email address (coder123, firstname.lastname, etc). The second group `([\da-z\.-]+)` consists of the characters just after the @ sign in an email address (gmail, hotmail, etc). The third group `([a-z\.]{2,6})` consists of the domain after the dot `.` at the end of the email address (com, net, co.jp, etc). 
### Bracket Expressions
Anything with `[]` around it is considered a bracket expression. In this regex there is three.
1. `/^([a-z0-9_\.-]+)` this is to find any lowercase letter from a-z and any number from 0-9
2. `([\da-z\.-]+)\` this is to find any lowercase letter from a-z and the /d puts a number to each of those letters
3. `([a-z\.]{2,6})$/` this is to find any lowercase letter from a-z and also is looking for a period(.)
### Character Classes
Character Classes are identified with a backslash `\` and can be found proceeding `.` and `d` characters in our regex: <br>

/^([a-z0-9_<b>\.</b>-]+)@([<b>\d</b>a-z<b>\.</b>-]+)\.([a-z<b>\.</b>]{2,6})$/ <br>
 
Including the backslash before a dot `\.` indicates that we are literally searching for a dot. In our regex above, we want to ensure our search matches email addresses that may include a dot before the @ sign (<i>firstname.lastname</i>@gmail.com) and as part of the domain (.com, '.net, .co.jp). <i>Note: in regular expressions, a dot by itself indicates that we are searching for any character.</i>

The `\d` Character Class matches a single character that is a digit from 0-9. In our regex above, `[\da-z\.-]` indicates that we are looking for a digit, or a letter from a-z, or a dot `.` or a dash `-`. As described above in the [OR Operator](#or-operator) section, this piece refers to the portion of the email address after the @ sign (gmail, hotmail, etc). 
### The OR Operator
The square brackets `[]` in the regex are called OR operators (or "Bracket Expressions") and are found 3 times throughout the expression: <br>

/^(<b>[</b>a-z0-9_\.-<b>]</b>+)@(<b>[</b>\da-z\.-<b>]</b>+)\.(<b>[a-z\.]</b>{2,6})$/ <br>

These brackets `[]` indicate that the search may match any of the items included in the character set listed between the brackets. For example [abc] would match a string that includes a, b, <i>or</i> c. <br>

Looking at the first OR Operator in our regex above `[a-z0-9_\.-]`, any letter from a-z, <i>or</i> any integer from 0-9, <i>or</i> a dot `.`<i>or</i> a dash `-` in this location would return a match. This refers to the beginning of the email address before the @ sign. For example, the characters "coder123" in the email address "coder123@gmail.com" would return a match as they are comprised of letters from a-z and integers from 0-9. <br>

The second OR Operator in the regex `[\da-z\.-]`  indicates that any digit `\d`, <i>or</i> any letter from a-z, <i>or</i> a dot `.`, <i>or</i> a dash `-` in this location would return a match. This refers to the portion of the email address after the @ sign. For example, the characters "gmail" in the email address "coder123@gmail.com" would return a match as they are comprised of letters from a-z.<br>

The final OR Operator in the regex `[a-z\.]` indicates that any letter from a-z <i>or</i> a dot `.` in this location would return a match. As mentioned in the [Quantifiers](#quantifiers) section above, this refers to the domain at the end of the email address. For example, the characters "com" in the email address "coder123@gmail.com" would return a match as they are comprised of letters from a-z. International or similar domains including an extra dot `.` such as ".co.jp" would also return a match, as a dot `.` is included within the OR Operator.
### Flags
Flags are the forward slashes `//` that begin and end the regex: <br>

<b>/</b>^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$<b>/</b> <br>

Regular expressions, including our regex above, are generally contained within slashes `//` that simply delimit the search pattern. Some expressions have specific flags that modify the search parameters, such as making the seach case-insensitive, but our regex just includes standard flags. 
### Character Escapes
The backslash \ is used before { in order for the regx to know to search for the information inside the brackets and not the start of the quantifier itself. But once it is inside a bracket it no longer is used for that purpose. As you can see in the email validation the backslash is inside of brackets /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/.
## Author
<a href="https://github.com/ajrego13" target="_blank">Github Profile</a>
