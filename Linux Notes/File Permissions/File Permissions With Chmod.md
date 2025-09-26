#unix-permissions

## Permissions continued
* Broken down into 3 different groups of 3:
	* `user permissions` - based user owner
	* `group permissions` - based on group owner
	* `other permissions` - all other users
* Each 3 is broken into: 
	* `r` Read
	* `w` Write
	* `x` Execute

---
# Symbolic Notation Syntax

- `r`: **R**ead
- `w`: **W**rite
- `x`: e**X**ecute

| Who (Letter) | Meaning |
| ------------ | ------- |
| **u**        | user    |
| **g**        | group   |
| **o**        | others  |
| **a**        | all     |

## Using Operators
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
# Numeric Notation Syntax

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

# References
https://www.linode.com/docs/guides/modify-file-permissions-with-chmod/
https://unix.stackexchange.com/questions/94212/chmod-by-letters-vs-numbers

