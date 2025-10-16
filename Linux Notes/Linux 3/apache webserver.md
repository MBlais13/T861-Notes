
## Service Tools
You can use systemd tools to start and stop the apache server
- `systemctl start apache2 `- start the service now
- `systemctl enable apache2` - have the service start at system startup
- `systemctl stop apache2` - stop the service
- `systemctl restart apache2` - restart the service
- `systemctl reload apache2` - reload is supported by apache2, this will reload the configuration without stopping the server

apachectl
use systemd to manage the service, only use apachectl for configtest, status, fullstatus
	- ⁠`apachectl start` - Start the server
	- `apachectl stop` - Stop the server
	- `apachectl restart` - Restart the server

- `apachectl configtest` - Test the syntax of the configuration
- `apachectl status` - Display a brief status of the server
- `apachectl fullstatus` - Display full status report from ⁠mod_status

## v-hosts
Apache on debian also comes with its own tool for enabling/disabling sites(vhosts):

- `a2ensite site.com.conf`
	Enable the iacobacci.com.conf site on apache2 by creating symlinks from sites-available in sites-enabled

- `a2dissite site.com.conf`
	Disable the iacobacci.com.conf module on apache2 by removing symlinks from sites-enabled

## SSL/TLS
enable SSL module: `a2enmod ssl`
set a certificate
```
SSLCertificateFile     /etc/letsencrypt/site.com/fullchain.pem
SSLCertificateKeyFile  /etc/letsencrypt/site.com/privkey.pem
```

## Error page
specify an error page by `ErrorDocument {error code} {action/location}`

## Aliases
set alias paths for certain files
`Alias /robots.txt /var/html/common/robots.txt`

```
<VirtualHost *:80>
	ServerName java.example.com
	ProxyPreserveHost On
	ProxyPass / http://127.0.0.1:50080/
	ProxyPassReverse / http://127.0.0.1:50080/
</VirtualHost>
```





---


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
