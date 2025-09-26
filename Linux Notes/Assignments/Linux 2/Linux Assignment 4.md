w0844719_michaelb.docx

Student ID: w0844719
Name: Michael Blais

---

## 1. Script

```bash nums
#!/bin/bash

if [ $# -ne 1 ]
then
	echo "no args"
	exit
fi

if [! -f /usr/sbin/vsftpd]
then
	sudo apt-get install vstpd -y 2>/dev/null
fi

USERNAME="$1"
HOME_DIR="/home/$USERNAME"
USER_PASS=$(openssl rand -base64 12)
FTP_DIR="$HOME_DIR/ftp"

useradd -m -s /sbin/nologin "$USERNAME"
echo "$USERNAME: $USER_PASS" | chpasswd
mkdir -p "SFTP_DIR/upload"

chown root:root "$HOME_DIR"
chown -R "$USERNAME" : "$USERNAME" "$FTP_DIR"
chmod 755 "$HOME_DIR"
chmod 750 "$FTP_DIR"
chmod 700 "$FTP_DIR/upload"

if ! grep -q "^chroot_local_user=" /etc/vsftpd.conf;
then
	echo "chroot_local_user=YES" >> /etc/vsftpd.conf
fi

systemctl restart vsftpd
echo "made ftp account for: $USERNAME"
echo "password is: $USER_PASS"
```

only throwaway linux vm available disregard user.. ran out of lab hours ;(
![[Pasted image 20250409154635.png]]