#regex #awk

# Basic Regex Syntax

- `[]` creates a list of characters
	- `[A-Z]`
	- `[A-Za-Z` - any letter
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

#### Quirks with vim & sed
- SED
	- does not have `\d`, instead list or use `'` `[[:digit:]]`
	- you have to escape brackets, instead of `(` its `\(`
	- you have to escape braces, instead of `{4}` its `\{4\}`
- VIM
	- you have to escape brackets, instead of `(` its `\(`
	- you have to escape only the first brace: `{4}` its `\{4}`
### Regex in linux


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

