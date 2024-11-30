
Test Topics
* [apt](#apt)
* [chown](#chown)
* [chmod](#chmod)
* [color syntax](#color-syntax)
* [file permissions](#file-perms)
* [file system](#file-system)
* [grep](#grep)
* [htop](#htop)
* [kill](#kill-process)
* [scp](#scp)
* [systemd commands](#systemd-commands)
* [scripting](#bash scripting)
* [signals](#signals)
* [ssh](#ssh)
* [top](#top)
* [vim](#vim)
* [users & groups](#users-&-groups)

# apt
apt-file search
`apt-file search bin/tmux`

# chown
`chown [options] [owner][:[group]] file`

| Command                      | Description                                                                   |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `chown $user $file`          | changes the user to `$user` on `$file`.                                       |
| `chown $user:$group $folder` | changes the user to `$user` and the group to `$group`.                        |
| `chown :$group $folder`      | change the group of the `folder` to `$group`.                                 |
| `chown $user: $file`         | change the user to `$user` and the group to the primary group of the `$user`. |

# chmod
File and folder permissions can be changed with `chmod`:
* Stands for change mode  
* Used in conjunction with numeric or character permissions
```
chmod [options]... mode[,mode]... file...
chmod [options]... numeric_mode file...
```
to make a file executable when creating a shell script in vim use:
`chmod +x script.sh`

# file-perms
## Numeric Permissions
`ls -ld $file`
## Permissions breakdown
The first 10 characters is the file type
*  `-` means a regular file
* `b` Block special
* `d` directory
* `l` symbolic link
* `s` socket
* `p` named pipe
* `c` character device file
### Numerical Values
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
## umask
sets default permissions for newly created files and folders.
`umask [-S] [mask]`

## Adding permissions
#### Groups
`groupadd $username`
`gpasswd -a $username $group`



# file-system
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

# color-syntax
`echo -e "\033[0m"` - normal
`echo -e "\033[32m this is green\033[0m back to normal"`
outputs terminal color to green and back to normal

# kill-process
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

# systemd-commands
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

# users-&-groups
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

# vim

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
# example bash questions
* create a script to read each line of a file. each line will contain a path to a file, delete that file.

* create a script to check if the number a user provided in the first argument is greater than the number in the second argument

* use brace expansion to create all folders following this pattern from a-z outputa, outputb, outputc


---
ranger - file explorer
glow - markdown files