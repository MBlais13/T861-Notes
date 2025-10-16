#test 
> [!info] apps for vm
> ranger - file explorer
> glow - markdown files

```
Test Content
---
Mariadb
Mariadb + replication
Nginx
Nginx + loadbalance
Docker
Bind9
Config files
```

```table-of-contents
title: **Table Of Contents:**
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 3 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

---

# Config File Locations (quick list)

- **Nginx:** `/etc/nginx/nginx.conf`, `/etc/nginx/sites-available/` → symlink to: `/etc/nginx/sites-enabled/`
- **php-fpm:** `/etc/php/<ver>/fpm/pool.d/www.conf`
- **MariaDB:** `/etc/mysql/mariadb.conf.d/50-server.cnf`
- **Bind9:** `/etc/bind/named.conf` (also `named.conf.local`), zone files in `/var/lib/bind/` (master), cache in `/var/cache/bind/`
- **Docker (data not config):** use `docker inspect` for container IP/env


---

# Nginx

## Install & Layout
```bash
sudo apt install nginx php-fpm curl ssl-cert php-mysql
sudo systemctl enable nginx
sudo systemctl start nginx
```
- Main config: `/etc/nginx/nginx.conf`
- Sites: `/etc/nginx/sites-available/` → symlink to `/etc/nginx/sites-enabled/`
- Test & reload:
```bash
sudo nginx -t
sudo systemctl reload nginx
```

## Basic vhost
Create `/etc/nginx/sites-available/example.com.conf`:
```nginx
server {
    server_name example.com;
    listen 80;
    listen [::]:80;

    root /var/vhost/com/example.com;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Enable symlink:
```bash
sudo ln -s /etc/nginx/sites-available/example.com.conf /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```
Test (without editing /etc/hosts):
```bash
curl -H "Host: example.com" http://127.0.0.1
```

## PHP-FPM
- Pool config: `/etc/php/<version>/fpm/pool.d/www.conf` (socket path)
Vhost snippet:
```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.2-fpm.sock; # verify version
}
```
Update index list when using PHP:
```nginx
index index.php index.html;
```

## SSL vhost
```nginx
server {
    server_name ssl.example.com;
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_certificate     /etc/ssl/certs/ssl-cert-snakeoil.pem;
    ssl_certificate_key /etc/ssl/private/ssl-cert-snakeoil.key;

    root /var/vhost/com/example.com;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
    }
}
```

## Reverse Proxy
```nginx
server {
    listen 80;
    server_name search.example.com;

    location / {
        proxy_set_header Host example.com;
        proxy_pass http://example.com;
    }
}
```

## Load Balancing (HTTP upstream)
Put upstream inside `http {}` (either in nginx.conf or an included file you create, then include it):
```nginx
# /etc/nginx/conf.d/upstreams.conf  (remember to: include /etc/nginx/conf.d/*.conf; in nginx.conf)
upstream dockersites {
    least_conn;
    server 127.0.0.1:8080 weight=4;
    server 127.0.0.1:58080;
}
```
Vhost proxying to upstream:
```nginx
server {
    listen 80;
    server_name lb.example.com;

    location / {
        proxy_pass http://dockersites;
        # timeouts (connection lifecycle)
        proxy_connect_timeout 5s;
        proxy_read_timeout 10s;
        proxy_send_timeout 10s;
        send_timeout 10s; # client read timeout
    }
}
```
- Change strategy examples:
  - `least_conn;`
  - `ip_hash;`
  - `hash $remote_addr$remote_port consistent;`

## Proxy
Install stream module and configure (useful for DNS/SFTP etc.):
```nginx
stream {
    upstream dnsservers {
        server 10.0.0.2:53;
        server 10.0.0.3:53;
    }
    server {
        listen 53 udp;   # udp only for UDP services
        proxy_pass dnsservers;
    }
}
```


---

# Docker

## Core commands
```bash
# images / containers
docker pull <image>
docker create [options] <image>

docker start|stop <name>
docker ps # list running
docker container ls -a # list all
docker rm <name>

docker inspect <name> # view details about container
docker exec -it <name> bash # enter container cmd
docker logs <name> # view container logs

docker cp <src> <container>:<dest> # copy to container
docker cp <container>:<src> <dest> # copy from container
```
Common options:
- `-p <host_port>:<container_port>`
- `-v <host_dir>:<container_dir>`
- `--name <name>`
- `--restart always|on-failure|unless-stopped`
- `-e KEY=VALUE`

## Docker Labs
### Lab: httpd #1 (copy in file)
```bash
docker pull httpd
echo "<h1>hello from 8080</h1>" > ~/index.html

docker create -p 8080:80 --name basichttpd --restart always httpd
docker cp ~/index.html basichttpd:/usr/local/apache2/htdocs/index.html
docker start basichttpd
curl http://127.0.0.1:8080
```

### Lab: httpd #2 (bind mount)
```bash
mkdir -p ~/public_html
echo "<h1>hello from 58080 (mounted)</h1>" > ~/public_html/index.html

docker create -p 58080:80 --name mountedhttpd --restart always \
  -v ~/public_html:/usr/local/apache2/htdocs httpd
docker start mountedhttpd
curl http://127.0.0.1:58080
```

### Lab: MariaDB in Docker
```bash
docker pull mariadb
docker create --name mariadb --restart always \
  -e MARIADB_ROOT_PASSWORD='changeme' mariadb
docker start mariadb
docker inspect mariadb | grep -i ipaddress -A2
docker exec -it mariadb mariadb -uroot -p'changeme'
```
Inside MariaDB:
```sql
CREATE DATABASE lab1;
CREATE USER 'dev1'@'%' IDENTIFIED BY 'drowssap';
GRANT ALL PRIVILEGES ON lab1.* TO 'dev1'@'%';
FLUSH PRIVILEGES;
```

### Lab: PHP app image
Folder structure:
```
~/myapp/
└─ src/index.php
└─ Dockerfile
```
`src/index.php`:
```php
<?php echo $_SERVER['REMOTE_ADDR']; ?>
```
If using `Dockerfile`:
```dockerfile
FROM php:8.4.12-apache
COPY src/ /var/www/html
```
Without Dockerfile - Build & run:
```bash
cd ~/myapp

docker pull php:apache
docker build -t myphpapp .
docker create -p 61080:80 --name phpapache --restart always myphpapp
docker start phpapache

curl http://127.0.0.1:61080
docker save myphpapp | gzip > ~/myphpapp_latest.tar.gz
```


---

# MariaDB (bare metal or inside container)

## Basics
```bash
sudo mariadb # local root
mariadb -u <user> -p"password"
mariadb -u <user> -p"password" --host=<ip> --port=3306
```
Create DB/Grants:
```sql
CREATE DATABASE mit550;

CREATE USER 'student'@'%' IDENTIFIED BY 'test1';

GRANT ALL PRIVILEGES ON mit550.* TO 'student'@'%'; /* Grant all privileges to student for the database mit416 and its tables */

GRANT SELECT ON exampledb.* to student@localhost /* Grant read privileges to student on exampledb */
FLUSH PRIVILEGES;
```
Dump/Restore:
```bash
mariadb-dump -u root -p"pass" --all-databases > alldb.sql
mariadb -u root -p"pass" < alldb.sql
```

## Replication (Master → Replica)
Primary (`/etc/mysql/mariadb.conf.d/50-server.cnf`):
```
server-id = 1
log_bin   = /var/log/mysql/mysql-bin.log
```
Restart server, then in SQL on master:
```sql
CREATE USER 'replica'@'%' IDENTIFIED BY 'reppassword';
GRANT REPLICATION SLAVE ON *.* TO 'replica'@'%';
FLUSH PRIVILEGES;
SHOW MASTER STATUS\G -- note Log File and Position
```
Replica (`50-server.cnf`):
```
server-id = 2
log_bin   = /var/log/mysql/mysql-bin.log
```
Restart replica, then in SQL on replica:
```sql
STOP SLAVE;
CHANGE MASTER TO
  MASTER_HOST='<master_ip>',
  MASTER_USER='replica',
  MASTER_PASSWORD='reppassword',
  MASTER_LOG_FILE='mysql-bin.000001',
  MASTER_LOG_POS=1187;
START SLAVE;
SHOW SLAVE STATUS\G
```
Test on master:
```sql
CREATE DATABASE lab4;
USE lab4;
CREATE TABLE students (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50), email VARCHAR(100));
INSERT INTO students VALUES (DEFAULT,'Neo','neo@matrix.io'),(DEFAULT,'Trinity','trinity@matrix.io');
```

## Replication Troubleshooting
| Issue | Check | Fix |
|-------|--------|------|
| Slave not connecting | Master IP / port | Verify Docker bridge or container IP |
| Error in position | Wrong file or position | Re-run CHANGE MASTER TO with correct values |
| Slave stopped | `Slave_IO_Running: No` | Restart slave and verify credentials |
| Duplicate entries | Manual inserts on slave | Only write to master unless using multi-source replication |


---

# Bind9 (DNS)

## Run with Docker (master+slave)
Prep host folders:
```bash
sudo mkdir -p /var/dockerdns/{master,slave}/{conf,cache,lib}
sudo chmod 777 /var/dockerdns/{master,slave}/{cache,lib}
```
Run containers (example names `dns-master`, `dns-slave`) mapping their folders to `/etc/bind` (conf), `/var/cache/bind` (cache), `/var/lib/bind` (lib) as per image docs.
```bash
docker run -d --name dns-master \
    -v /var/dockerdns/master/conf:/etc/bind \
    -v /var/dockerdns/master/lib:/var/lib/bind \
    -v /var/dockerdns/master/cache:/var/cache/bind \
     ubuntu/bind9
```
## named.conf options (master+slave)
```yaml
options {
    directory "/var/cache/bind";
    listen-on port 53 { any; };
    listen-on-v6 { any; };
    allow-query { any; };
    allow-recursion { any; };
};
```

## Master zone
`/var/dockerdns/master/conf/named.conf.local`:
```yaml
zone "test.com" {
    type master;
    file "/var/lib/bind/test.com.conf";
    notify yes;
    allow-transfer { 172.17.0.0/24; };
    also-notify { 172.17.0.3; };    # slave IP
    allow-update { 127.0.0.1; 172.17.0.1; };  # nsupdate from localhost & docker host
};
```
Zone file `/var/dockerdns/master/lib/test.com.conf`:
```conf
$TTL 86400
@ IN SOA ns.test.com. admin.test.com. (
    1      ; Serial
    180    ; Refresh (3 hours)
    1h     ; Retry
    1w     ; Expire
    1h     ; Negative TTL
)
@      IN NS ns
@      IN NS nsbkp
ns     IN A  172.17.0.2
nsbkp  IN A  172.17.0.3

; round robin example
www    IN A  127.0.0.1
www    IN A  127.0.0.2
www    IN A  127.0.0.3

; MX and a few extra A records for the lab
@      IN MX 10 mail.test.com.
mail   IN A  172.17.0.50
api    IN A  172.17.0.51
app    IN A  172.17.0.52
```

## Slave zone
`/var/dockerdns/slave/conf/named.conf.local`:
```yaml
zone "test.com" {
    type slave;
    file "test.com.conf";     # relative file (goes to cache)
    masters { 172.17.0.2; };  # master IP
};
```

## Update & admin
Dynamic add (master):
```bash
nsupdate
> server 172.17.0.2
> update add temp.test.com 600 A 127.1.1.1
> send
> quit
```
Freeze → edit file → thaw:
```bash
rndc freeze test.com
# (edit zone file, bump serial)
rndc thaw test.com   # or 'rndc reload test.com' to just reload
```
Test from host:
```bash
dig @<master_ip> test.com NS
dig @<slave_ip>  www.test.com A
dig @<master_ip> -x 127.0.0.1
```


---

# Systemd
## Basic Usage
You can use systemd tools to start and stop the apache server
- `systemctl start apache2 `- start the service now
- `systemctl enable apache2` - have the service start at system startup
- `systemctl stop apache2` - stop the service


---

# Quick Tests & Troubleshooting

- Nginx config: `sudo nginx -t`
- Service status: `systemctl status nginx mariadb`
- Logs:
  - Nginx: `/var/log/nginx/error.log`
  - MariaDB (inside container): `docker logs mariadb`
  - Bind9 (inside container): `docker logs dns-master`
- Curl loops for LB testing:
```bash
for i in {1..20}; do curl -sS http://lb.example.com/ -H "Host: lb.example.com"; echo; done
```
- Background curl (sleep test):
```bash
for i in {1..10}; do curl -sS http://sleep.example.com/ & done
```


---

# Exam Tips (based on labs)

- Use `least_conn` for the first LB test, then add `weight=4` to the 8080 server and observe distribution.
- For sleep PHP servers, set `proxy_read_timeout` to 10s (then to 40s with SSL) and note behavior.
- For MariaDB replication, always note `Log File` and `Position` from `SHOW MASTER STATUS\G` before configuring the replica.
- For Bind9, remember to **notify** and **allow-transfer** to inform the slave, and use `nsupdate` + `rndc freeze/thaw` correctly.
