

# CCNA 3: Enterprise Networking, Security, and Automation - Study Sheet

## 1. Network Design

- **Failure Domains**: Minimize using switch blocks, redundant paths, and collapsed core.
- **Three-tier Architecture**: Core, Distribution, Access layers for scalability and performance.
- **Converged Networks**: Single infrastructure for voice, video, and data.

## 2. Routing Protocols

### OSPF (Open Shortest Path First)
- **Single-Area OSPF**: All routers in Area 0.
- **Hello Packet**: Establishes neighbor adjacency.
- **Types of LSAs**:
  - Type 1: Router LSA
  - Type 2: Network LSA
  - Type 3: Summary LSA

### EIGRP
- Uses Diffusing Update Algorithm (DUAL).
- Supports VLSM and CIDR.
- Reliable transport via RTP.

## 3. WAN Technologies

- **Types**:
  - **MPLS**: Label-based, fast switching, scalable.
  - **DSL**: Uses copper lines, asymmetric speeds.
  - **Metro Ethernet**: Dedicated high-speed links in metropolitan areas.
- **VPNs**:
  - **Remote Access VPN**: Users connect from remote locations using VPN client software.
  - **Site-to-Site VPN**: Persistent connection between offices.

## 4. Network Security

- **Viruses**: Require activation, payloads vary.
- **Trojan Horses**: Appear benign, often open backdoors.
- **Worms**: Self-replicating, spread over networks.
- **Security Devices**:
  - Firewalls
  - IPS/IDS
  - AAA Servers (Authentication, Authorization, Accounting)
- **ACLs**: Filter traffic by source/destination IP, port, protocol.

## 5. Device Management

- **Password Recovery**:
  - Change `configuration register` (e.g., to 0x2142).
  - Access `startup-config` from NVRAM after reboot.
- **Syslog**: Collect and store logs.
- **NTP**: Synchronizes device time.
- **SNMP**: Monitor and manage devices using MIBs.

## 6. Automation and Virtualization

- **Cisco DNA Center**: Network management via controller-based architecture.
- **Software Defined Networking (SDN)**:
  - Control plane separated from data plane.
  - Centralized management.
- **APIs**:
  - RESTful APIs using HTTP methods (GET, POST, PUT, DELETE).
- **JSON/YAML**: Used for configuration automation.

## 7. IPv4/IPv6 Concepts

- **Private IP Address Ranges**:
  - Class A: 10.0.0.0/8
  - Class B: 172.16.0.0/12
  - Class C: 192.168.0.0/16
- **NAT**: Conserves public IPs, hides internal addresses.
- **Dual Stack**: Devices run both IPv4 and IPv6.
- **Tunneling**: IPv6 packets inside IPv4 (6to4, ISATAP).
- **IPv6 Address Types**:
  - Global Unicast
  - Link-local
  - Multicast

## 8. Cloud Computing

- **Benefits**:
  - On-demand resources.
  - Reduced need for onsite hardware.
  - Access from anywhere.
- **Deployment Models**:
  - Private, Public, Hybrid, Community.
- **Services**:
  - IaaS, PaaS, SaaS.

## 9. Disaster Recovery and Virtualization

- **Virtualization**: Run multiple OSes on one host.
- **Hypervisors**:
  - Type 1: Bare metal (e.g., ESXi).
  - Type 2: Hosted (e.g., VirtualBox).
- **Data Center**: Supports redundancy, high availability.

---

## Notes

- OSPF neighbor states and LSA types.
- Interpreting NAT tables.
- CLI syntax and troubleshooting.
- Review automation concepts

