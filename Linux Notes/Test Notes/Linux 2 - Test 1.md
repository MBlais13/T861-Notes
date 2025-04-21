
> [!info] apps for vm
> ranger - file explorer
> glow - markdown files

```table-of-contents
title: **Table Of Contents:**
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

---
# apt
apt-file search
`apt-file search bin/tmux`

* `apt install`= installs package
* `apt search app`= search for specific app
* `apt info app`= provides information on a package
* `apt update app`= updating the image
* `apt upgrade`= actually installing the new update onto your system

# chown
`chown [options] [owner][:[group]] file`

| Command                      | Description                                                                   |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `chown $user $file`          | changes the user to `$user` on `$file`.                                       |
| `chown $user:$group $folder` | changes the user to `$user` and the group to `$group`.                        |
| `chown :$group $folder`      | change the group of the `folder` to `$group`.                                 |
| `chown $user: $file`         | change the user to `$user` and the group to the primary group of the `$user`. |

---
# chmod
* Broken down into 3 different groups of 3:
	* `user permissions` - based user owner
	* `group permissions` - based on group owner
	* `other permissions` - all other users
* Each 3 is broken into: 
	* `r` Read
	* `w` Write
	* `x` Execute
## Symbolic Notation Syntax

- `r`: **R**ead
- `w`: **W**rite
- `x`: e**X**ecute

| Who (Letter) | Meaning |
| ------------ | ------- |
| **u**        | user    |
| **g**        | group   |
| **o**        | others  |
| **a**        | all     |
### Using Operators
#### Adding Permissions
```
chmod g+rw example.txt
```
#### Removing Permissions
```
chmod g-rw example.txt
```
alternatively you can remove permissions by doing:
```
chmod go= example.txt
```

#### Example:
```
chmod u=rwx,g=rwx,o=rwx example.txt
```

---
## Numeric Notation Syntax

* `r` = 4
* `w` = 2
* `x` = 1

Example:
* `rw-r--r--` = 644
* `rwx------` = 700
* `rwxrw-r--` = 764
* `rwxrwxrwx `= 777
#### Examples:
```
chmod 777 example.txt
```


## file Permissions ext
### Numeric Permissions
`ls -ld $file`
### Permissions breakdown
The first 10 characters is the file type
*  `-` means a regular file
* `b` Block special
* `d` directory
* `l` symbolic link
* `s` socket
* `p` named pipe
* `c` character device file
#### Numerical Values
* `r` = 4
* `w` = 2
* `x` = 1
Example:
* `rw-r--r--` = 644
* `rwx------` = 700
* `rwxrw-r--` = 764
* `rwxrwxrwx `= 777
### sticky bits
`d---------`
`----------`
`---------t`
### umask
sets default permissions for newly created files and folders.
`umask [-S] [mask]`

### Adding permissions
#### Groups
`groupadd $username`
`gpasswd -a $username $group`


---
# file system
## linked files
symbolic link: `ln -s file1 file2`
remove symlink: `unlink <path to symlink>`
find all broken links and delete them: `find /home/mblais -xtype l -delete`
# grep
`grep "word" /filename`
`grep "Blue" colors.txt`
Params:
* `grep --color ` - If colors do not display
* `grep -r "word" *` - To search recursively in directory
* `grep -c ` - Count the amount of matches
* `grep -i ` - Ignore case sensitivity
* `grep -v ` - Display lines that don't contain word

# color syntax
`echo -e "\033[0m"` - normal
`echo -e "\033[32m this is green\033[0m back to normal"`
outputs terminal color to green and back to normal
you need to return the color back to normal.

# kill process
`kill -[signal] [options] pid`
`kill [options] processName`
`killall`

* `kill -9 1234` - send SIGKILL to process id 1234
* `kill 342` - send SIGTERM to process id 342

# scp
copy source file to remote destination:
`scp source_file user@remote_host:destination_file`
`scp colors.txt mblais@remote_host:/home/mblais`
copy directory to remote destination:
`scp -r /favcolors mblais@remote_host:/home/mblais`
copy from remote onto local host:
`scp mblais@remote_host:/path/to/source/file /path/to/local/destination/`
Params:
* -p : port
* -r : directory

# systemd commands
* `systemctl start service `- start a service
* `systemctl enable service` - enable service to start at system startup (creates a symlink * from /lib/systemd/system to /etc/systemd/system)
* `systemctl status service` - check the service status
* `systemctl restart service` - stop then start the service
* `systemctl reload service` - if supported reload the service with new configuration files
* `systemctl stop service` - stop a service  
* `systemctl disable service` - disable service at startup
* `systemctl daemon-reload `- used to reload the systemd configurations
* `journalctl` - used to display systemd logs  
* `systemctl list-unit-files --type=service` - list services
## systemd states
* poweroff.target
* rescue.target
* multiuser.target
* graphical.target
* reboot.target

# signals
| **Signal** | **Description**                                                                                       |
| ---------- | ----------------------------------------------------------------------------------------------------- |
| SIGHUP     | Hang-up detected on controlling terminal or death of controlling process.                             |
| SIGINT     | Issued if the user sends an interrupt signal (Ctrl + C).                                              |
| SIGQUIT    | Issued if the user sends a quit signal (Ctrl + D).                                                    |
| SIGFPE     | Issued if an illegal mathematical operation is attempted.                                             |
| SIGKILL    | If a process gets this signal, it must quit immediately and will not perform any clean-up operations. |
| SIGTERM    | Software termination signal (sent kill by default).                                                   |
| SIGALRM    | Alarm clock signal (used for timers).                                                                 |

# users & groups
* `useradd user`
* `usermod -aG group user
* `groupadd group`
* `passwd user` - change password
## usermod
* `useradd user`
* `usermod -aG group user
* `usermod -d homedir user` - change user home directory
* `usermod -d homedir -m user` - move user home directory
* `usermod -s shell user` - change user default shell
* `usermod -u UID user` - change user ID
* `usermod -l newuser user` - change username
* `sudo usermod -e date user` - set user expiry date
* `sudo chage -l user` - view user details
* `usermod -L user` - lock user account
* `usermod -U user` - unlock user account

---
# vim keybinds

* `h`  - Move left
* `j`  - Move down
* `k`  - Move up
* `l`  - Move right
* `gg` - Move to top
* `G`  - Move to bottom 
* `w`  - Move to start of next word
* `e`  - Move to end of next word
* `b`  - Move backwards to start of word
* `ge` - Move backwards to end of word
* `0`  - Jump to beginning of current line
* `^`  - Jump to first non-blank character
* `5gg` - Go to line 5
* `i`  - Insert before cursor
* `I`  - Insert at beginning of line
* `a`  - Insert after cursor
* `A`  - Insert at end of line
* `o`  - Insert in new line below cursor
* `O`  - Insert in new line above cursor
* `yy` - Yank line
* `2yy` - Yank 2 lines
* `p`  - Paste after cursor
* `P`  - Paste before cursor
* `:q` - Quit program without saving
* `:wq` - Save and quit program
* `:w` - Save program
* `escape` - Exit insert mode
* `x`  - Delete character at cursor
* `dw` - Delete word
* `d$/D` - Delete to end of liine
* `$`  - Go to end of text on line
* `2w` - Go two words forward
* `3e` - Go to end of third word ahead
* `d2w` - Delete 2 words
* `dd` - Delete line
* `2dd` - Delete two lines
* `u`  - Undo last changes
* `U`  - Undo changes on entire line
* `ctrl+r` - Redo changes
* `r`  - Replace character under cursor
* `cw` - Change word
* `c$/C` - Change to end of line
* `c2w` - Change 2 words
* `50G` - Go to line 50
* `G`  - Go to last line in file
* `gg` - Go to first line
* `/waldo` - Search for waldo
* `n`  - Go to next search result
* `N`  - Go to previous search result
* `?waldo` - Search backwords for waldo
* `ctrl+o` - Jump to previous location
* `ctrl+i` - Jump to next location
* `%`  - Go to matching parentheses or brackets
* `:%s/bad/good `- Replace bad with good in current line
* `:%s/hi/bye/g` - Replace hi with bye in entire file
* `:%s/x/y/gc` - replace x with y in entire file, prompt for changes
* `:!ls `- Run shell command ls
* `v` - Open visual mode
* `vw` - Visual select word
* `vwd` - Visual select word, then delete word
* `:w play.rb` - Save file as play.rb
* `:r hat.rb` - Read in file hat.rb
* `R` - Enter replace mode
* `yw` - Yank word
* `vwy` - Visual select word then yank
* `y$` - Yank to end of line
* `set ic` - Change search to ignore case
* `set noic` - Change search to use case
* `:e sun.rb` - Open file sun.rb
* `:help w` - Get help for w command


---
# Basic Regex Syntax
- `[]` creates a list of characters
	- `[A-Z]`
	- `[A-Za-Z` - any letterx
	- `[0-9a-z]`
	- `^` negates the list such as `[^A-Z]` is anything but A-Z (including new line)
- `\d` - represents a digit
- `\D` - a non digit
- `\w` - word character `[A-Za-z0-9_]`
- `\W` - non word character
- `\s` - white space (not new line)
- `^` - beginning of line
- `$` - end of line
#### Multiplicity
- `? = 0 or 1 of the desired character`

- `{n,m}` - *n* to *m* times
	- `{1,3}` - 1 to 3 times
- `{n}` - exactly n times
- {n, } - *n* to infinite times
	- `{3, }` - at least 3 times
#### Replace variables
- `(.*)` - will remember everything in the brackets
- `\1` - will pull data from the first set of brackets

#### Character Case
- Uppercase - `\u [[:upper:]]`
- Lowercase - `\l[[:lower:]]`

#### Quirks with vim & sed
- SED
	- does not have `\d`, instead list or use `'` `[[:digit:]]`
	- you have to escape brackets, instead of `(` its `\(`
	- you have to escape braces, instead of `{4}` its `\{4\}`
- VIM
	- you have to escape brackets, instead of `(` its `\(`
	- you have to escape only the first brace: `{4}` its `\{4}`

---
# Basic Awk Usage
- Sometimes you'll want to manipulate data and report on it, awk is a very powerful tool to allow you to perform data manipulation
- You can use awk when piping, therefore if you combine it with a tail feed to do live data manipulation

``` bash
awk '/systemd/ {print “\033[41m”$0”\033[0m”; next}
		// {print $0}
'
```
#### AWK Variables
- $0 - the whole line
- $1 - the first element space separated
- $2 - the second element space separated
- $3 - ...third...etc
- NR - current record count usually lines
- NF - current field count usually divided by spaces
- FS - field separator, default space
- RS - record separator, default new line
- OFS - output field separator, default space
- ORS - output field separator, default new line
##### `BEGIN` & `END`
- `BEGIN` to run commands before parsing the file
- `END` to run commands after parsing the file
##### substring
- `substr(var,start,number)` creates a substring from a variable
	- var is the variable
	- start is the start index (from 0)
	- number is optional, the number of characters to extract


---
# MariaDB
## Installing and config
```sql
apt install mariadb-client, mariadb-server
```

```sql
mysql_secure_installation
```

```sql
mysql -u bob -p"drowssap"
```
`-p` then your password cannot have a space between

```sql
mysql -u bob -p"drowssap" --host=php.scweb.ca --port=3306
```

## Creating Users
```sql
CREATE USER 'student'@localhost IDENTIFIED BY 'password';
--
/* Allow users from any host */
CREATE USER 'student'@'%' IDENTIFIED BY 'password';

/* Allow users from any host that ends with scweb.ca */
CREATE USER 'student'@'%.scweb.ca' IDENTIFIED BY 'password';

/* Allow users from any IP that starts with 192.168 */
CREATE USER 'student'@'192.168.%.%' IDENTIFIED BY 'password';
```

### View Users
```sql
SELECT user,host,password FROM mysql.user;
```

## Privileges
```sql
/* Grant all privileges to student for the database mit416 and its tables */
GRANT ALL PRIVILEGES ON mit416.* to student@localhost

/* Grant read privileges to student on exampledb */
GRANT SELECT ON exampledb.* to student@localhost
```

### View Privileges
```sql
SHOW GRANTS FOR fiacobacci@localhost
```

### Remove Privileges
Remove privileges `REVOKE`
```sql
REVOKE ALL ON exampledb.* FROM student@localhost;
REVOKE SELECT ON proddb.* FROM student@localhost;
```


## Tables
### Create Tables
```sql
CREATE TABLE employee(
id INT NOT NULL AUTO_INCREMENT,
firstname VARCHAR(20),
lastname VARCHAR(20),
department VARCHAR(20),
PRIMARY KEY (id)
);
```

### Remove Tables
```sql
DROP TABLE employee;
```

### Inserting/Updating/Deleting Records
You can create records using `INSERT INTO`
Modify them with `UPDATE`
Remove them with `DELETE FROM`
```sql
/* Create a record */
INSERT INTO employee VALUES (DEFAULT,"Franco", "Iacobacci", "Networking");

/* Modify the record */
UPDATE employee SET department="IT" WHERE id=1;

/* Delete the record */
DELETE FROM employee WHERE id=1;
```

### Viewing Records
To View data you can use `SELECT`
```sql
/* Select all records from employee */
SELECT * FROM employee

/* Select all records with the first name Bob */
SELECT * FROM employee WHERE firstname='Bob'

/* Select all records and order by the ID */
SELECT * FROM employee ORDER BY id
```


## Export database
```sql
mysqldump -u username -p"password" database_name > File.sql
```

## Resetting the root password
1. Stop the mysqld service
2. Run `mysqld_safe --skip-grant-tables &`
3. Login to mysql shell using `mysql`
4. Update forgotten password using (see code below)
5. Restart service

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
FLUSH PRIVILEGES;
```

---
# Bash Scripting

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

---
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
#-- output final result into .txt file
done < input.txt
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
## Bash input redirection from variables
* Sometimes you want to redirect standard input from a variable, to do that use <<<

```bash
value="welcome"
cat <<< $value
```

The output of cat will be welcome

---
## Brace String Manipulation

- `${string:start:length}` - get a substring
- `echo ${string:5}` - Gets the first 
- `echo ${string:5:5}`
- `echo ${string:0:-3}`
- `var//match//replace`

```bash
string="why has it been sooooo COLD!"
echo ${string:5}
echo ${string:5:5}
echo ${string:0:-3}
```

---
## Bash Array

* ${var:start:length} – get a substring  
* ${var/match/replace} – replace the first occurrence of match with replace
* ${var//match/replace} – replace all instances of match with replace

* Recall arrays are lists of values  
* To declare and array from a list use:
     * `declare -a arrayName=(item1 item2 item3)`
     * `arrayName=(item1 item2 item3)`
     * `arrayName[0]=item1`
     * `arrayName[1]=item2`
### Create Array
```
array = (one two three)
```

### Arrays continued
* To access elements of an array you can use the following syntax
	* `${arrayName[0]} `= first element
	* `${arrayName[1]}` = second elements
	
* To access all elements we can use:
	* `${arrayName[@]}` = array expansion into list
	* Note in this case if this is quoted "`${arrayName[@]}`" then each array element will be quoted when creating a list

```bash
"${array[@]}" # “One Item” “Two Item” - 2 Items (Usually the desired result)
${array[@]} # One Item Two Item – 4 Items
```