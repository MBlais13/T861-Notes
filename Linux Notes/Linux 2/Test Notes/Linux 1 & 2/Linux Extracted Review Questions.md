

1. Command to log in to MariaDB as root:
sudo mysql -u root -p

2. Create database MIT450:
CREATE DATABASE MIT450;

3. Switch to database:
USE MIT450;

4. Create new user 'admin':
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';

5. Grant all privileges with grant option:
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;

6. Reload privilege tables:
FLUSH PRIVILEGES;

7. View privileges for user:
SHOW GRANTS FOR 'admin'@'localhost';

8. Exit MariaDB:
EXIT;

9. Login as admin:
mariadb -u admin -p -h localhost

10. Alternate login:
sudo mysql -u admin -p

11. Confirm user:
SELECT USER();

12. Select MIT450:
USE MIT450;

13. Create students table:
CREATE TABLE students (
  student_id INT AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL
);

14. Create courses table with FK:
CREATE TABLE courses (
  course_id INT AUTO_INCREMENT PRIMARY KEY,
  course_name VARCHAR(100) NOT NULL,
  student_id INT,
  FOREIGN KEY (student_id) REFERENCES students(student_id)
);

15. Show tables:
SHOW TABLES;

16. Start MariaDB at boot:
sudo systemctl enable mariadb

17. MariaDB root login:
mysql -u root -p

18. Create user osabri:
CREATE USER 'osabri'@'localhost' IDENTIFIED BY 'password';

19. Create wwwprod DB:
CREATE DATABASE wwwprod;

20. Grant full privileges on wwwprod:
GRANT ALL PRIVILEGES ON wwwprod.* TO 'osabri'@'localhost';

21. Check privileges:
SHOW GRANTS FOR 'osabri'@'localhost';

22. Grant read-only on datawarehouse:
GRANT SELECT ON datawarehouse.* TO 'osabri'@'localhost';

23. Grant view and update:
GRANT SELECT, UPDATE ON datawarehouse.* TO 'osabri'@'localhost';

24. Create user from any IP:
CREATE USER 'employee_user'@'%' IDENTIFIED BY 'SecurePass123';

25. Meaning of '%':
Allows any IP connection.

26. User restricted to 127.0.0.1:
CREATE USER 'admin'@'127.0.0.1' IDENTIFIED BY 'admin';

28. Grant all on company_db from any IP:
GRANT ALL PRIVILEGES ON company_db.* TO 'employee_user'@'%' WITH GRANT OPTION;

29. Grant all on company_db from 127.0.0.1:
GRANT ALL PRIVILEGES ON company_db.* TO 'admin'@'127.0.0.1' WITH GRANT OPTION;

30. Login as user:
mysql -u osabri -p

31. Root login with sudo:
sudo mysql -u root -p

32. SHOW DATABASES output:
Lists available databases.

33. Login with inline password:
mysql -u osabri -p"omar1234"

34. Remote MySQL login:
mysql -u osabri -p"omar1234" --host=php.scweb.ca --port=3306

35. What is DNS?
Maps domain names to IPs.

36. Why DNS?
Humans prefer names over IPs.

37. A Record:
Maps domain to IPv4.

38. AAAA Record:
Maps domain to IPv6.

39. CNAME Record:
Domain alias.

40. MX Record:
Mail server for domain.

41. NS Record:
Identifies DNS servers.

42. PTR Record:
Reverse DNS lookup.

43. TXT Record:
Stores readable text.

44. SOA Record:
Metadata for DNS zone.

45. DNS recursion:
Server queries other servers.

46. DNS resolver:
Resolves names to IPs.

47. Primary DNS server:
Holds master zone copy.

48. Secondary DNS server:
Backup server.

49. Root DNS server:
Top-level DNS direction.

50. Domain zone:
Managed domain/IP block.

51. BIND server:
Popular Linux DNS server.

52. BIND9:
Version of BIND.

53. Check DNS config:
named-checkconf

54. Query DNS:
dig

55. Check DNS resolution:
nslookup google.com

56. IP of google.com:
dig google.com

57. Check reachability:
dig @8.8.8.8 google.com

58. Enable DNS at boot:
sudo systemctl enable bind9

59. Check BIND config syntax:
named-checkconf /etc/bind/named.conf

60. Create zone file:
sudo nano /etc/bind/db.sabrico.com

61. A record for ns:
ns.sabrico.com. IN A 192.168.1.111

62. A record for sabrico.com:
@ IN A 192.168.1.111

63. Install Apache2, PHP, etc:
sudo apt install apache2 php libapache2-mod-php php-mysql curl

64. HTML file name:
index.html

65. Enable SSL in Apache:
a2enmod ssl

66. Enable blog site:
a2ensite blog.example.com.conf

67. Reload firewall:
firewall-cmd –reload

68. View Apache modules:
sudo apachectl -M

69. Disable SSL:
sudo a2dismod ssl

70. List available modules:
ls /etc/apache2/mods-available

71. Enable example.com.conf:
sudo a2ensite example.com.conf

72. Enable PHP:
sudo a2enmod php

73. Web server to restart:
Apache

74. Alias command:
Alias /robots.txt /var/www/html/common/robots.txt

75. Apache logs:
access.log and error.log

76. WordPress setup:
sudo mkdir -p /var/wordpress/wp-content/uploads
sudo mkdir -p /var/wordpress/wp-content/cache
sudo chown -R www-data:www-data /var/wordpress/wp-content/uploads
sudo chown -R www-data:www-data /var/wordpress/wp-content/cache
sudo nano /etc/hosts
127.0.0.1 wordpress.sabrico.com
lynx wordpress.sabrico.com

77. Create SFTP user:
sudo useradd -m -s /sbin/nologin sftpuser
sudo passwd sftpuser

78. Change ownership:
sudo chown root:sftpuser /home/sftpuser
sudo chmod 750 /home/sftpuser

79. SFTP directories:
sudo mkdir /home/sftpuser/in /home/sftpuser/out /home/sftpuser/archive
sudo chown sftpuser:sftpuser /home/sftpuser/in /home/sftpuser/out /home/sftpuser/archive
sudo chmod 700 /home/sftpuser/in /home/sftpuser/out /home/sftpuser/archive

80. PSCP from Windows to Linux:
pscp -P 22 C:/test.txt osabri@sabrico.com:/home/osabri/

81. PSCP from Linux to Windows:
pscp -P 22 osabri@sabrico.com:/home/osabri/.bashrc C:/path/to/local/directory/

82. Generate SSH key:
ssh-keygen

83. Append SSH key:
cat /path/to/id_rsa.pub >> ~/.ssh/authorized_keys

84. SOCKS proxy:
ssh -D 1080 user@sabrico.com

85. Set up SFTP Chroot Jail:
sudo mkdir -p /home/user1
sudo chown root:root /home/user1
sudo chmod 755 /home/user1
sudo nano /etc/ssh/sshd_config

# Add to sshd_config:
Match User user1
    ChrootDirectory /home/user1
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no

sudo mkdir -p /home/user1/uploads
sudo chown user1:user1 /home/user1/uploads
sudo chmod 755 /home/user1/uploads
sudo systemctl restart sshd

# Optional for group:
Match Group sftpusers
    ForceCommand internal-sftp
    ChrootDirectory %h
    AllowTcpForwarding no

86. Symmetric vs Asymmetric Encryption:
Symmetric: Same key for encryption/decryption. Fast but requires secure key sharing.
Asymmetric: Uses public/private key pair. Public key encrypts, private key decrypts. Used in SSH/SSL.

87. SSH public vs private key:
Public Key: Shared, encrypts or verifies signature.
Private Key: Secret, decrypts or signs data.

88. SFTP vs SCP:
SFTP: Interactive file transfer over SSH.
SCP: Secure file copy, non-interactive.

89. SCP download file from remote:
scp root@php.scweb.ca:~/hello.txt /tmp/

90. SFTP list local files and remote tmp:
lls /tmp/

91. SFTP upload:
put ~/filename /tmp/

92. SFTP download from /tmp:
get /tmp/file.txt ~

93. Script to create user and set password:
useradd -m -s /sbin/nologin $1
echo "$1:$2" | chpasswd

94. Secure home directory:
chown root:$1 /home/$1
chmod 750 /home/$1

95. Create 3 FTP directories:
mkdir /home/$1/in /home/$1/out /home/$1/archive
chmod 755 /home/$1/in /home/$1/out /home/$1/archive
chown $1:$1 /home/$1/in /home/$1/out /home/$1/archive

96. FTP active mode uses port 21 for both channels:
False

97. FTP always uses port 21:
False

98. FTPS over plain FTP:
True

99. SFTP preferred over FTPS:
True

100. Who initiates data transfer in Active FTP?
Server

101. Why Passive FTP?
Avoids firewall/NAT issues.

102. Blocked FTP users listed in:
/etc/ftpusers

103. vsftpd config location:
/etc/vsftpd.conf

104. Samba shares defined in:
/etc/samba/smb.conf

105. Restart Samba services:
sudo systemctl restart smb nmb

106. NFS share setup script:
#!/bin/bash
sudo mkdir /homeshare
sudo useradd user1
sudo passwd user1
sudo mkdir /homeshare/user1
sudo chown user1:user1 /homeshare/user1
echo "/homeshare 127.0.0.1(rw,sync,subtree_check)" | sudo tee -a /etc/exports
sudo systemctl restart nfs-server
echo "127.0.0.1:/homeshare /mnthome nfs defaults 0 0" | sudo tee -a /etc/fstab
sudo reboot
echo "Test file content" | sudo tee /homeshare/user1/testfile.txt
sudo cat /homeshare/user1/testfile.txt

107. SELinux for Samba:
sudo chcon -t samba_share_t /smbshare
sudo restorecon -v /smbshare

108. smb.service vs nmb.service:
smb.service: File sharing
nmb.service: Network discovery, NetBIOS

109. Create Samba share with full perms:
sudo mkdir -p /smbshare
sudo chmod 777 /smbshare

110. Test Samba config:
testparm

111. Create local-only MariaDB user:
CREATE USER 'developer01'@'localhost' IDENTIFIED BY 'dev@2025';

112. Apache listen on IPs:
Listen { 127.0.0.1; 10.0.0.5; };

113. FTP listen on IPs:
listen_address=127.0.0.1
listen_address=192.168.1.25

114. Create BIND zone file:
sudo touch /etc/bind/named.conf.zones

115. DNS config for mysite.com:
zone "mysite.com" {
    type master;
    file "/etc/bind/db.mysite.com";
};

116. CNAME record:
shop.companyxyz.com. IN CNAME shop.ecommerce.com.

117. Install PHP and Apache module:
sudo apt install php php-mysql

118. Enable reverse proxy in Apache:
sudo a2enmod proxy proxy_http

119. SFTP download remote file:
get /remote/path/file.txt /local/directory/

120. SSH tunnel for RDP:
ssh -L 54000:10.13.37.2:3389 root@server.com

121. SSH tunnel for MySQL:
ssh -L 3307:192.168.2.50:3306 user@dbserver.com

122. SFTP uploads dir for user2:
sudo mkdir -p /home/user2/uploads
sudo chown user2:user2 /home/user2/uploads
sudo chmod 755 /home/user2/uploads

123. SSHD config to restrict user2:
Match User user2
    ChrootDirectory /home/user2
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no

124. Generate 4096-bit RSA key:
ssh-keygen -t rsa -b 4096 -C osabri@stclaircollege.ca

125. What is NFS?
Network File System for sharing files over a network.

126. Purpose of /etc/exports:
Defines shared directories and permissions.

127. Meaning of rw in NFS:
Read-write access.

128. root_squash in NFS:
Prevents root access from clients.

129. UID issues in NFS:
UID must match on client/server.

130. Mount NFS share:
sudo mount -o rw 172.19.135.73:/shared /mount/shared

131. Auto-mount NFS at boot:
Add entry to /etc/fstab

132. What is Samba?
SMB implementation for file/printer sharing.

133. Install Samba:
sudo apt install samba smbclient samba-common

134. Two Samba services:
smb.service (sharing), nmb.service (discovery)

135. Add user to Samba:
sudo smbpasswd -a username

136. Where are shares defined?
/etc/samba/smb.conf