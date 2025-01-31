
Link aggregation - bundling multiple links: such as combining two different ethernet connections to act as one.  

- Slight performance decrease over raw paper performance
- This form of load balancing works by increasing the performance for multiple clients

Example of client speeds: Two 1000 mbp/s LACP links]

| # of Clients  | Without LACP | With LACP = link1 - link2 |
| ------------- | ------------ | ------------------------- |
| One Client    | 1000mbp/s    | 1000mbp/s - 0mbp/s        |
| Two Clients   | 500mbp/s     | 1000mbp/s - 1000mbp/s     |
| Three Clients | 333mbp/s     | 1000mbp/s - 500mbp/s      |
| Four Clients  | 250mbp/s     | 500mbp/s - 500mbp/s       |

Having three clients connected through two LACP links might have awkward performance. Since it likes to put one client per link instead of splitting the client onto multiple links.

TLDR;
LAG will only increase your bandwidth if you're performing simultaneous transfers to/from different clients (or multiple NICs on a single PC).  A single connection from a single NIC will only use one path to the NAS regardless of how many NICs are teamed on the NAS or how fast the client NIC is - that's just how it works.


|                                      | **SMB3 Multichannel**                                                                                                                                                   | **Link Aggregation**                                                                                                                                  |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Usage scenario**                   | For enhancing the performance of SMB for a single client                                                                                                                | For environments with multiple users and devices                                                                                                      |
| **Hardware requirements**            | The client and the server both require [multiple network adapters](https://kb.synology.com/en-nz/DSM/tutorial/smb3_multichannel_link_aggregation#x_anchor_id2dcad7a778) | The client and the server both require multiple network adapters                                                                                      |
| **Applicable services/applications** | SMB Service                                                                                                                                                             | All applications                                                                                                                                      |
| **Throughput enhancement**           | - Enhances server throughput for SMB Service<br>- Enhances single client throughput for SMB Service                                                                     | - Enhances server overall throughput<br>- Does not enhance single client throughput                                                                   |
| **Network fault tolerance**          | Supported with multiple network adapters                                                                                                                                | Supported                                                                                                                                             |

# Etherchannel
Fast ethernet ports cannot be mixed with gigabit ethernet ports.

when enabled Pag-P ensures connection.
