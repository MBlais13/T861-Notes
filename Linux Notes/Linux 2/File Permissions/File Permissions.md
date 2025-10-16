

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

### Permissions continued
* Broken down into 3 different groups of 3:
	* `user permissions` - based user owner
	* `group permissions` - based on group owner
	* `other permissions` - all other users
* Each 3 is broken into: 
	* `r` Read
	* `w` Write
	* `x` Execute

### Numeric Permissions
* `r` = 4
* `w` = 2
* `x` = 1

Example:
* `rw-r--r--` = 644
* `rwx------` = 700
* `rwxrw-r--` = 764
* `rwxrwxrwx `= 777

### Breakdown
Highest possible permissions, This gives EVERYONE full permissions:

| user | group | other |
| ---- | ----- | ----- |
| rwx  | rwx   | rwx   |
| 777  | 777   | 777   |

This gives a user full control but only lets users in a group read the files:

| user | group | other |
| ---- | ----- | ----- |
| rwx  | rwx   | rwx   |
| 777  | 7--   | ---   |

### Adding permissions
#### Groups
`groupadd $name`
`gpasswd -a $name $group`



## Special Permissions
### Sticky Bit
`d---------`
`----------`
`---------t`


### chmod
File and folder permissions can be changed with `chmod`:
* Stands for change mode  
* Used in conjunction with numeric or character permissions
```
chmod [options]... mode[,mode]... file...
chmod [options]... numeric_mode file...
```

### chown
Lets you change the user/group owner.
The user and group owners can be changed with `chown`
* Stands for change owner
```
chown [options] [owner][:[group]] file
```

| Command                      | Description                                                                   |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `chown $user $file`          | changes the user to `$user` on `$file`.                                       |
| `chown $user:$group $folder` | changes the user to `$user` and the group to `$group`.                        |
| `chown :$group $folder`      | change the group of the `folder` to `$group`.                                 |
| `chown $user: $file`         | change the user to `$user` and the group to the primary group of the `$user`. |



### umask
sets default permissions for newly created files and folders.
```
umask [-S] [mask]
```


