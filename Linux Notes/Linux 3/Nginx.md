

## Install and Basic Config
### Basic Setup
```bash
apt install nginx php-fpm curl ssl-cert php-mysql
```

```bash
systemctl enable nginx
systemctl start nginx
```

Default config files:
- Main config: `/etc/nginx/nginx.conf`
- Sites available: `/etc/nginx/sites-available`
- Sites enabled: `/etc/nginx/sites-enabled'

To enable a site: (creates linked file)
```bash
ln -s /etc/nginx/sites-available/sitename /etc/nginx/sites-enabled/
```

Reload to apply changes:
```bash
systemctl reload nginx
```

### Docker Nginx

```bash
docker pull nginx
docker create --name nginx-lb -p 80:80 nginx
docker cp ./nginx.conf nginx-lb:/etc/nginx/nginx.conf
docker start nginx-lb
docker exec -it nginx-lb bash
```

---

## nginx vs Apache
- **Apache:** creates a new process for each request  
  → easy but uses more resources  
- **nginx:** single-process event-driven model  
  → handles more requests efficiently (better for reverse proxying)  
- **nginx** must be configured to use all cores (`worker_processes auto;`)

---

## Creating a Virtual Host
Example file: `/etc/nginx/sites-available/example.com`
- (enable with symlink to `/etc/nginx/sites-enabled/example.com`)`
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

Create and enable the site:
```bash
ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
systemctl reload nginx
```

Test:
```bash
curl -H "Host: example.com" 127.0.0.1 
```

---

## PHP with nginx
Install `PHP-FPM` and connect via socket.

`/etc/nginx/sites-available/search.example.com`
```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.2-fpm.sock;
}
```

Example index file:
```php
<?php
echo $_SERVER['REMOTE_ADDR'];
?>
```

---

## SSL Virtual Host
1. Create subdomain: `ssl.example.com`
2. Use a self-signed certificate (`ssl-cert` package)

- Cert paths in the example:
	- /etc/ssl/certs/ssl-cert-snakeoil.pem and
	- /etc/ssl/private/ssl-cert-snakeoil.key

`/etc/nginx/sites-available/ssl.example.com`
```nginx
server {
    server_name ssl.example.com;
    listen 443 ssl;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_certificate /etc/ssl/certs/ssl-cert-snakeoil.pem;
    ssl_certificate_key /etc/ssl/private/ssl-cert-snakeoil.key;

    root /var/vhost/com/example.com;
    index index.php index.html;

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
    }
}
```

---

## Reverse Proxy
`/etc/nginx/sites-available/search.example.com`
```nginx
server {
    server_name search.example.com;
    listen 80;

    location / {
        proxy_set_header Host google.com;
        proxy_pass http://google.com;
    }
}
```

---

## Load Balancing (Upstream)
Define your backend servers in an `upstream` block:
`/etc/nginx/sites-available/myloadbalancer.com`
```nginx
upstream dockersites {
    least_conn;
    server 10.0.0.2:8080;
    server 10.0.0.3:8080;
}
```

Reverse proxy to the upstream:
```nginx
server {
    listen 80;
    server_name myloadbalancer.com;

    location / {
        proxy_pass http://dockersites;
    }
}
```

---

## Load Balancing Methods
- `round-robin` – default  
- `least_conn` – least active connections  
- `ip_hash` – sends same client to same backend  
- `weight` – prioritize one server more

Example with weights:
```nginx
upstream dockersites {
    server 10.0.0.2:8080 weight=4;
    server 10.0.0.3:8080;
}
```

---

## Timeouts
```nginx
proxy_connect_timeout 10s;
proxy_read_timeout 30s;
proxy_send_timeout 30s;
send_timeout 15s;
```
- `proxy_connect_timeout` – how long to connect to the server
- `proxy_read_timeout` – wait for response
- `proxy_send_timeout` – how long to send data
- `send_timeout` – client reading timeout

---

## Testing and Troubleshooting
```bash
nginx -t        # Test config syntax
systemctl reload nginx
docker ps        # Check running containers
curl -I domain.com
```

Common logs:
```
/var/log/nginx/access.log
/var/log/nginx/error.log
```

---

## Proxy Streams (for TCP/UDP)
```nginx
stream {
    upstream dnsservers {
        server 10.0.0.2:53;
        server 10.0.0.3:53;
    }

    server {
        listen 53 udp;
        proxy_pass dnsservers;
    }
}
```

---

## Testing Load Balancer
```bash
for i in {1..10}; do curl -s myloadbalancer.com | grep Server; done
```
> You’ll see requests alternating between servers.


---

## Summary of Key Commands
| Task              | Command                                                           |
| ----------------- | ----------------------------------------------------------------- |
| Test config       | `nginx -t`                                                        |
| Reload service    | `systemctl reload nginx`                                          |
| View container IP | `docker inspect nginx-lb`                                         |
| Check site        | `curl -H "Host: domain.com" 127.0.0.1`                            |
| Enable site       | `ln -s /etc/nginx/sites-available/site /etc/nginx/sites-enabled/` |
