#cisco #iOS
#tags

> [!warning] Old Notes
> [[Cisco Commands#tag]]

Description

---
## Heading
### Sub Heading


> [!warning] Old Notes
### Check SSH support
If SSH is unsupported the command will be unknown.
```
S1# show ip ssh
```
### Configure IP domain
```
S1# conf term
S1(config)# ip domain-name cisco.com
```
### Generate RSA key pairs
```
S1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
```
### Configure user authentication
```
S1(config)# username admin secret Passw0rd
```
### Configure VTY lines
The catalyst 2960 has only 0-15 VTY lines. This prevents non SSH connections.
The login local command uses the username and password database.
```
S1(config)# line vty 0 15
S1(config-line)# transport input ssh
S1(config-line)# login local
S1(config-line)# exit
```
### Enable SSH
```
S1(config)# ip ssh version 2
```

### Check SSH connections
```
S1# show ssh
%No SSHv1 server connections running.
Connection Version Mode Encryption  Hmac               State          Username

0          2.0     IN   aes256-cbc  hmac-sha1    Session started       admin

0          2.0     OUT  aes256-cbc  hmac-sha1    Session started       admin
```
