# Mastering REGEX

# Chapter 1

Full regular expressions are composed of two types of characters.
1. Special characters (like \*) are called *metacharacters*
2. The rest are called *literals*

"Literal text is the words, metacharacters are the grammar."

## Searching Text Files: Egrep
Egrep searches files and attempts to match the regular expression to each line of each file, displaying only those lines in which a match is found.
- Egrep is equivalent to "grep -E"

## Start and End of the Line
It's best to get into the habit of interpreting RE in a literal way</br>
Don't think </br>
^cat matches a line with "cat" at the beginning
but rather: </br>
^cat matches if you have the beginning of a line, followed immediately by c, followed immediately by a, followed immediately by t.

## Anchors
Caret : Matches at the beginning of the line (^cat)</br>
Dollar sign : Matches at the end of the line (cat$)</br>

The caret and dollar symbols are special in that they match a position in the line rather than any actual text characters themselves.

## Character Classes
Character Class : RE construct [...] lets you list the characters that you want to allow at that point in the match.</br>
- Example : [e] matches any e, [a] matches any a, [ea] matches either. For a word like 'gray' or 'grey', gr[ea]y would serve as a RE to match both forms of the word. Another example is sep[ea]r[ea]te for the spelling of 'separate'.

Outside of a class, literal characters have an implied 'and then' between them - match g and then r and then...

Example : \<H\[123456\]\> matches \<H1\>, \<H2\>, \<H3\>

*Character-class metacharacter '-'* indicates a range of characters like \<H\[1-6]\>. \[a-z\] and \[0-9\] are common shorthands.
- Note that dash is a special character only inside the character class, otherwise it's treated as a normal character.

### Other examples
ˆcat$ - Literally means: matches if the line has a beginning-of-line (which, of course, all lines have), followed immediately by c ⋅ a ⋅ t, and then followed immediately by the end of the line.</br>
Effectively means: a line that consists of only cat — no extra words, spaces, punctuation... just ‘cat’.</br>
ˆ\$ - Literally means: matches if the line has a beginning-of-line, followed immediately by the end of the line.</br>
Effectively means: an empty line (with nothing in it, not even spaces).</br>
ˆ - Literally means: matches if the line has a beginning-of-line.</br>
Effectively meaningless! Since every line has a beginning, every line will match — even lines that are empty!

## Negated Character Classes

