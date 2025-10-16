#regex #awk

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







# Syntax

| What                                                | [Perl](http://perldoc.perl.org/perlre.html)/PCRE | [Python's `re`](https://docs.python.org/library/re.html) | POSIX (BRE)                          | POSIX extended (ERE)                 | Vim                                    |     |                         |
| --------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------- | ------------------------------------ | ------------------------------------ | -------------------------------------- | --- | ----------------------- |
| Basics                                              |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Custom character class                              | `[...]`                                          | `[...]`                                                  | `[...]`                              | `[...]`                              | `[...]`                                |     |                         |
| Negated custom character class                      | `[^...]`                                         | `[^...]`                                                 | `[^...]`                             | `[^...]`                             | `[^...]`                               |     |                         |
| \ special in class?                                 | yes                                              | yes                                                      | no, `]` escaped if comes first       | no, `]` escaped if comes first       | yes                                    |     |                         |
| Ranges                                              | `[a-z]`, `-` escaped if first or last            | `[a-z]`, `-`escaped if first or last                     | `[a-z]`, `-`escaped if first or last | `[a-z]`, `-`escaped if first or last | `[a-z]`, `-`escaped if first or last   |     |                         |
| Alternation                                         | `\|`                                             | `\|`                                                     | `\\                                  | `                                    | `\|`                                   | `\\ | ` `\&` (low precedence) |
| Escaped character                                   | `\033` `\x1B``\x{1234}` `\N{name}``\N{U+263D}`   | `\x12`                                                   |                                      |                                      | `\%d123` `\%x2A``\%u1234``\%U1234ABCD` |     |                         |
| Character classes                                   |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Any character (except newline)                      | `.`                                              | `.`                                                      | `.`                                  | `.`                                  | `.`                                    |     |                         |
| Any character (including newline)                   |                                                  |                                                          |                                      |                                      | `\_.`                                  |     |                         |
| Match a "word" character (alphanumeric plus `_`)    | `\w` `[[:word:]]`                                | `\w`                                                     | `\w`                                 | `\w`                                 | `\w`                                   |     |                         |
| Case                                                | `[[:upper:]]` / `[[:lower:]]`                    |                                                          | `[[:upper:]]`/ `[[:lower:]]`         | `[[:upper:]]`/ `[[:lower:]]`         | `\u` `[[:upper:]]`/ `\l``[[:lower:]]`  |     |                         |
| Match a non-"word" character                        | `\W`                                             | `\W`                                                     |                                      |                                      | `\W`                                   |     |                         |
| Match a whitespace character (except newline)       |                                                  |                                                          | `\s``[[:space:]]`                    | `\s``[[:space:]]`                    | `\s` `[[:space:]]`                     |     |                         |
| Whitespace including newline                        | `\s` `[[:space:]]`                               | `\s`                                                     |                                      |                                      | `\_s`                                  |     |                         |
| Match a non-whitespace character                    | `\S`                                             | `\S`                                                     | `[^[:space:]]`                       | `[^[:space:]]`                       | `\S``[^[:space:]]`                     |     |                         |
| Match a digit character                             | `\d` `[[:digit:]]`                               | `\d`                                                     | `[[:digit:]]`                        | `[[:digit:]]`                        | `\d` `[[:digit:]]`                     |     |                         |
| Match a non-digit character                         | `\D`                                             | `\D`                                                     | `[^[:digit:]]`                       | `[^[:digit:]]`                       | `\D``[^[:digit:]]`                     |     |                         |
| Any hexadecimal digit                               | `[[:xdigit:]]`                                   |                                                          | `[[:xdigit:]]`                       | `[[:xdigit:]]`                       | `\x``[[:xdigit:]]`                     |     |                         |
| Any octal digit                                     |                                                  |                                                          |                                      |                                      | `\o`                                   |     |                         |
| Any graphical character excluding "word" characters | `[[:punct:]]`                                    |                                                          | `[[:punct:]]`                        | `[[:punct:]]`                        | `[[:punct:]]`                          |     |                         |
| Any alphabetical character                          | `[[:alpha:]]`                                    |                                                          | `[[:alpha:]]`                        | `[[:alpha:]]`                        | `\a` `[[:alpha:]]`                     |     |                         |
| Non-alphabetical character                          |                                                  |                                                          | `[^[:alpha:]]`                       | `[^[:alpha:]]`                       | `\A``[^[:alpha:]]`                     |     |                         |
| Any alphanumerical character                        | `[[:alnum:]]`                                    |                                                          | `[[:alnum:]]`                        | `[[:alnum:]]`                        | `[[:alnum:]]`                          |     |                         |
| ASCII                                               | `[[:ascii:]]`                                    |                                                          |                                      |                                      |                                        |     |                         |
| Character equivalents (e = é = è) (as per locale)   |                                                  |                                                          | `[[=e=]]`                            | `[[=e=]]`                            | `[[=e=]]`                              |     |                         |
| Zero-width assertions                               |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Word boundary                                       | `\b`                                             | `\b`                                                     | `\b` / `\<` (start) / `\>` (end)     | `\b` / `\<` (start) / `\>` (end)     | `\<` (start) / `\>`(end)               |     |                         |
| Anywhere but word boundary                          | `\B`                                             | `\B`                                                     | `\B`                                 | `\B`                                 |                                        |     |                         |
| Beginning of line/string                            | `^` / `\A`                                       | `^` / `\A`                                               | `^`                                  | `^`                                  | `^` (beginning of pattern ) `\_^`      |     |                         |
| End of line/string                                  | `$` / `\Z`                                       | `$` / `\Z`                                               | `$`                                  | `$`                                  | `$` (end of pattern) `\_$`             |     |                         |
| Captures and groups                                 |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Capturing group                                     | `(...)` `(?<name>...)`                           | `(...)` `(?P<name>...)`                                  | `\(...\)`                            | `(...)`                              | `\(...\)`                              |     |                         |
| Non-capturing group                                 | `(?:...)`                                        | `(?:...)`                                                |                                      |                                      | `\%(...\)`                             |     |                         |
| Backreference to a specific group.                  | `\1` `\g1` `\g{-1}`                              | `\1`                                                     | `\1`                                 | `\1` non-official                    | `\1`                                   |     |                         |
| Named backreference                                 | `\g{name}` `\k<name>`                            | `(?P=name)`                                              |                                      |                                      |                                        |     |                         |
| Look-around                                         |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Positive look-ahead                                 | `(?=...)`                                        | `(?=...)`                                                |                                      |                                      | `\(...\)\@=`                           |     |                         |
| Negative look-ahead                                 | `(?!...)`                                        | `(?!...)`                                                |                                      |                                      | `\(...\)\@!`                           |     |                         |
| Positive look-behind                                | `(?<=...)`                                       | `(?<=...)`                                               |                                      |                                      | `\(...\)\@<=`                          |     |                         |
| Negative look-behind                                | `(?<!...)`                                       | `(?<!...)`                                               |                                      |                                      | `\(...\)\@<!`                          |     |                         |
| Multiplicity                                        |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| 0 or 1                                              | `?`                                              | `?`                                                      | `\?`                                 | `?`                                  | `\?`                                   |     |                         |
| 0 or more                                           | `*`                                              | `*`                                                      | `*`                                  | `*`                                  | `*`                                    |     |                         |
| 1 or more                                           | `+`                                              | `+`                                                      |                                      | `+`                                  | `\+`                                   |     |                         |
| Specific number                                     | `{n}` `{n,m}` `{n,}`                             | `{n}` `{n,m}``{n,}`                                      | `\{n\}` `\{n,m\}` `\{n,\}`           | `{n}` `{n,m}``{n,}`                  | `\{n}` `\{n,m}` `\{n,}`                |     |                         |
| 0 or 1, non-greedy                                  | `??`                                             | `??`                                                     |                                      |                                      |                                        |     |                         |
| 0 or more, non-greedy                               | `*?`                                             | `*?`                                                     |                                      |                                      | `\{-}`                                 |     |                         |
| 1 or more, non-greedy                               | `+?`                                             | `+?`                                                     |                                      |                                      |                                        |     |                         |
| Specific number, non-greedy                         | `{n,m}?` `{n,}?`                                 | `{n,m}?``{n,}?`                                          |                                      |                                      | `\{-n,m}` `\{-n,}`                     |     |                         |
| 0 or 1, don't give back on backtrack                | `?+`                                             |                                                          |                                      |                                      |                                        |     |                         |
| 0 or more, don't give back on backtrack             | `*+`                                             |                                                          |                                      |                                      |                                        |     |                         |
| 1 or more, don't give back on backtrack             | `++`                                             |                                                          |                                      |                                      |                                        |     |                         |
| Specific number, don't give back on backtrack       | `{n,m}+` `{n,}+`                                 |                                                          |                                      |                                      |                                        |     |                         |
| Other                                               |                                                  |                                                          |                                      |                                      |                                        |     |                         |
| Independent non-backtracking pattern                | `(?>...)`                                        |                                                          |                                      |                                      | `\(...\)\@>`                           |     |                         |
| Make case-sensitive/insensitive                     | `(?i)` / `(?-i)`                                 | `(?i)` / `(?-i)`                                         |                                      |                                      | `\c` / `\C`                            |     |                         |