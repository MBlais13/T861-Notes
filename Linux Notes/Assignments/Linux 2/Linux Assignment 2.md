
## Task 1
```
(\d{2})-(\d{2})-(\d{4}),([^,]+),([^,]+),([^,]+),(\d{10}),(\d+)
```

```
insert into users values ('\3-\1-\2','\4 \5','\6','\7x\8');
```
rearranges data into an SQL insert statement with proper formatting.
changes date format to `yyyy-mm-dd`
## Task 2
```
sed 's/\(.*\)|\(.*\)/\L\1\2/' names.txt
```
changes names separated by `|` into a lowercase first letter username.

## Task 3

```bash
#!/bin/bash

ls -l | awk '{

if ($1 == "total") {
print $0;
next;
} 

green="\033[0;32m"
red="\033[0;34m"
blue="\033[0;31m"
reset="\033[0m"

UserPerm=substr($1, 2, 3)
GroupPerm=substr($1, 5, 3)
OtherPerm=substr($1, 8, 3)

printf "%s%s%s%s %s %s %s %s %s %s %s %s %s %s\n",

(substr($1, 1, 1)),
green UserPerm reset,
blue GroupPerm reset,
red OtherPerm reset,
$2,
$3,
}
```
awk is taking the command and grabbing each column, we are specifying which columns to change.

For the file permissions column:
- user = green.
- group = blue.
- others = red.