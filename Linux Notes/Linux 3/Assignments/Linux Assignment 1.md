
doc_name: 0844719_michaelblais.docx

- qaapp.company.com root subdomain proxies to port 8085 on three servers.
- The numbered ones use the port in the childs subdomain and forward traffic to the same 3 servers.
## Config
```lua
upstream qaapp_base {
		server 10.34.37.2:8085;
		server 10.34.36.2:8085;
		server 10.34.35.2:8085;
	}
	server {
		listen 80;
		server_name qaapp.company.con;
		location / {
		proxy_pass http://qaapp_base;
	}
}
```

```lua
server {
	listen 80;
	server_name ~^(?\d{2,5})\.qaapp\.company\.com$;
	location / {
		proxy_pass http://10.34.37.2:$port;
		proxy_pass http://10.34.36.2:$port
		proxy_pass http://10.34.35.2:$port;
	}
}
```

## Hate Regex:
```
server_name ~^(?<port>\d{2,5})\.qaapp\.company\.com$;
\d - digit
{2,5} - between 2 & 5
^ start of string
\. escape the any character shit
```

So i in conclusion it'l extract subdomain port such as 9085 and route it to the backend server of the servers IP address
## Reference Links
• NGINX load balancing: https://nginx.org/en/docs/http/load_balancing.html
• Proxy module: https://nginx.org/en/docs/http/ngx_http_proxy_module.html

For the 'future administrators': Quit while you can.