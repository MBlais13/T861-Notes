
# CheatSheet

```bash
evans stuff = /home/student
```

## Apache
- **Install Apache & PHP:**
  ```bash
  sudo apt install apache2 php libapache2-mod-php php-mysql curl
  sudo systemctl enable apache2
  ```
#### Config Files
- **Main Config File:** `/etc/apache2/apache2.conf`
- **Site Configs:** `/etc/apache2/sites-available/`
	- (`/etc/apache2/sites-available/example.com.conf`)
- Mods Available: `/etc/apache2/mods-available/`
- Web Root Directory: `/var/www/html`
#### Log Files:
   - `/var/log/apache2/access.log`
   - `/var/log/apache2/error.log`
#### Check Enabled Modules:
```bash
  apache2ctl -M
```
#### Enable/Disable Modules & Sites:
  ```bash
sudo a2enmod ssl # Enable
sudo a2dismod ssl # Disable

sudo a2ensite example.com.conf
sudo systemctl reload apache2

sudo a2enmod ssl
sudo a2enmod rewrite
sudo a2enmod headers
sudo a2ensite default-ssl

sudo a2enmod php8.1
sudo systemctl restart apache2
  ```
#### Check Config:
```bash
sudo apachectl configtest     # Validate config
```
#### Enable Reverse Proxy:
  ```bash
  sudo a2enmod proxy proxy_http
  ```
#### Full Virtual Host Config:
**File:** `/etc/apache2/sites-available/example.com.conf`
```xml
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

  <Directory /var/www/example>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>
  ErrorLog ${APACHE_LOG_DIR}/example_ssl_error.log
  CustomLog ${APACHE_LOG_DIR}/example_ssl_access.log combined
</VirtualHost>
```
#### Alias Example:
```bash
  Alias /robots.txt /var/www/html/common/robots.txt
```

---



## MariaDB
- **Config File:** `/etc/mysql/mariadb.conf.d/50-server.cnf`
#### Basic Setup:
```bash
sudo mysql -u root -p

#login to mariadb
sudo mariadb             # Login as root
mariadb -u username -p   # Login with a user
```
#### Create a database:
```sql
CREATE DATABASE MIT450;
USE MIT450;
```
#### Create a user & set permissions:
make sure to `FLUSH PRIVILEGES;` to apply changes
```sql
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin'; -- creates user 'admin' with password 'admin'
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION; -- grants all permissions
FLUSH PRIVILEGES; -- applies changes

-- Set password for existing user
SET PASSWORD FOR 'username'@'localhost' = PASSWORD('new_password');
-- or
ALTER USER 'username'@'localhost' IDENTIFIED BY 'new_password';
```
#### View permissions/privileges:
```sql
SHOW GRANTS FOR 'admin'@'localhost';
```
#### Log in as a user:
```bash
mariadb -u admin -p -h localhost
```
#### Confirm logged in as correct user:
```sql
SELECT USER();
```
#### Create tables:
```sql
CREATE TABLE students (
  student_id INT AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL
);

--foreign key--
CREATE TABLE courses (
  course_id INT AUTO_INCREMENT PRIMARY KEY,
  course_name VARCHAR(100) NOT NULL,
  student_id INT,
  FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```
#### CRUD examples:
```sql
INSERT INTO students (first_name, last_name) VALUES ('Alice', 'Johnson');
SELECT * FROM students;
UPDATE students SET last_name = 'Smith' WHERE student_id = 1;
DELETE FROM students WHERE student_id = 1;
```
#### Backup & Restore:
```bash
mysqldump -u root -p myDB > backup.sql       # Backup
mysql -u root -p myDB < backup.sql           # Restore
```
#### Other useful commands:
```sql
SHOW TABLES;
SHOW DATABASES;
USE myDB;
SHOW GRANTS FOR 'user'@'host';
\q    -- Quit
```
#### Read-only privilege:
```sql
GRANT SELECT ON datawarehouse.* TO 'osabri'@'localhost';
```
#### Read/Write privilege:
```sql
GRANT SELECT, UPDATE ON datawarehouse.* TO 'osabri'@'localhost';
```
#### Connect from localhost only:
```shell
mysql -u admin -p"pass" -h localhost
```
#### Connect remotely:
```bash
mysql -u admin -p"pass" --host=php.scweb.ca --port=3306
```
#### Notes:
- **Show Stuff:**
```sql
SHOW DATABASES;, SHOW TABLES;, SHOW GRANTS FOR 'user'@'host';
```
- Use DROP DATABASE dbname; **with caution**.
- Type \q to quit MySQL shell - also use `EXIT;`.
- localhost can be replaced with % (any host) or a specific IP/domain if needed.
- create user and grant permissions (explained):
```sql
CREATE USER 'user1'@'localhost' IDENTIFIED BY 'password';

-- Grant all privileges
GRANT ALL PRIVILEGES ON myDB.* TO 'user1'@'localhost';

-- Specific privileges
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, INDEX,
      CREATE TEMPORARY TABLES, CREATE VIEW, SHOW VIEW, TRIGGER,
      REFERENCES, EXECUTE, FILE, GRANT OPTION, LOCK TABLES,
      EVENT, RELOAD, PROCESS, SHUTDOWN, SUPER
ON myDB.* TO 'user1'@'localhost';

FLUSH PRIVILEGES;  -- Reload privilege tables
```
- What Flush Privileges does:
	- Does **not** delete or add privileges
	- Reloads privileges from database files into memory
	- Activates changes you’ve already made
---

## DNS
#### Config Files:
- Config File: `/etc/bind/named.conf`
- Zone Config File: `/etc/bind/named.conf.local`,  `/etc/bind/named.conf.zones`
- Forward Zone: `/etc/bind/db.example.com`
- Reverse zone: `/etc/bind/db.192`
#### Install:
```bash
sudo apt install bind9
sudo systemctl enable named
```
#### Common Records:
  ```
  A     - Maps name to IPv4
  AAAA  - Maps name to IPv6
  CNAME - Alias
  MX    - Mail Server
  NS    - Authoritative DNS server
  PTR   - Reverse DNS
  SOA   - Zone metadata
  TXT   - Text record for SPF, DKIM, etc.
  ```
#### DNS Tools:
```bash
  dig example.com
  dig @8.8.8.8 google.com
  nslookup google.com
  named-checkconf
  named-checkzone mike.com db.mike.com
  systemctl restart named
  host domain.com
  dig -x 10.0.0.14 @localhost
```
#### Create A Record:
  ```
  ns.example.com. IN A 192.168.1.111
  @ IN A 192.168.1.111
  ```
#### Sample Zone Block: `/etc/bind/named.conf.local`
  ```bash
  zone "mysite.com" {
    type master;
    file "/etc/bind/db.mysite.com";
  };
  ```
#### Reverse Zone Example (db.10.0.0):
```conf
$TTL 86400
@ IN SOA main.mike.com. test.mike.com. (
  2025041701 ; Serial
  3600 ; Refresh
  1800 ; Retry
  1209600 ; Expire
  86400 ) ; Minimum TTL
  IN NS main.mike.com.
14 IN PTR www.mike.com.
```
#### Zone File Template (db.mike.com):
```conf
$TTL 86400
@ IN SOA main.mike.com. test.mike.com. (
  2025041701 ; Serial
  3600       ; Refresh
  1800       ; Retry
  1209600    ; Expire
  86400 )    ; Minimum TTL

  IN NS main.mike.com.
  IN MX 10 mail.mike.com.
www IN A 10.0.0.14
mail IN A 10.0.0.14
```
#### /etc/hosts Entry:
```conf
127.0.0.2 test.mike.com
```
#### Check Config & Restart:
```bash
named-checkconf
named-checkzone example.com /etc/bind/db.example.com
sudo systemctl restart bind9
```
#### Time Conversion:

|**Hours**|**Seconds**|
|---|---|
|1|3600|
|2|7200|
|3|10800|
|4|14400|
|6|21600|
|12|43200|
#### Notes:
- what is a root DNS server?
	The top-level server that directs DNS queries
- what is a domain zone?
	A domain or IP range managed by DNS
- what is a bind server?
	a popular DNS server for linux
- what is BIND9
	a version of the BIND DNS software
- what is the command to query DNS records
	`Dig`
- command to check DNS config
	`named-checkconf /etc/bind/named.conf`
- command to check DNS resolution
	`nslookup google.com`
- check IP address of site using DIG
	`dig google.com`
- How to check if a DNS server is reachable for a site
	`dig @8.8.8.8 google.com`
- start DNS server at startup
	`sudo systemctl enable bind9`
- create new zone file for your domain blue.com
	`sudo nano /etc/bind/db.blue.com`
---

## SFTP
- SSHD Config File: `/etc/ssh/sshd_config`
- Basic Config File: `/etc/vsftpd.conf`

- restart service: `sudo systemctl restart vsftpd`
#### Install & Enable:
```bash
sudo apt install vsftpd
sudo apt install openssh-server
sudo systemctl enable vsftpd
```
#### Active vs Passive
- **Active:** Server connects **back** to client (less firewall-friendly)
- **Passive:** Server tells client what port to use (firewall/NAT friendly)
#### Add User:
  ```bash
 sudo groupadd sftpusers
 sudo useradd -m -d /home/sftpuser -s /sbin/nologin -G sftpusers sftpuser
 sudo passwd sftpuser

 sudo mkdir /home/sftpuser/in
 sudo chown root:root /home/sftpuser
 sudo chmod 755 /home/sftpuser
 sudo chown sftpuser:sftpusers /home/sftpuser/in
  ```
  - simple add user
```bash
  echo "ftpuser" | sudo tee -a /etc/vsftpd.userlist
```
#### Chroot Jail Setup:
  ```bash
  sudo chown root:root /home/sftpuser
  sudo chmod 755 /home/sftpuser
  sudo mkdir /home/sftpuser/uploads
  sudo chown sftpuser:sftpuser /home/sftpuser/uploads
  sudo chmod 755 /home/sftpuser/uploads
  ```
#### Basic Config:
```config
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
chroot_local_user=YES
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```
#### Match Block in: `sshd_config`
  ```
  Match User sftpuser
    ChrootDirectory /home/sftpuser
    ForceCommand internal-sftp
    X11Forwarding no
    AllowTcpForwarding no
  ```

#### Setup SSL:
Enable SSL Module:
```bash
a2enmod ssl
```
Keys:
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/vsftpd.key \
-out /etc/ssl/certs/vsftpd.crt
```
- Add to vsftpd.conf:
```config
ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key

pasv_enable=YES
pasv_min_port=10090
pasv_max_port=10090
```
#### Common Config Changes: `/etc/vsftpd.conf`
- anonymous_enable=NO
- local_enable=YES
- write_enable=YES
- chroot_local_user=YES

---

## FTP (vsftpd)
#### Config Files
- **Main Config File:** `/etc/vsftpd.conf`
- **Blocked Users File:** `/etc/ftpusers`
#### Passive Mode:
```conf
  pasv_enable=YES
  pasv_min_port=40000
  pasv_max_port=50000
```
#### Multi Listen:
```conf
  listen_address=127.0.0.1
  listen_address=192.168.1.25
```
#### Create RSA Cert:
  ```bash
  openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/vsftpd.key \
    -out /etc/ssl/certs/vsftpd.pem
  ```
#### Chroot Setup:
- Set `chroot_local_user=YES` in vsftpd.conf

---

## SSH
#### Test SSH Config:
```bash
sudo sshd -t
```
#### Disable Root Login: `/etc/ssh/sshd_config`
```bash
PermitRootLogin no
PasswordAuthentication yes
```
#### Generate Keys:
  ```bash
  ssh-keygen -t rsa -b 4096 -C "email@example.com"
  ```
#### Copy Public Key:
  ```bash
  cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  ```
#### Dynamic Proxy:
  ```bash
  ssh -D 1080 user@host
  ```
#### Tunneling:
  ```bash
  ssh -L 54000:10.13.37.2:3389 root@server.com
  ssh -L 3307:192.168.2.50:3306 user@dbserver.com
  ```
---

## SCP vs SFTP Comparison

| Task                    | SCP Command                                  | SFTP Command             |
| ----------------------- | -------------------------------------------- | ------------------------ |
| Upload                  | `scp local.txt user@host:/tmp/`              | `put local.txt /tmp/`    |
| Download                | `scp user@host:/tmp/file.txt .`              | `get /tmp/file.txt`      |
| Rename Upload           | `scp local.txt user@host:/tmp/newname.txt`   | N/A                      |
| List Local Files        | N/A                                          | `lls /tmp/`              |
| Download remote .bashrc | `pscp -P 22 user@host:/home/user/.bashrc ./` | `get /home/user/.bashrc` |

```bash
scp file.txt user@host:/path/to/destination
scp user@host:/path/to/file.txt ./localdir

# FROM local → VM
pscp -P 49291 ex.txt student@<AZURE_HOST>:~/student

# FROM VM → local desktop
pscp -P <PORT> student@<AZURE_HOST>:~/student/ex.txt C:\Users\YourName\Desktop\
```
---

## NFS
- **Config Files:** `/etc/exports`, `/etc/nfs.conf`
#### Install:
```bash
sudo apt install nfs-kernel-server
```
#### Share Setup:
  ```bash
  sudo mkdir -p /homeshare/user1
  sudo chown user1:user1 /homeshare/user1
  echo "/homeshare 127.0.0.1(rw,sync,subtree_check)" | sudo tee -a /etc/exports
  sudo systemctl restart nfs-server
  ```
- export means to allow read and write access to the shared directory.
#### Export File Config: `/etc/exports`
```config
/homeshare 127.0.0.1(rw,sync,subtree_check)
```
#### Auto Mount at boot via fstab: `/etc/fstab`
```config
  127.0.0.1:/homeshare /mnt nfs defaults 0 0
```
#### Mount: 
```bash
sudo apt install nfs-common
sudo mount -t nfs 10.0.0.14:/srv/nfs /mnt/nfs

# basic mount
sudo mount server_ip:/home/nfs /mnt
```
### Restart:
```bash
sudo exportfs -a
sudo systemctl restart nfs-server
```
#### Options:
- -o ro = Read-only
- -o rw = Read/Write
- sync = Safe
- async = Fast
---

## SMB (Samba)
- **Config File:** `/etc/samba/smb.conf`
#### Install:
  ```bash
  sudo apt install samba smbclient samba-common
  ```
#### Add User:
  ```bash
  sudo smbpasswd -a user
  ```
#### Restart Services:
  ```bash
  sudo systemctl restart smb nmb
  sudo systemctl restart smbd
  ```
#### SELinux Command (if needed):
  ```bash
  sudo chcon -t samba_share_t /smbshare
  sudo restorecon -v /smbshare
  ```
#### Test Config:
  ```bash
  testparm
  ```
#### Example Config: `/etc/samba/smb.conf`
```config
[share]
    path = /srv/samba
    valid users = sambauser
    read only = no
    browsable = yes
    guest ok = no
```
#### Mount Windows Share:
```bash
sudo apt install cifs-utils
sudo mount -t cifs //hostname/share /mnt -o user=sambauser
```
#### UnMount and check:
```bash
df -h
sudo umount /mnt
```
### Other SMB Commands:
```bash
sudo smbpasswd -a sambauser
sudo systemctl restart smbd
```
---

## General Commands

#### Enable service at boot:
  ```bash
  sudo systemctl enable apache2
  sudo systemctl enable mariadb
  sudo systemctl enable bind9
  ```
#### Reload firewall:
  ```bash
  firewall-cmd --reload
  ```

---
