doc_name: 0844719_michaelblais.docx

am I supposed to do this on the linux vm??
## Commands
```shell
# make department folders
mkdir /shared
mkdir /shared/sales /shared/hr /shared/naptime

# make groups
groupadd sales_grp
groupadd hr_grp
groupadd naptime_grp

# set permissions
chown root:sales_grp /shared/sales
chown root:hr_grp /shared/hr
chown root:naptime_grp /shared/naptime
chmod 2770 /shared/sales
chmod 2770 /shared/hr
chmod 2770 /shared/naptime
# fingers crossed
```


## Script
```bash
#!/bin/bash

# w0844719 - mikey

# check file exists
if [ ! -f "$1" ]; then
    echo "Usage: $0 <userfile>"
    exit 1
fi

while IFS='|' read -r fullname email username departments; do
    # create user ++ home directory & bash shell
    useradd -m -s /bin/bash "$username" -c "$fullname"
    
    # random password - 11/10 losing my mind
    password=$(openssl rand -base64 12)
    # set the password and expire
    echo "$username:$password" | chpasswd
    passwd --expire "$username"

    # add user to department groups
    for dept in $(echo "$departments" | tr ',' ' '); do
        usermod -aG "${dept}_grp" "$username"
    done

    # output results
    echo "User: $username, Pass: $password"
done < "$1"
# runs off of hopes and dreams
```

## File Format
```bash
Mikey Boy|mikeyboy@bullshitcorp.com|mboy|sales,naptime
```

## Final Output
```bash
root@ML-RefVm-370084:/shared# ./assignment1.sh userfile
passwd: password changed.
User: mboy, Pass: UGmz9LQpj1/kd5Pd
```
running again results in:
```bash
useradd: user 'mboy' already exists
passwd: password changed.
```

Needs some sort of empty line validation, any blank lines will result in an error. I quit.