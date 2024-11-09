---
Date (Made): 2024-04-27
tags:
  - Linux
  - Linux-Shell
Linked Docs: "[[Linux Commands]]"
sticker: lucide//recycle
---
## Using pattern with `egrep`
1. Print every line in `index.html` that contains "penpot"
```
egrep penpot index.html
```
2. How many lines in `indedx.html`that contains "penpot" or "Penpot"?
```
egrep "penpot|Penpot" index.html | wc -l

%% OR %%

egrep "(p|P)enpot" index.html | wc -l
```

## Regular Expressions of egrep
- `(c|C)(s|S)246` matches cs246, CS246, cS246 and Cs246.
- `[cC][sS]246` is equivalent; the syntax `[...]` 
	- matches any one character between the square brackets  
- `[^...]` matches any one character except one of the characters between the square brackets
- `[cC][sS] ?246` allows for an optional space before the 246; the syntax ? 
	- indicates 0 or 1 occurrences of the preceding expresssion (in this case, 0 or 1 space)  
-  `*` indicates 0 or more occurrences of the preceding expression; 
- `(cs)*246` matches 246, cs246, cscs246, cscscs246, etc.
- `+` indicates 1 or more occurrences of the preceding expression
- `.`  matches any single character; 
	- thus, the pattern `.*` matches any string at all, and 
	- the pattern `.+` matches any non-empty string
- The special patterns `^` and `$` match, respectively, the beginning and end of the line. 
	- Thus, the pattern `^cs246` matches lines that <u>begin with cs246</u>, 
	- and the pattern `^cs245$` matches lines <u>exactly equal to cs246.</u>

## Examples of Regular Expressions of egreppa
- Example: Fetch lines of even length
	`^(..)*$`
- Example2: List files in the current directory whose names contain exactly one a.
	`ls | egrep "^[^a]*a[^a]*$"`
- Example3: Fetch all words in the global dictionary that start with 'e' and consist of five characters
	`egrep "e....$" /usr/share/dict/words`
	