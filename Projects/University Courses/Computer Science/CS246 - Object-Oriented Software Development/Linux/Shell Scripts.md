---
Date (Made): 2024-05-12
tags:
  - Linux
  - Linux-Shell
Linked Docs:
  - "[[Linux Commands]]"
  - "[[Linux Files - Input,Output]]"
  - "[[Linux Pipes]]"
  - "[[Pattern-Matching in Text Files]]"
  - "[[Permissions]]"
sticker: lucide//file-code
---
## What is Shell Scripts?
- Files containing sequences of [[Linux Commands]], excuted as programs
- `#!/bin/bash`: Shebang line
	- Indicates that the file should be executed as a bash script
- Example:
```bash
#!/bin/bash
date
whoami
pwd

chmod u+x myscript
./myscript
```

## Shell Script Variables
```bash
x=1 
xy=2
%% No Spaces! %%

echo $x
1

echo ${x}y
1y

echo $xy
2
```
- $ = "Fetch the value of"
	- Use $ when fetching the value of a variable
	- No $ when setting a variable
- Differences of using brackets
	- Using braces (`{}`) is particularly useful when you need to concatenate a variable with other text without introducing ambiguity about where the variable name ends.
- All vars contain <i>strings</i>, 
	- e.g., `x` above contains the string "1"

## Shell Global Variables
- Some "global" variables available
```bash
dir=~/cs246

echo ${dir}
/u/bmlushma/cs246

ls ${dir}
(contents of /u/bmlushma/cs246)
```
- `PATH`: Shows the list of directories
- As we learned in [[Linux Commands#Linux Pipes]] and [[Linux Pipes#Using output as an argument]]:
	- Double Quotes `""` - $ expansion happens
	- Single Quotes `''` - no $ expansion
```bash
echo "${PATH}"
(shows the path)

echo '${PATH}'
${PATH}
```

## Examples of Shell Script

### Arguments
- Example1: Check whether a word is in the dictionary.
	- e.g. ./isItAWord hello
```bash
#!/bin/bash
egrep "^$1$" /usr/share/dict/words

%% Prints nothing if word not found. %%
%% Prints the word if found. %%

%% $1 indicates the first argument(text) here %%
```

### If - else
- Example2: A good password should not be in the dictionary. Answer whether a word is a good password.
```bash
#!/bin/bash
egrep "^$1$" /usr/share/dict/words > /dev/null 

# Note: redirecting stdout to /dev/null suppresses output 
# Note: every program returns a status code when finished 

# egrep-- returns 0 if found, 1 if not found 

# (in Unix: 0 = success, non-zero = failure) $? = status of most recently-executed command

if [ $?-eq 0 ]; then
	echo Bad password 
else 
	echo Maybe a good password 
fi
```

- Example3: Verify correct number of args; print error msg if wrong.
```bash
#!/bin/bash 
usage() { # Good idea to make usage a function, so it can be used multiple times 
	echo "Usage: $0 password" 
} 

if [ $#-ne 1 ]; then
	usage
	exit 1
fi 
egrep "^$1$" /usr/share/dict/words > /dev/null 
(etc.)
```

### Loops
- Example4: Loops: print numbers from 1 to $1
```bash
#!/bin/bash
x=1 

while [ $x-le $1 ]; do 
	echo $x
	x=$((x + 1)) # $((...)) syntax for doing arithmetic 
done
```

- Example5: Looping over a list:
```bash
for x in a b c; do 
	echo $x; 
done 
# could demo this right on the command-line 
# to quickly show what for does 

prints a b c
```

- Example6: rename all .cpp files to .cc
```bash
#!/bin/bash
for name in *.cpp; do # the glob *.cpp is replaced inline with all matching files 
	mv ${name} ${name%cpp}cc 
done
```
- The `for ... in ...`syntax sets the variable to each word in the given list. 
- The syntax `${name%cpp}` produces the value of name, without the trailing cpp.

- Example7: Payday is on the last Friday of the month. Compute this month’s payday (2 tasks: compute the date; present the answer)
```bash
#!/bin/bash
report() { # Inside a function, $1, etc. denote the *function’s* params 
	if [ $1-eq 31 ]; then 
	echo "This month: the 31st" 
	# be ready for students who point out that else 
	# rd and nd are possible in February 
	echo "This month: the ${1}th" 
	fi 
} 

# Compute the date; pass as argument 1 to answer 
report $(cal | awk ’{print $6}’ | egrep "[0-9]" | tail-1)

```

- example8: Generalize this script to any month.
	- `cal May 2016` gives the calendar for May 2016. 
	So let `./payday May 2016` give May 2016’s payday
```bash
report $(cal $1 $2 | awk ’{print $6}’ | egrep "[0-9]" | tail-1) $1
```
- If arguments are not supplied to payday, then `$1` and `$2` are blank, 
	- and this pipeline reverts to its previous behaviour. 
	- We pass an extra parameter `$1` (the month) to report so that it can report the month:
```bash
report() {
	if [ $2 ]; then 
	# $2 (2nd argument) is the month, if supplied 
		echo-n $2 
	#-n suppresses the trailing newline 
	else 
		echo-n "This month" 
	fi 
	
	if [ $1-eq 31 ]; then 
		echo ": the 31st" 
	else 
		echo ": the ${1}th" 
	fi 
}
```
- Note that argument `$2` in report is equal to argument `$1` in the main script, as `$1` was passed as the second argument to report.