#tags

> [!info] Commands
> [[Cisco Commands#Passwords & Security]]

Description
http://password-decrypt.com

---
## Heading
###
```
Switch(config)#enable secret ?
  0      Specifies an UNENCRYPTED password will follow
  5      Specifies a MD5 HASHED secret will follow
  8      Specifies a PBKDF2 HASHED secret will follow
  9      Specifies a SCRYPT HASHED secret will follow
  LINE   The UNENCRYPTED (cleartext) 'enable' secret
  level  Set exec level password
```
### Set username & password login
 `login local` command tells the switch to refer to a local database of usernames and passwords for authentication.
 
After using the commands here: [[Cisco Commands#Set username & password]], this is the result:
```
Press RETURN to get started.

User Access Verification

Username: admin
Password: 
Switch>
```