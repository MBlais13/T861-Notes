#bash


`chmod u+x script.sh` to fix permissions
### Script Execution
first line should start with `#!`
* `#! /bin/bash`
* `#! /bin/python`
* `#! /bin/node`
* `#! /bin/zsh` default on mac
* `#! /bin/csh`
---
### Positional Parameters
* `$0` stores the script name
* `$1-9` stores the first 8 arguments passed into the script
* `$?` stores the exit code of the last program run
* `$@` all arguments separated by space and commas
* `$*` all the arguments passed in a single word
* `$#` the number of arguments passed
* `$$` the process id of the script
---
### Brace Expansion
* `echo {1..10}` outputs `1 2 3 4 5 6 7 8 9 10`
* `echo {a..z}` outputs `a - z`
* `mkdir Output{1..3}` creates `Output1 Output2 Output3`
---
### If statement
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
### Backticks
```bash
files=`ls`
echo $files
```

---
### Input
```bash
read input -p "enter something"
echo $input
```

---
### Looping
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
### Math
usage ((`math inside`))

```bash
((100/49))
```

---
### Functions
Functions must be declared before they are run
```bash
function TryMe() {
	echo $1
	echo $2
}
Tryme Blue Green

OUTPUT= Blue Green
```

