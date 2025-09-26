
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