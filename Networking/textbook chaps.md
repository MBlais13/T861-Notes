
## 1. Network Design
### 1.1. Hierarchical Network Design
**Three Layers:**
- **Access Layer**: Connects end devices like PCs, printers, and phones to the network. It's the "edge" of the network.
- **Distribution Layer**: Connects access layer switches to core routers. Performs routing, filtering, and policy-based network control.
- **Core Layer**: Backbone of the network. Provides high-speed and reliable data transport.
**Why it matters**:
- Easier troubleshooting
- Scalable design (you can grow without redesigning everything)
- Better performance and security (segmentation, policies)

---
### 1.2. Redundancy and Failure Domains
**Redundancy** means having backup links or devices in case something fails.
**Failure Domain**: Part of the network impacted by a failure (like a broken switch or router). We design networks to keep failure domains small.
**Example**:
- If a switch at the access layer dies, only a few users lose connection — not the entire network.
**Redundancy Methods**:
- Dual power supplies
- Backup connections between switches
- FHRP protocols like HSRP/VRRP

---
### 1.3. Converged Networks
A **converged network** supports voice, video, and data on the same physical infrastructure.
**Why it matters**:
- Cost-effective (no need for separate networks)
- Requires QoS (Quality of Service) to prioritize delay-sensitive traffic like voice or video

---
### 1.4. Collapsed Core Design
In smaller networks, the **distribution and core layers** can be combined into a single layer — this is called a **collapsed core**.
**Benefits**:
- Cheaper and simpler for small businesses
- Still supports some scalability and redundancy

---
### 1.5. Cisco Enterprise Architecture Modules
Cisco breaks down networks into modules to organize different network functions. Key modules include:
- **Enterprise Campus**: Access, distribution, and core layers
- **Enterprise Edge**: Connects the network to the Internet, VPNs, and cloud
- **Data Center**: Where servers and services live
- **Service Provider Edge**: Interfaces with ISPs
- **Remote Access and Branch**: Supports remote users/sites

---
## 2. Routing Protocols
### 2.1. Static vs. Dynamic Routing
**Static Routing**:
- Manually configured by an admin (`ip route` command)
- No overhead from routing protocols
- Best for small or simple networks
**Pros**:
- Secure (not advertised over network)
- Predictable (no route changes unless you do it)
**Cons**:
- Doesn’t adapt to network changes
- Hard to manage in large networks
**Dynamic Routing**:
- Routers share routing information with each other automatically
- Examples: OSPF, EIGRP, RIP
**Pros**:
- Automatically adjusts to changes
- Scales well
**Cons**:
- Uses bandwidth and CPU
- More complex to configure and troubleshoot

---
### 2.2. OSPF (Open Shortest Path First)
**Type**: Link-State protocol  
**Metric**: Cost (based on bandwidth; lower cost = better path)  
**Administrative Distance (AD)**: 110  
**Algorithm**: Dijkstra SPF (Shortest Path First)
**Single Area OSPF**:
- All routers are in Area 0 (backbone area)
- Simpler to manage in small/medium networks
**OSPF Terms**:
- **Router ID (RID)**: 32-bit ID used to identify OSPF router; highest IP or manually set
- **Hello packets**: Sent every 10 seconds to discover/maintain neighbors
- **Dead Interval**: 40 seconds (default) — if no Hello in this time, neighbor is down
- **DR/BDR**: On multiaccess networks (like Ethernet), OSPF elects a **Designated Router** and **Backup DR** to reduce LSA traffic
**Neighbor Adjacency Process** (states):
1. Down
2. Init
3. Two-Way
4. ExStart
5. Exchange
6. Loading
7. Full
**LSA Types**:
- Type 1: Router LSA (info about directly connected networks)
- Type 2: Network LSA (sent by DRs)
- Type 3: Summary LSA (between areas)
**Useful OSPF Commands**:
```bash
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
show ip ospf neighbor
show ip ospf interface
```

---
### 2.3. EIGRP (Enhanced Interior Gateway Routing Protocol)
**Type**: Advanced Distance-Vector (Cisco proprietary)  
**Metric**: Composite (bandwidth + delay, reliability, load)  
**Administrative Distance**: 90 (internal), 170 (external)  
**Algorithm**: DUAL (Diffusing Update Algorithm)
**DUAL Concepts**:
- **Successor**: Best route
- **Feasible Successor**: Backup route (no loop)
- **Feasible Distance (FD)**: Metric of the best path
- **Reported Distance (RD)**: Neighbor's distance to the destination
**EIGRP Hello/Dead Times**:
- Hello: 5 sec (default)
- Hold: 15 sec (default)
**EIGRP Characteristics**:
- Partial, bounded updates (only changes are sent)
- Uses RTP (Reliable Transport Protocol) for delivery
**Useful EIGRP Commands**:
```c
router eigrp 100
 network 10.0.0.0
show ip route eigrp
show ip eigrp neighbors
```

---
### 2.4. Route Summarization
Combines multiple routes into one to reduce routing table size.
**Manual Summarization**:
- Done in EIGRP or static routes
**Automatic Summarization**:
- Legacy behavior in older EIGRP versions (now disabled by default)

---
### 2.5. Administrative Distance (AD)
Used to decide which routing protocol to trust when multiple routes exist.

| Route Source       | AD Value |
|--------------------|----------|
| Directly Connected | 0        |
| Static             | 1        |
| EIGRP (internal)   | 90       |
| OSPF               | 110      |
| RIP                | 120      |
| EIGRP (external)   | 170      |

---
## 3. WAN Technologies
### 3.1. What is a WAN?
A **Wide Area Network (WAN)** connects devices across large geographical areas, enabling communication between remote locations. Unlike LANs, which are confined to a single building or campus, WANs span cities, countries, or even continents.
**Key Characteristics**:
- **Ownership**: Typically leased from service providers.
- **Speed**: Generally slower than LANs due to longer distances and shared infrastructure.
- **Cost**: Higher operational costs compared to LANs.
- **Technology**: Utilizes various transmission technologies like MPLS, DSL, and Metro Ethernet.

---
### 3.2. WAN Connection Types
#### 3.2.1. Leased Lines (Point-to-Point)
- **Description**: Dedicated physical connection between two sites.
- **Speed**: Offers consistent bandwidth.
- **Use Case**: Ideal for constant, high-volume traffic between two locations.
- **Pros**: High reliability and security.
- **Cons**: Expensive due to dedicated nature.
#### 3.2.2. DSL (Digital Subscriber Line)
- **Description**: Transmits data over traditional telephone lines.
- **Types**:
  - **ADSL**: Asymmetric speeds; faster download than upload.
  - **SDSL**: Symmetric speeds; equal download and upload rates.
- **Use Case**: Suitable for small businesses and residential users.
- **Pros**: Widely available and cost-effective.
- **Cons**: Distance-sensitive; performance degrades with distance from the provider's central office.
#### 3.2.3. Cable Broadband
- **Description**: Uses coaxial cables to deliver internet services.
- **Use Case**: Common in residential areas.
- **Pros**: Higher speeds than DSL.
- **Cons**: Shared bandwidth can lead to congestion during peak times.
#### 3.2.4. Metro Ethernet
- **Description**: Extends Ethernet services over a metropolitan area.
- **Use Case**: Connects multiple sites within a city.
- **Pros**: Scalable and integrates easily with existing LANs.
- **Cons**: Availability may be limited to urban areas.
#### 3.2.5. MPLS (Multiprotocol Label Switching)
- **Description**: Directs data from one node to the next based on short path labels rather than long network addresses.
- **Use Case**: Preferred for enterprise networks requiring QoS.
- **Pros**: Efficient routing and supports multiple protocols.
- **Cons**: More complex and potentially costly.
#### 3.2.6. Satellite
- **Description**: Provides internet access via satellite communication.
- **Use Case**: Remote or rural areas lacking terrestrial infrastructure.
- **Pros**: Wide coverage area.
- **Cons**: High latency and weather-dependent reliability.

---
### 3.3. VPN (Virtual Private Network)
A **VPN** creates a secure, encrypted connection over a less secure network, such as the internet.
#### Types of VPNs:
- **Site-to-Site VPN**:
  - **Description**: Connects entire networks to each other.
  - **Use Case**: Linking branch offices to a central office.
  - **Pros**: Seamless integration between sites.
  - **Cons**: Requires dedicated VPN hardware or routers.
- **Remote Access VPN**:
  - **Description**: Allows individual users to connect to a network remotely.
  - **Use Case**: Telecommuting employees accessing corporate resources.
  - **Pros**: Flexibility for remote workers.
  - **Cons**: May require client software and proper configuration.

---
### 3.4. WAN Devices
- **Modem**: Converts digital signals to analog for transmission over telephone lines.
- **DSL Modem**: Specifically designed for DSL connections.
- **Cable Modem**: Used for cable internet services.
- **CSU/DSU (Channel Service Unit/Data Service Unit)**: Connects a digital line to a router.
- **Router**: Directs data packets between networks.
- **VPN Concentrator**: Manages VPN connections and security.

---
### 3.5. WAN Topologies
- **Point-to-Point**:
  - **Description**: Direct connection between two nodes.
  - **Use Case**: Simple, dedicated links.
  - **Pros**: High performance and security.
  - **Cons**: Not scalable for multiple sites.
- **Hub-and-Spoke**:
  - **Description**: Central hub connects to multiple spokes.
  - **Use Case**: Centralized networks.
  - **Pros**: Simplified management.
  - **Cons**: Hub becomes a single point of failure.
- **Full Mesh**:
  - **Description**: Every node connects to every other node.
  - **Use Case**: High availability requirements.
  - **Pros**: Redundant paths increase reliability.
  - **Cons**: Complex and costly to implement.

---
### 3.6. WAN Encapsulation Protocols
- **PPP (Point-to-Point Protocol)**:
  - **Description**: Encapsulates network layer protocol information over point-to-point links.
  - **Features**: Authentication, compression, error detection.
- **HDLC (High-Level Data Link Control)**:
  - **Description**: Cisco's default encapsulation on serial interfaces.
  - **Features**: Simple and efficient for point-to-point links.

---
### 3.7. Quality of Service (QoS)
**QoS** refers to mechanisms that control traffic prioritization to ensure the performance of critical applications.
- **Traffic Classification**: Identifying and categorizing traffic types.
- **Traffic Shaping**: Controlling the volume of traffic being sent into the network.
- **Congestion Management**: Prioritizing packets during congestion.
- **Congestion Avoidance**: Preventing congestion through proactive measures.

---
### 3.8. WAN Troubleshooting Commands
- `show ip interface brief`: Displays interface status and IP addresses.
- `show interfaces`: Provides detailed interface statistics.
- `show controllers`: Displays hardware-related information.
- `ping`: Tests connectivity to a specific IP address.
- `traceroute`: Traces the path packets take to a destination.

---
## 4. Network Security
### 4.1. Security Threats
**Types of Threats**:
- **Malware**: Malicious software (viruses, worms, trojans, spyware).
- **Phishing**: Fraudulent attempt to obtain sensitive info via fake communication.
- **Denial of Service (DoS)**: Floods a network to overwhelm it and make it unavailable.
- **Man-in-the-Middle (MITM)**: Attacker intercepts and possibly alters communications between two parties.
- **Spoofing**: Pretending to be someone else (e.g., IP spoofing, MAC spoofing).
**Attack Types**:
- **Reconnaissance**: Information gathering (e.g., scanning, sniffing).
- **Access Attacks**: Gaining unauthorized access (e.g., password cracking).
- **DoS/DDoS Attacks**: Disrupting services.

---
### 4.2. Security Policies
**Components of a Security Policy**:
- **Acceptable Use Policy (AUP)**: Defines acceptable employee behavior.
- **Password Policy**: Requirements for password strength and expiration.
- **Remote Access Policy**: Rules for VPN/remote login.
- **Incident Response Plan**: How to handle security breaches.

---
### 4.3. Authentication, Authorization, Accounting (AAA)
**AAA** is used for user access control:
- **Authentication**: Verifying identity.
- **Authorization**: What the user is allowed to do.
- **Accounting**: Tracking what the user did.
**Implemented via**:
- **Local**: Stored on the router.
- **Centralized**: Using RADIUS or TACACS+ servers.
**TACACS+**:
- Cisco proprietary, separates all 3 AAA functions.
- Uses TCP.
**RADIUS**:
- Open standard, combines authentication/authorization.
- Uses UDP.

---
### 4.4. VPN Security Concepts
- **Encryption**: Ensures data confidentiality.
- **Tunneling**: Encapsulates packets to travel securely over untrusted networks.
- **IPSec**: Common VPN protocol suite that provides authentication, integrity, and encryption.
  - **ESP (Encapsulating Security Payload)**: Encrypts and optionally authenticates.
  - **AH (Authentication Header)**: Authenticates only, no encryption.
**GRE (Generic Routing Encapsulation)**:
- Used to encapsulate a wide variety of network layer protocols.
- Lacks security, often paired with IPSec.

---
### 4.5. Layer 2 Security
**Switchport Security**:
- Prevent unauthorized devices on switch ports.
**Methods**:
- **MAC Address Sticky**: Learns and saves MACs dynamically.
- **Violation Modes**:
  - **Protect**: Drops unknown traffic silently.
  - **Restrict**: Drops and logs.
  - **Shutdown**: Port error-disables.
**Commands**:
```bash
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

---
### 4.6. ACLs (Access Control Lists)
Used to filter traffic based on criteria like source IP, destination IP, protocol, or port.
**Types**:
- **Standard ACLs**:
  - Filters by source IP only.
  - Use numbers 1–99 or 1300–1999.
- **Extended ACLs**:
  - Filters by source/destination IP, protocol, port.
  - Use numbers 100–199 or 2000–2699.
**Placement**:
- **Standard ACL**: Close to destination.
- **Extended ACL**: Close to source.
**Commands**:
```bash
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 110 permit tcp any any eq 80
ip access-group 10 in
```

---
### 4.7. Zone-Based Policy Firewall (ZPF)
A modern firewall method using security zones instead of interfaces.
**Concept**:
- Traffic between zones is controlled by policies.
- No traffic allowed between zones by default.
**Steps**:
1. Define zones.
2. Assign interfaces to zones.
3. Create class-maps (match traffic).
4. Create policy-maps (define actions).
5. Apply policies to zone-pairs.
**Commands (simplified)**:
```bash
zone security INSIDE
zone security OUTSIDE
zone-pair security ZP_INSIDE_OUTSIDE source INSIDE destination OUTSIDE
class-map type inspect match-any CM_HTTP
 match protocol http
policy-map type inspect PM_HTTP
 class type inspect CM_HTTP
  inspect
service-policy type inspect PM_HTTP interface fa0/0
```

---
### 4.8. Secure Management
- **SSH**: Encrypted remote access. Replace Telnet.
- **Passwords**: Use `enable secret`, `line vty`, and strong passwords.
- **Banner**: Legal notification for users (`banner motd # Unauthorized access prohibited #`)
- **Syslog**: Logs messages from network devices.
- **SNMP**: Used for monitoring and managing devices.

---
## 5. Network Automation and Programmability
### 5.1. Traditional vs. Software-Defined Networking (SDN)
#### Traditional Networking:
- Control and data planes are **integrated** in each device.
- **Manual configuration** via CLI on each individual device.
- **Static, device-by-device** management.
- Difficult to scale and maintain.
#### Software-Defined Networking (SDN):
- Control plane is **centralized** in an SDN controller.
- Devices are **programmable** and can be managed dynamically.
- Network becomes **abstracted** from the underlying hardware.
- Enables **automation**, **scalability**, and **policy-based** control.
**Control Plane**: Makes decisions about where traffic is sent.
**Data Plane (Forwarding Plane)**: Forwards traffic according to control plane decisions.

---
### 5.2. SDN Components
- **Application Layer**: Interfaces and tools (e.g., analytics, security).
- **Control Layer (Controller)**: Central "brain" of the network (e.g., Cisco DNA Center, OpenDaylight).
- **Infrastructure Layer**: Physical devices (switches, routers, firewalls) that follow instructions from the controller.

---
### 5.3. Southbound vs. Northbound APIs
- **Southbound APIs**:
  - Connect the SDN controller to the infrastructure layer.
  - Most common: **OpenFlow**, Cisco OpFlex, NETCONF.
  - Purpose: Push configurations, collect data.
- **Northbound APIs**:
  - Connect SDN controller to applications or business logic.
  - Commonly use **REST APIs**.
  - Purpose: Let applications **read** and **write** network policies.

---
### 5.4. REST APIs
**Representational State Transfer (REST)** is a set of rules for designing web services.
- **CRUD Operations**:
  - **Create**: `POST`
  - **Read**: `GET`
  - **Update**: `PUT` or `PATCH`
  - **Delete**: `DELETE`
**Example REST API Call**:
```bash
GET /api/v1/devices
```
**Data is often returned in**:
- **JSON (JavaScript Object Notation)** — lightweight data format.

---
### 5.5. JSON Example
```json
{
  "device": {
    "hostname": "router1",
    "ip": "192.168.1.1",
    "status": "up"
  }
}
```
JSON is used for easy readability and parsing by scripts and applications.

---
### 5.6. Configuration Management Tools
These tools allow for **automated deployment** and **management of configurations**:
- **Puppet**: Declarative, Ruby-based configuration management.
- **Chef**: Ruby-based, uses recipes to describe server setups.
- **Ansible**:
  - Agentless.
  - Uses **YAML playbooks**.
  - Push-based model — configs are sent from a central control machine.
**Why use them?**
- Reduce human error.
- Consistency across devices.
- Fast rollout and rollback.

---
### 5.7. Python and Automation
Python is commonly used for scripting automation tasks.
**Libraries**:
- `netmiko` – SSH-based automation.
- `paramiko` – Low-level SSH.
- `napalm` – Cross-vendor configuration and state reading.
**Sample Python Script** (using `netmiko`):
```python
from netmiko import ConnectHandler
device = {
    'device_type': 'cisco_ios',
    'ip': '10.10.10.1',
    'username': 'admin',
    'password': 'cisco'
}
connection = ConnectHandler(**device)
output = connection.send_command("show ip int brief")
print(output)
connection.disconnect()
```
---
### 5.8. Cisco DNA Center
- Cisco’s **SDN controller** for enterprise networks.
- Provides centralized management, automation, assurance, and analytics.
- Uses **REST APIs** for programmability.
- Integrates with tools like **Ansible** and **Python scripts**.

---
### 5.9. Benefits of Automation and SDN
- **Reduced human error**
- **Faster provisioning and changes**
- **Scalability**
- **Improved consistency**
- **Simplified management and troubleshooting**
- **Better network insight and analytics**

---
## Final Review Tips
1. **Understand SDN concepts**, REST APIs, and JSON.
2. **Memorize key commands** (ACLs, VLANs, routing, port-security).
3. **Understand diagrams**, like WAN topologies, IP addressing, ACL placement.
4. **How NAT and ACLs work together**.

