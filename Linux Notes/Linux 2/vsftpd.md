
- `/etc/ftpusers` is where disallowed users are listed

> [!INFO] !
> `!` to run local commands while in ftp


`/etc/vsftpd.userlist`

#### CONF
- `userlist_enable`
- `userlist_deny`
- `userlist_file`

#### chrooting
- `chroot_local_user` = chroot jail a local user
- `chroot_list_user`


#### Passive mode
`pasv_enable`
`pasv_max_port`
`pasv_min_port`

## Using SSL with FTP
Generate ssl cert:
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout vsftpd.key -out vsftpd.crt
```

Public Key Location:
`rsa_cert_file` = /etc/ssl/private/vsftpd.crt
Private Key Location:
`rsa_private_key_file` = /etc/ssl/private/vsftpd.key

#### vsftpd Security
`ssl_enable` = enable SSL
`allow_anon_ssl` = allow anonymous users to use ssl?
`force_local_data_ssl` = force SSL on data connection
`force_local_logins_ssl` = force SSL on command connection

`ssl_tlsv1` = permit tlsv1 protocol
`ssl_tlsv2` = should be disabled
`ssl_tlsv3` = should be disabled

