---
sticker: lucide//command
---
## [[Linux Files - Input,Output]]
- `^C (Control-C)` : Kills the command
- `^D (Control-D)`: Sends an end-of-file (EOF) signal such that it terminate gracefully
- `<`: `stdin` (standard input)
- `>`: `stdout` (standard output)
- `pwd`: Current Directory
- `cat` : Displays the content of a file - e.g., `cat usr/share/dict/words`

## [[Linux Pipes]]
- `head [-n lines | -c bytes] [file ...]` : print the top N number of data of the given input
- `tail [-n lines | -c bytes] [file ...]` : print the  N number of data of the given input
- `wc [-clmw] [file]`: Count the c:columns, l:lines, w:words, c:characters.
-  `uniq`: removes adjacent duplicate lines,
- `sort`: sort lines

## [[Pattern-Matching in Text Files]]
`egrep`(“extended global regular expression print”)
- `egrep pattern file` prints every line in file that contains pattern

## [[Permissions]]
- `ls -l`: gives a "long form" listing of the files in the current directory
- `chmod mode file`: Change permissions of files or directories
- `echo "${PATH}`: the shell searches these dirs, in order, for a program with that name.
