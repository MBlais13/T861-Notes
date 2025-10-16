#share


## Mount NFS

define mount options in `/etc/fstab`
```
sudo mount -o rw 172.16.125.128:/shared /mount/shared
```


 Example For `/shared`
 Do not put a space between the host and bracket
```
/shared 192.168.1.0/24(rw,sync,no_subtree_check,root_squash)
```


```
{remote location} {local location} {type} [options, ...]
--
172.16.125.128:/shared /mount/shared nfs rw,users,noauto
```
- noauto = don’t automount
- users = allow other users to mount this drive
- rw = read write

## Unmount
```
sudo umount ~/mnt
```


