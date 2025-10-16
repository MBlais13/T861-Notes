#bash


`chmod u+x script.sh` to fix permissions
## Script Execution
first line should start with `#!`
* `#! /bin/bash` - what we use
* `#! /bin/python`
* `#! /bin/node`
* `#! /bin/zsh` - default on mac
* `#! /bin/csh`
---
## Positional Parameters
* `$0` stores the script name
* `$1-9` stores the first 8 arguments passed into the script
* `$?` stores the exit code of the last program run
* `$@` all arguments separated by space and commas
* `$*` all the arguments passed in a single word
* `$#` the number of arguments passed
* `$$` the process id of the script
---
## Brace Expansion
Basic Usage
* `echo {1..10}` outputs `1 2 3 4 5 6 7 8 9 10`
* `echo {a..z}` outputs `a - z`
* `mkdir Folder{1..3}` creates `Folder1 Folder2 Folder3`
counting by 'amount'
- `echo {1..50..10}` outputs `10 20 30 40 50`

## Common Metacharacters
Here’s a breakdown of common metacharacters and their functions:
- **`^`** (caret): Matches the start of a string.
- **`$`** (dollar): Matches the end of a string.
- **`.`** (dot): Matches any single character except a newline character.
- **`[]`** (square brackets): Defines a character class, matching any one character within the brackets.
- **`{}`** (curly brackets): Specifies a specific quantity of characters to match.
- **`-`** (hyphen): Specifies a range of characters when used within square brackets.
- **`?`** (question mark): Makes the preceding character optional, matching zero or one occurrence.
- **`*`** (asterisk): Matches zero or more occurrences of the preceding character.
- **`+`** (plus): Matches one or more occurrences of the preceding character.
- **`()`** (parentheses): Groups expressions together.
- **`|`** (pipe): Indicates an OR condition between two expressions.
- **`\`** (backslash): Escapes a metacharacters, allowing it to be matched as a literal character.
---
## If statements
```bash
if ping -c 1 google.ca >> /dev/nul 2>> /dev/null; then
	echo "google down"
elsif ping -c 1 microsoft.ca >> /dev/nul 2>> /dev/null; then
	echo "microsoft is crazy"
else
	echo "the world is ending"
fi
```
---
## Backticks
```bash
files=`ls`
echo $files
```

---
## Input
```bash
read input -p "enter something"
echo $input
```

---
## Looping
Different types of loops
* `for in`
* `while`
* `for`

```bash
for homedir in $(ls /home); do
	echo $homedir
done
```
while
```bash
while read line; do
	echo $line
done
```

---
## Math
usage ((`math inside`))

```bash
((100/49))
```

---
## Functions
Functions must be declared before they are run
```bash
function TryMe() {
	echo $1
	echo $2
}
Tryme Blue Green

OUTPUT= Blue Green
```

## IFS
(Input Field Separator) by default, space, tab, new line. The IFS can be changed to allow for parsing special types of files.

| column 1 | separator | column 2 |
| -------- | --------- | -------- |
| name     | ,         | userid   |
```bash
IFS=","; while read name userid; do
	echo $name - $userid
done < "$1"
```

---

