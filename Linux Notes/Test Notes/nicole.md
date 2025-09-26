

 **1. MariaDB / MySQL Cheatsheet**
 **Login & Users**
sudo mariadb              # Login as root
mariadb -u username -p    # Login with a user (will prompt for password)

**Creating a Database**
CREATE DATABASE myDB;

**Creating and Granting Privileges to Users**
CREATE USER 'user1'@'localhost' IDENTIFIED BY 'password';

  -- Grant all privileges on one database
GRANT ALL PRIVILEGES ON myDB.* TO 'user1'@'localhost';

-- Specific privileges
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, INDEX,
       CREATE TEMPORARY TABLES, CREATE VIEW, SHOW VIEW, TRIGGER,
       REFERENCES, EXECUTE, FILE, GRANT OPTION, LOCK TABLES,
       EVENT, RELOAD, PROCESS, SHUTDOWN, SUPER
ON myDB.* TO 'user1'@'localhost';
  
-- Refresh privileges
FLUSH PRIVILEGES;
**What does FLUSH PRIVILEGES do?**
It does NOT delete privileges.  
It does NOT change or add any new privileges.  
It simply reloads the existing privileges from the database files into memory.
It activates or refreshes what's already been changed
  
 **Connecting with User and Password from CLI**
mariadb -u user1 -p     # (Enter password when prompted)
**Backup and Restore**
mysqldump -u root -p myDB > backup.sql        # Backup 
mysql -u root -p myDB < backup.sql            # Restore from backup
**Tips**
- Use SHOW DATABASES;, SHOW TABLES;, SHOW GRANTS FOR 'user'@'host';
- Use DROP DATABASE dbname; with caution…
- Use \q to quit the MySQL shell.

 **2. DNS Cheatsheet**
 **Zone File Example (db.gyorgy.com)**
```
$TTL 86400
@   IN  SOA main.gyorgy.com. nicole.gyorgy.com. (
        2025041701 ; Serial //I**ncrement** this every time you make changes to the zone file…
        3600       ; Refresh //**Range:** Usually 15 minutes (900) to 12 hours (43200)
        1800       ; Retry  //**Rule of thumb:** About half the refresh value 
        1209600    ; Expire //**Range:** Often between 1–4 weeks
        86400 )    ; Minimum TTL //**Common value:** 86400 = 1 day
  
    IN  NS   main.gyorgy.com.
    IN  MX 10 mail.gyorgy.com.
www IN  A    10.0.0.14
mail IN  A   10.0.0.14
```

| **Hours** | **Seconds** |
| --------- | ----------- |
| 1         | 3600        |
| 2         | 7200        |
| 3         | 10800       |
| 4         | 14400       |
| 5         | 18000       |
| 6         | 21600       |
| 7         | 25200       |
| 8         | 28800       |
| 9         | 32400       |
| 10        | 36000       |
| 11        | 39600       |
| 12        | 43200       |

  

 **Record Types**

- A – Maps name to IP
- CNAME – Alias to another name
- MX – Mail server
- NS – Name server
- PTR – Reverse DNS
- SOA – Start of Authority
- TXT – Text record for SPF/DKIM

  

 **Tools and Commands**
named-checkconf
named-checkzone gyorgy.com db.gyorgy.com
systemctl status named
systemctl restart named
# Query DNS records
host domain.com
nslookup domain.com
dig domain.com
  
dig -x 10.0.0.14 @localhost   # Reverse lookup (PTR)
 **Reverse Zone File (db.10.0.0)**
$TTL 86400
@ IN SOA main.gyorgy.com. nicole.gyorgy.com. (
    2025041701 ; Serial
    3600 ; Refresh
    1800 ; Retry
    1209600 ; Expire
    86400 ) ; Minimum TTL
  IN NS main.gyorgy.com.
14 IN PTR www.gyorgy.com.
 **/etc/hosts Entry**
127.0.0.2 test.gyorgy.com
  
 **3. Apache and PHP Cheatsheet**
 **Full Virtual Host Example (HTTP & HTTPS)**
**File: /etc/apache2/sites-available/example.com.conf**
<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example  
    <Directory /var/www/example>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/example_error.log
    CustomLog ${APACHE_LOG_DIR}/example_access.log combined
</VirtualHost>


<VirtualHost *:443>
    ServerAdmin admin@example.com
    ServerName example.com
    DocumentRoot /var/www/example
  
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
    SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
// ^^^ To find these certs do : VIM /etc/apache2/sites-available/default-ssl.conf
    <Directory /var/www/example>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
        ErrorLog ${APACHE_LOG_DIR}/example_ssl_error.log
    CustomLog ${APACHE_LOG_DIR}/example_ssl_access.log combined
</VirtualHost>

 **Enable Site and Reload Apache**
sudo a2ensite example.com.conf
sudo systemctl reload apache2

 **Enable SSL and Modules**
sudo a2enmod ssl
sudo a2enmod rewrite
sudo a2enmod headers
sudo a2ensite default-ssl
sudo systemctl restart apache2
 **Validate Apache Config**
sudo apachectl configtest

 **Enable PHP**
sudo a2enmod php8.1
sudo systemctl restart apache2

 **4. SSH and SFTP Cheatsheet**
 
 **Disable Root Login**
sudo nano /etc/ssh/sshd_config
PermitRootLogin no
PasswordAuthentication yes

 **Chroot Setup for SFTP Group**
Match Group sftpusers
    ChrootDirectory %h
    ForceCommand internal-sftp
    X11Forwarding no
    AllowTcpForwarding no
    
 **Create SFTP User**
sudo groupadd sftpusers
sudo useradd -m -d /home/sftpuser -s /sbin/nologin -G sftpusers sftpuser
sudo passwd sftpuser
sudo mkdir /home/sftpuser/in
sudo chown root:root /home/sftpuser
sudo chmod 755 /home/sftpuser
sudo chown sftpuser:sftpusers /home/sftpuser/in

 **Verify SSH Config**
sudo sshd -t

 **SCP File Transfer**
scp file.txt user@host:/path/to/destination
scp user@host:/path/to/file.txt ./localdir
  
**Scp transfer of ex.txt from local computer’s desktop  to our VM (student’s home directory)**
pscp -P 49291 ex.txt student@[everything after the ‘@’ in our Azure link]:/home/student


**Scp transfer of ex.txt from our VM (student’s home directory) to our computer’s local desktop**
pscp -P [PORT] username@hostname:/remote/path/to/file C:\Users\YourName\Desktop\
example: pscp -P [our port here] student@[everything after the ‘@’ in our Azure link]:/home/student/ex.txt C:\Users\nicol\Desktop\

^^^The above commands would both be done within the local computer’s command prompt

  

 **5. FTP / VSFTPD Cheatsheet**
 **vsftpd.conf Settings (Basic + SSL)**
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
chroot_local_user=YES
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO


 **SSL Certificate Setup**
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/vsftpd.key \
-out /etc/ssl/certs/vsftpd.crt

**Add to vsftpd.conf:**
ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key

pasv_enable=YES
pasv_min_port=10090
pasv_max_port=10090

 **Add User to Userlist**
echo "ftpuser" | sudo tee -a /etc/vsftpd.userlist

 **Verify & Restart**
vsftpd -version
sudo systemctl restart vsftpd

 **Active vs Passive FTP**
- **Active:** Client opens port, server connects back — may fail with firewalls.
- **Passive:** Server tells client what port to use — firewall/NAT friendly.

 **6. NFS and Samba Cheatsheet**
 
 **NFS Server Setup**
sudo apt install nfs-kernel-server

**/etc/exports**
/srv/nfs 10.0.0.0/24(rw,sync,no_subtree_check)
sudo exportfs -a
sudo systemctl restart nfs-server

 **NFS Client Mount**
sudo apt install nfs-common
sudo mount -t nfs 10.0.0.14:/srv/nfs /mnt/nfs
- -o ro = read-only
- -o rw = read-write
- sync = write confirmed before success
- async = faster but less safe

 **Samba Server Setup**
sudo apt install samba

**/etc/samba/smb.conf**

[share]
    path = /srv/samba
    valid users = sambauser
    read only = no
    browsable = yes
    guest ok = no
sudo smbpasswd -a sambauser
sudo systemctl restart smbd

**Mount Windows Share (Client)**
sudo apt install cifs-utils
sudo mount -t cifs //hostname/share /mnt -o user=sambauser

 **Verify or Unmount**
df -h
sudo umount /mnt

 **Notes**
- User and group IDs may mismatch between client and server (check /etc/passwd and /etc/group)
- Samba users must be system users and added with smbpasswd -a