# Matching a URL with a Regular Expression (Regex)

The following gist will provide a description and explanations of the URL Matching Regex.

## Summary

This regex uses a sequence of characters to define a specific search pattern. With this regex, we will be able to match any valid URL. 
````
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```` 
This regex asks and answers a simple-yet-necesarry question; 

-*Is the input a valid URL?*

This regex can have a wide variety of applications, the most primary usage being the validation of input data.

## Table of Contents

- [Anchors](#anchors)
- [Grouping Constructs](#grouping-constructs)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Bracket Expressions](#bracket-expressions)
- [Character Escapes](#character-escapes)
- [Author](#author)
## Regex Components

### Anchors
The two anchors in this regex are the `^` at the beginning and the `$` at the end. These constitute an exact string match with the components between the two anchors. When used alone, the `^` anchor matches any string that *begins* with the characters that follow the anchor. The `$` matches any string that *ends* with the characters that precede it. By enclosing the regex between these two anchors, the search function will match exactly what is included between them (what it begins AND ends with). 

###Grouping Contructs
Examining the expression, we can see that there are a number of components separated by parentheses `()`. Parentheses are used in regex to create separate groups of interest. Within each of these groups, there is another regex that we may look at separately to see what is evaluated:
- the initial `https` component: `(https?:\/\/)`
- the domain name (e.g. `www.google`, or `pets`): `([\da-z\.-]+)\.`
- the top level domain (`.com`, `.gov`, etc): `([a-z\.]{2,6})`
- the file path: `([\/\w \.-]*)*`

### Quantifiers 
A few of the components of *capture groups* end with a `?` or a `*`. These are the **quantifiers**. Quantifiers are used to define the number of times a given expression may be identified. The `?` makes a single instance of the character preceding the quantifier optional, while the `*` makes multiple instances of the characters preceding the quantifier optional. 
For example; 
```
(https?:\/\/)?
```
contains two `?` quantifiers. This expression is looking for `http://` OR `https://`. For this reason a *single* internal `s` is optional. The same is true for the entire expression in the parenthesis, and is therefor followed by a `?`. In other words, a valid URL may begin with `http://` OR `https://`, or it may not begin with either of them (the input begins with `www.`). The same applies for the `/` at the end of the expression. 

Likewise, the `*` makes the expression optional, but in this case it may be *one or more* instances that are optional. So if we look at the last group:
```
([\/\w \.-]*)*
```
The expression is allowing any number of filepath characters that may follow the initial specified domain.

Finally, the `{}` quantifier sets a range of instances where a match may be identified. In evaluating the Top level domain, the regular expression allows for the top level domain to consist of 2 to 6 characters.


### Character Classes
The main character classes used in the above expression include the `\d` character class which will look for numerical digits, and the `\w` character class will look for ASCII characters `[A-Za-z0-9_]`. 

### The OR Operator 
The main OR operator used in the above regex is the `[]`. Which is better explained with it's tandem use in the following bracket expressions section.

### Bracket Expressions
The expression will match for any characters or character classes included in the brackets. For example the `[\da-z\.-]` expression matches numerical digits (`\d`) OR alphabetical characters between a and z (`a-z`) OR any '.' (`\.`) OR any '-' (`-`). 

### Character Escapes
If you need to escape a character in a string literal, you will need to use the dollar sign ($) instead of percent (%). An example would be; <br>
use query=title%20EQ%20"$3CThe title$3E" instead of query=title%20EQ%20'%3CThe title%3E'.

## Author

This regex tutorial was researched and compiled by James VonLienen. My Github: [UnbindingNote](https://github.com/UnbindingNote)
