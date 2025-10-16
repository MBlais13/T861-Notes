w0844719_michaelb.docx

Student ID: w0844719
Name: Michael Blais

---

## 1. Virtual host

```xml
<VirtualHost *:80>
    ServerName webserver.ca
    ServerAlias *.webserver.ca
    VirtualDocumentRoot /home/%1/public_html

    <Directory /home/*/public_html>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

`mod_vhost_alias` dynamically maps requests for `username.webserver.ca` to the users public_html dir
- `ServerAlias *.webserver.ca` = subdomain wildcard
- `VirtualDocumentRoot /home/%1/public_html` = Maps to `/home/username/public_html`
- `%1` = placeholder for the subdomain
- `public_html` = allow access to the directories

---

## 2. Reverse proxy for scweb.blais.com

```xml
<VirtualHost *:80>
    ServerName scweb.blais.com

    ProxyPreserveHost On
    ProxyPass / http://scweb.ca/
    ProxyPassReverse / http://scweb.ca/
</VirtualHost>
```

This enbles a reverse proxy to forward requests made to `scweb.blais.com` to `http://scweb.ca`
- `ProxyPass` and `ProxyPassReverse` handle forwarding and responses
- `ProxyPreserveHost On` makes sure the original host header is kept

---

## 3. Reverse proxy for node.blais.com

```xml
<VirtualHost *:80>
    ServerName node.blais.com

    ProxyPreserveHost On
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/
</VirtualHost>
```


Forwards requests to `node.blais.com` to a locally running service on port 3000
- `ProxyPass` and `ProxyPassReverse` make sure requests are routed properlu


