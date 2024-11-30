


| Table 8-1  Common DNS resource record types |                                                                                                                                                                                          |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A (Host)                                    | Resolves an FQDN to an IPv4 address                                                                                                                                                      |
| AAAA (IPv6 Host)                            | Resolves an FQDN to an IPv6 address                                                                                                                                                      |
| CNAME (Canonical Name)                      | Also called an alias, it resolves one FQDN to another FQDN. For example, a CNAME record may be used to resolve [www.microsoft.com](http://www.microsoft.com/) to server05.microsoft.com. |
| MX (Mail Exchanger)                         | Identifies an email server for a zone                                                                                                                                                    |
| NS (Name Server)                            | Identifies a DNS server that is authoritative for a zone                                                                                                                                 |
| PTR (Pointer)                               | Resolves an IP address to an FQDN                                                                                                                                                        |
| SOA (Start of Authority)                    | Contains zone configuration information, such as zone transfer settings and the default TTL for resource records                                                                         |
| SRV (Service Location)                      | Used to identify the FQDN of a domain controller that provides Active Directory services                                                                                                 |
| WINS Lookup                                 | Used to relay forward lookup requests for a NetBIOS name to a Windows Internet Name Service (WINS) server. The configuration of WINS is discussed later in this module.                  |