#tags

> [!info] Commands
> [[Cisco Commands#Remote Connection]]

Description

---
## VTY lines
Your router or switch will have a certain amount of VTY lines. These are virtual terminal lines that define how many concurrent connections it supports.
```
R1(config)# line vty 0 ?
  <1-924>  Last Line number
```
This router supports more than 900 VTY lines which is a shit ton. Smaller boxes will typically have 8 or 16 VTY lines.

## SSH

#### Positives and Negatives
**-- Positives**
+ Requires a username and password
+ Username and password can be authenticated locally
**-- Negatives**
- Accounts must be configured locally on each device.
- No fallback authentication method.

## Telnet (Discouraged)
> [!warning] Should not be used as it is unencrypted.
> Telnet is not covered due to it being outdated and highly discouraged.

Because I like doing things I'm not supposed to, I'll show you anyway.

- Telnet sends everything in plain text so it is not secure. It’s better to use SSH instead.
- If you use telnet, it’s best to use an access-list to restrict what devices are allowed to connect.
### Telnet Setup
```
S1(config)#line vty 0 4
S1(config-line)#transport input ?
  all      All protocols
  lapb-ta  LAPB Terminal Adapter
  lat      DEC LAT protocol
  mop      DEC MOP Remote Console Protocol
  none     No protocols
  pad      X.3 PAD
  rlogin   Unix rlogin protocol
  **ssh      TCP/IP SSH protocol**
  **telnet   TCP/IP Telnet protocol**
  udptn    UDPTN async via UDP protocol
  v120     Async over ISDN
```

Now lets turn on telnet
```
S1(config-line)# transport input telnet
S1(config-line)# password my_password
S1(config-line)# login
```
![[Pasted image 20241014011823.png]]
Above is a giant middle finger if you actually followed through with enabling telnet :)

### Telnet Client
With all being said about the server, there are some (useful) things you can accomplish with the telnet client.

**Remember plaintext is still plaintext**
```
R2#telnet 192.168.1.1 ?
  /debug             Enable telnet debugging mode
  /ipv4              Force use of IP version 4
  /ipv6              Force use of IP version 6
  /line              Enable telnet line mode
  /noecho            Disable local echo
  /quiet             Suppress login/logout messages
  /route:            Enable telnet source route mode
  /source-interface  Specify source interface
  /stream            Enable stream processing
  /terminal-type     Set terminal type
  <0-65535>          Port number
  bgp                Border Gateway Protocol (179)
  chargen            Character generator (19)
  cmd                Remote commands (rcmd, 514)
  daytime            Daytime (13)
  discard            Discard (9)
  domain             Domain Name Service (53)
  drip               Dynamic Routing Information Protocol (3949)
  echo               Echo (7)
  exec               Exec (rsh, 512)
  finger             Finger (79)
  ftp                File Transfer Protocol (21)
  ftp-data           FTP data connections (20)
  gopher             Gopher (70)
  hostname           NIC hostname server (101)
  ident              Ident Protocol (113)
  irc                Internet Relay Chat (194)
  klogin             Kerberos login (543)
  kshell             Kerberos shell (544)
  login              Login (rlogin, 513)
  lpd                Printer service (515)
  nntp               Network News Transport Protocol (119)
  onep-plain         ONEP Cleartext (15001)
  onep-tls           ONEP TLS (15002)
  pim-auto-rp        PIM Auto-RP (496)
  pop2               Post Office Protocol v2 (109)
  pop3               Post Office Protocol v3 (110)
  smtp               Simple Mail Transport Protocol (25)
  sunrpc             Sun Remote Procedure Call (111)
  tacacs             TAC Access Control System (49)
  talk               Talk (517)
  telnet             Telnet (23)
  time               Time (37)
  uucp               Unix-to-Unix Copy Program (540)
  whois              Nicname (43)
  www                World Wide Web (HTTP, 80)
```
PSA: some of these may be possible with SSH, I've never tried.