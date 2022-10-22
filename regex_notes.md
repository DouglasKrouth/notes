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

Example : \<H[123456]\> matches \<H1\>, \<H2\>, \<H3 \>

*Character-class metacharacter '-'* indicates a range of characters like \<H[1-6]>. [a-z] and [0-9] are common shorthands.
- Note that dash is a special character only inside the character class, otherwise it's treated as a normal character.

## Other examples
ˆcat$ - Literally means: matches if the line has a beginning-of-line (which, of course, all lines have), followed immediately by c ⋅ a ⋅ t, and then followed immediately by the end of the line.</br>
Effectively means: a line that consists of only cat — no extra words, spaces, punctuation... just ‘cat’.</br>
ˆ\$ - Literally means: matches if the line has a beginning-of-line, followed immediately by the end of the line.</br>
Effectively means: an empty line (with nothing in it, not even spaces).</br>
ˆ - Literally means: matches if the line has a beginning-of-line.</br>
Effectively meaningless! Since every line has a beginning, every line will match — even lines that are empty!

## Negated Character Classes
Using [^] instead of [...], the class matches any character that isn't listed. For example [1-6] matches a character that's not 1 through 6. The leading ^ negates the list.

Example : Words that have *q* followed by something other than *u* --> q[^u] which would generate matches like Iraqi, Iraqian, migra, qasida

## Matching any character with Dot
The metacharacter "." dot is shorthand for a class that matches any character. It can be convenient when you need an "any character here" placeholder.
- Example : I want to match dates for 03/19/2022, 03-19-2022 and 03.19.2022 --> These all can be matched with dot like 03.19.2022
- Caveat : Dot can match any character at all (or set of characters) so it would math 290319 2022 as well

## Alternation
### Matching any one of several subexpressions
A very convenient metacharacter is "|" which means "or". It allows combo of multiple expressions into a single expression that matches any of the individual ones.
- Example : Bob and Robert are distinct names --> Bob|Robert matches either instance in a single expression. 

Looking back at the earlier gr[ae]y example, we can write this as grey|gray and even gr(a|e)y. With gr(a|e)y, the parentheses are required because without them, gra|ey means "gra" or "ey" which is not what we want.

IMPORTANT NOTE : Alternation is not the same thing as a character class. A character class can match just a single character in the target text. With alternation, since each alternative can be a full-fledged regular expression in and of itself, each alternative can match an arbitrary amount of text.

Example <pre>
\^(From|Subject|Date):
</pre>
The alternation is constrained by the parentheses, so literally, the regex means "match the start of the line, then one of "From", "Subject", "Date, and then match ":" as below
1. start-of-line, followed by F r o m, followed by ":" -OR-
2. start-of-line, followed by S u b j e c t, followed by ":" -OR-
3. start-of-line, followed by D a t e, followed by ":"

## Ignoring Differences in Capitalization
*Case-insensitive* matches : Replace a string like "From" with any permutation of [Ff][Rr][Oo][Mm] to match any form of the word. This is cumbersome. Instead we use the */i* flag which can vary depending on the environment where RE is being used. For example, *egrep -i* enables the command in terminal egrep.

