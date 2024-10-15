#test

| port group              | number range   | description                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| well-known ports        | 0 - 1,023      | •These port numbers are reserved for common or popular services and applications such as web browsers, email clients, and remote access clients.<br><br>•Defined well-known ports for common server applications enables clients to easily identify the associated service required.                                                                                                            |
| registered ports        | 1024 - 49,151  | •These port numbers are assigned by IANA to a requesting entity to use with specific processes or applications.<br><br>•These processes are primarily individual applications that a user has chosen to install, rather than common applications that would receive a well-known port number.<br><br>•For example, Cisco has registered port 1812 for its RADIUS server authentication process. |
| private / dynamic ports | 49152 - 65,353 | •These ports are also known as ephemeral ports.<br><br>•The client’s OS usually assign port numbers dynamically when a connection to a service is initiated.<br><br>•The dynamic port is then used to identify the client application during communication.                                                                                                                                     |



to-know port numbers for the CCNA-200-301 test

| Port number | Protocol | Application   |
| ----------- | -------- | ------------- |
| 20          | TCP      | FTP - data    |
| 21          | TCP      | FTP - control |
| 22          | TCP      | SSH           |
| 23          | TCP      | Telnet        |
| 25          | TCP      | SMTP          |
| 53          | UDP, TCP | DNS           |
| 67          | UDP      | DHCP - server |
| 68          | UDP      | client        |
| 69          | UDP      | TFTP          |
| 80          | TCP      | HTTP          |
| 110         | TCP      | POP3          |
| 143         | TCP      | IMAP          |
| 161         | UDP      | SNMP          |
| 443         | TCP      | HTTPS         |

