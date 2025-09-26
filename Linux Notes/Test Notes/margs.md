

**MariaDB**
Secure installation and add password: mysql_secure_installation
Log in to Mariadb shell: mysql -u root -p
mysql -u bob -p"drowssap" --host=php.scweb.ca --port=3306
-u user
-p password (if none included it prompts
-D database
mariadb -u admin -p -h localhost

CREATE USER ‘{username}’@’localhost’ IDENTIFIED BY ‘{password}’;	(% instead of localhost for remote, can be ip too)
CREATE DATABASE wwwprod;
USE wwwprod;
GRANT ALL PRIVILEGES ON wwwprod.* to {username}@localhost;	(WITH GRANT OPTION at the end to make them able to grant priviledges)
SELECT user,host,password FROM mysql.user;
SHOW GRANTS FOR ‘{username}’@localhost;
read-only: GRANT SELECT ON wwwprod.* to {username}@localhost;
update: GRANT UPDATE ON wwwprod.* to {username}@localhost;	(comma and space for multiple)
REVOKE to remove priviledges
FLUSH PRIVILEGES;
SELECT USER();		User you're logged in as

mysql> CREATE DATABASE mit416;
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT,
    OrderNumber DECIMAL(5,2),
    PersonID TEXT,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
); 
INSERT INTO employee VALUES (DEFAULT,"Franco", "Iacobacci", "Networking");
UPDATE employee SET department="IT" WHERE id=1;
DELETE FROM employee WHERE id=1;

mysqldump -u {youname} -p{password} {databaseName} > {databaseName}.sql

Resetting the root password
1. Stop the mysqld service
2. Run mysqld_safe --skip-grant-tables &
3. Login to mysql shell using mysql
4. Update forgotten password using ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
FLUSH PRIVILEGES;
5. Restart service

Start at boot: systemctl enable mariadb





**DNS**
A = IPv4 address record
AAAA = IPv6 address record
CNAME = Canonical name record (one domain linking to another)
MX = Mail Exchanger record
NS = Name Server Record
PTR = Reverse pointer lookup records
TXT = Text record, often used for security and verification
purposes
SOA = start of authority, used int DNS configuration

/etc/bind/named.conf.options:
listen-on port 53 {127.0.0.1; 10.0.0.8; };
allow-recursion {any; };		(allows one DNS server to search other dns servers)
allow-query {127.0.0.1; 10.0.0.0/20;};
cli:
named-checkconf
systemctl restart named

/etc/bind/named.conf.zones
zone "8.0.0.10.in-addr.arpa" IN {
	type master
	file "db.10.0.0.8";
	allow-update{none;};
};
zone "linuxisthebest.com" IN {
	type master;
	file "/etc/bind/db.linuxisthebest.com";
	allow-update { none; };
};

db.filename.com (group owner bind and permissions 750)
$TTL 3h
@ IN SOA ns.linuxisthebest.com. franco.linuxisthebest.com. (
	1 ; Serial
	180 ; Refresh after 3 hours
	1h ; Retry after 1 hour
	1w ; Expire after 1 week
	1h ; Negative caching TTL of 1 hour
)
	IN	NS	ns.linuxisthebest.com.
4		IN	PTR	mail.linuxisthebest.com.

Serial: Incremented when the zone file changes.
Refresh: How often secondaries check for updates.
Retry: Time between retries if the last check failed.
Expire: Time before zone data is considered invalid if no response from master.
Negative caching TTL: How long to cache a failed lookup.

zone record examples:
ns 							IN	A		127.0.0.1
really.linuxisthebest.com.	IN	A		127.0.2.3
devserver 			300		IN	A		127.0.3.4 ;300 second ttl
* 							IN	NS		ns
@(current server) 			IN	MX	10 	mail.linuxisthebest.com.
mail 						IN 	A 		127.0.0.4
www     					IN  CNAME   linuxisthebest.com.
www.linuxisthebest.com to linuxisthebest.com

dig @localhost linuxisthebest.com
dig -x 10.0.0.8
nslookup google.com

named-checkzone linuxisthebest.com /etc/bind/db.linuxisthebest.com
named-checkconf /etc/bind/named.conf





**Apache and PHP**
# Block all by default
<Directory />
AllowOverride none
Require all denied
</Directory>

You have to allow individual directories:
<Directory "/var/www/html">
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
</Directory>

You can also block specific files:
<Files ".ht*">
Require all denied
</Files>

You can specify additional optional configuration files with the IncludeOptional:
IncludeOptional sites-available/*.conf

/etc/hosts:
127.0.0.1 subdomain.domain.com

<VirtualHost *:80>
ServerName example2.com
DocumentRoot /var/www/example2.com/html/# Comments with Hashes, next line is commentted out of use
#RedirectMatch permanent /(.*) https://www.example2.com/$1 #redirect to https instead of http
ErrorLog /var/log/apache2/error_log_ex2
CustomLog /var/log/apache2/access_log_ex1 common
</VirtualHost>
<VirtualHost *:80>
ServerName example1.com
DocumentRoot /var/www/example1.com/html/
ErrorLog /var/log/apache2/error_log_ex1
CustomLog /var/log/apache2/access_log_ex1 common
</VirtualHost> 
<Directory /var/www/example2.com/html/>
Require all granted
#Require ip 10.0.0.0/24
</Directory>

ErrorDocument 404 /missing.html
ErrorDocument 500 https://error.server.com/reportError.php

Alias /robots.txt /var/html/common/robots.txt

apachectl start 		Start the server
apachectl stop 			Stop the server
apachectl restart 		Restart the server
apachectl configtest 	Test the syntax of the configuration
apachectl status 		Display a brief status of the server
apachectl fullstsatus 	Display full status report from mod_status
apachectl -M			View currently active modules

a2enmod ssl
a2dismod ssl
a2ensite iaccobacci.com.conf
a2dissite iacobacci.com.conf
#/etc/apache2/mods-available
#/etc/apache2/conf-available
#/etc/apache2/conf-enabled
a2enconf security
a2disconf charset

Assignment 3:
<VirtualHost *:80>
	ServerName webserver.ca
	ServerAlias *.webserver.ca 
	VirtualDocumentRoot /home/%1/public_html
</VirtualHost>
<VirtualHost *:443>
	ServerName webserver.ca
	ServerAlias *.webserver.ca 
	VirtualDocumentRoot /home/%1/public_html
	SSLEngine on 
	#SSL certificates found in /etc/apache2/envvars
	SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
	SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
</VirtualHost>
<Directory /home/*/public_html>
	Require all granted 
</Directory>

Create /robots.txt in each DocumentRoot:
User-agent: *
Disallow: /

<?php
phpinfo();
?>
<?php echo $_SERVER["REMOTE_ADDR"]; ?>

The PHP configuration file is located in
/etc/php/{version}/{application}/php.ini
Some of the common configuration changes you might want to edit
include:
	upload directory
	global variables
	max uploading size
	max script execution time
error_reporting
	Default Value: E_ALL & ~E_NOTICE
	Development Value: E_ALL | E_STRICT
	Production Value: E_ALL & ~E_DEPRECATED
html_errors
	Default Value: On
	Development Value: On
	Production value: Off
log_errors
	Default Value: Off
	Development Value: On
	Production Value: On
display_errors
	Default Value: On
	Development Value: On
	Production Value: Off
	Example, display_errors = On
<?php
ini_set('display_errors', 1);
error_reporting(E_ALL);
?>

chown -R www-data:www-data /var/wordpress
lynx wordpress.name.com





**SSH and SFTP**
ssh php.scweb.ca 			Connect to php.scweb.ca and login as the current user on the client system
ssh root@php.scweb.ca 		Connect to php.scweb.ca login as user root
ssh -C root@php.scweb.ca 	Connect with compression enabled
ssh -p 50022 server.com 	Connect to port 50022
scp root@php.scweb.ca:~/hello.txt /tmp/ 	Copy hello.txt from the home directory of root on php.scweb.ca to /tmp on the current host
scp /etc/hosts root@php.scweb.ca:/etc/hosts Copy your local copy of /etc/hosts to php.scweb.ca /etc/hosts

sftp [user@]host
Example: sftp root@php.scweb.ca
put 	Upload a file to the server, source destination
get 	Download a file from the server
lls 	List local files
ls 		List remote files
lcd 	Change local directory
cd 		Change remote directory
lmkdir 	Make a directory locally
mkdir 	Make a directory remotely
exit 	Exit SFTP

~/.ssh/authorized_keys to add authentication keys (ssh-rsa key)
ssh-keygen [-b bits] [-t dsa | ecdsa | ed25519 | rsa] [-N new_passphrase]
ssh-keygen 														Will prompt the user for input to create SSH keys
ssh-keygen -t rsa -b 4096 -C "fiacobacci@stclaircollege.ca" 	Will create a 4096 bit RSA key, with the email specified

/etc/ssh/sshd_configfor ssh configuration
PermitRootLogin no or PermitRootLogin prohibit-password
man sshd_config
Match User franco
	AllowTcpForwarding no #disable SSH Tunnelling
Match Group students
	AllowTcpForwarding no
	XllForwarding no (GUI forwarding)
Match Address 172.22.100.0/24,172.22.5.0/24,127.0.0.1
	PermitRootLogin without-password #allow root login from specific networks
	PasswordAuthentication yes

CHROOT (don't want user to be able to create own /etc directory) jail, also make home directory user root and group user with permissions 550:
Match Group sftpusers
	ForceCommand internal-sftp #forces SFTP on login
	ChrootDirectory %h #uses the user home directory has chroot directory
	
ssh -D 2001 root@server.com 					Host a socks proxy on your local machine on port 2001 and route traffic through your SSH server
ssh -L 54000:10.13.37.2:3389 root@server.com 	Host an SSH tunnel on port 54000 locally that routes to the RDP server at the remote network at 10.13.37.2
ssh -R 54000:172.16.2.4:3389 root@server.com 	Host an SSH tunnel on port 54000 on the remote server that routes to 172.16.2.4 locally 22
ssh -p 49614 -D 1080 -n student@ml-lab-51ee3a76-1211-47fd-a193-b3ecdaa0965c.canadaeast.cloudapp.azure.com
ssh -D 1080 -C -q -N student@....com
Sometimes you may wish to allow remote hosts access to your tunnel
GatewayPorts yes

pscp -P 22 student@....com:/home/.bashrc C:/path/to/local/directory/

sshd -t





**FTP**
ftp localhost

/etc/vsftpd.conf
write_enable=YES

pasv_enable=YES
pasv_max_port=30000
pasv_min_port=30000
firewall-cmd --permanent --add-port={port chosen}/tcp

ssh -L 10021:localhost:21 -L 30000:localhost:30000 -p {port from azure} student@ml-lab-51ee3a76-1211-47fd-a193-b3ecdaa0965c.canadaeast.cloudapp.azure.com

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout vsftpd.key - out vsftpd.crt
rsa_cert_file=/etc/ssl/private/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
ssl_enable=YES
allow_anon_ssl = NO
force_local_data_ssl=YES
force_local_logins_ssl=YES

ssl_tlsv1 = YES or NO - permit tlsv1 protocol
ssl_sslv2 = YES or NO - permit ssl2 (should be disabled)
ssl_sslv3 = YES or NO - permit ssl3 (should be disabled)

/etc/ftpusers is where disallowed users are listed (generally at least includes root)
userlist_enable = YES or NO 	- whether or not to enable the user list features
userlist_deny = YES or NO 		– decide whether to only allow or deny based on the user list
userlist_file = {file} 			– where the user_list file is located

Chroot jail based on list:
chroot_local_user = NO
chroot_list_enable = YES
chroot_list_file = {file}

Active FTP: Server initiates, can cause firewall and NAT issues
Passive FTP: Client initiates

/etc/ftpusers		Blocked FTP users in vsftpd





**NFS and Samba**
/etc/exports (NFS)
/homeshare 127.0.0.1(rw,sync,subtree_check,root_squash)
/smbshare 10.0.0.8/20(rw,sync,no_subtree_check,root_squash,anonuid=1017,anongid=1010)
systemctl restart nfs

Permissions: ro = read only, rw = read write
Sychronous = sync vs async , doesn’t respond to the request until the write to the physical disk is complete. If async is enabled the response is sent but if the server or service crashes there is a risk of dataloss.
no_subtree_check = disabled confirmation that the file is actually shared, now disabling this can have some mild security concerns, however can be significantly advantageous in the event that there are a significant number of renames (default is subtree_check)
root_squash = this changes any requests made by root to an anonymous user
no_root_squash = will allow root permissions across NFS
all_squash = force all users to access through the annonymous id
anonuid and anongid = used to set annonymous user id and group id when squash is used instead of the default

sudo mount {VM IP}:/shared ~/mnt
sudo umount {mounted directory}

/etc/fstab
127.0.0.1:/homeshare /mnthome nfs
reboot
172.16.125.128:/shared /mount/shared nfs rw,users,noauto
noauto = don’t automount (counter intuitive to the title I know)
users = allow other users to mount this drive
rw = read write

symbolic link:  ln -s /mnthome/{user} /home/{user}/remoteShare

/etc/samba/smb.conf (samba)
[shared]
	comment = Shared
	read only = None
	path = /smbshare
	browsable = yes
	writable = yes
	guest ok = yes
	force user = username
systemctl restart smb

smbpasswd -a {username} - to authenticate throuugh samba server 
mount -t cifs -o username={samba user} //127.0.0.1/shared ~/smbmnt
mount -o rw 172.16.125.128:/shared /mount/shared

SELinux:
chcon -t samba_share_t {path} 	- allow samba with SELinux
restorecon -v {path} 			– reset SELinux context on your folder specified