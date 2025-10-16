
## **🧭 MIT 642 — Comprehensive Practice Exam**

  

### **Units 1 – 3  • Network Analysis & Design**

---

**1.** Which phase of the Network Design Process identifies _what_ the network must do, not _how_ it will do it?

a) Logical Design

b) Requirements Gathering

c) Physical Design

d) Analysis Phase

✅ **Answer:** b) Requirements Gathering

💡 Defines goals and functions before technical decisions.

---

**2.** What is the main deliverable from the Analysis Phase?

a) Logical Design Diagram

b) Traffic Specification Document

c) Physical Design Plan

d) Executive Overview

✅ **Answer:** b) Traffic Specification Document

💡 Summarizes baseline data, traffic patterns, and design goals.

---

**3.** The Waterfall Life Cycle proceeds in:

a) Random order

b) Iterative loops

c) Sequential stages

d) Ad-hoc steps

✅ **Answer:** c) Sequential stages

💡 Each phase flows downward — requirements → design → build → test → deploy.

---

**4.** A switch primarily segments a LAN to:

a) Reduce broadcast domains

b) Increase collision domains

c) Provide additional bandwidth

d) Route packets between networks

✅ **Answer:** c) Provide additional bandwidth

💡 Switches create separate collision domains, improving throughput.

---

**5.** The Spanning Tree Protocol (STP) prevents:

a) Network hacking

b) Broadcast loops

c) IP conflicts

d) Signal attenuation

✅ **Answer:** b) Broadcast loops

💡 STP builds a loop-free logical topology for Ethernet networks.

---

**6.** Which of the following is _not_ a Physical Layer consideration?

a) Transmission media

b) NIC selection

c) VLAN assignment

d) Bandwidth capacity

✅ **Answer:** c) VLAN assignment

💡 VLANs operate at Layer 2 (Data Link), not Layer 1.

---

**7.** The Secure Data Life Cycle applies primarily to:

a) LAN cabling

b) On-prem servers

c) Cloud data governance

d) Mainframe maintenance

✅ **Answer:** c) Cloud data governance

💡 Defines how data is created, stored, used, and retired securely in the cloud.

---

**8.** During requirements gathering, _constraints_ most often include:

a) User roles

b) Budget and schedule

c) IP address assignments

d) QoS priorities

✅ **Answer:** b) Budget and schedule

💡 Time and cost limit design decisions.

---

**9.** In a collapsed backbone, all subnet uplinks terminate on:

a) Edge switches

b) A central high-performance device

c) Multiple parallel routers

d) A single workgroup hub

✅ **Answer:** b) A central high-performance device

💡 Centralizes control and simplifies management.

---

**10.** Operational Expenditure (Op-Ex) represents:

a) One-time installation costs

b) Ongoing operating costs

c) Capital equipment purchases

d) Unused budget reserves

✅ **Answer:** b) Ongoing operating costs

💡 Recurring expenses such as maintenance and licensing.

---

**11. (True/False)** Logical Design occurs after the Physical Design phase.

✅ **Answer:** False – Logical design comes first.

---

**12. (True/False)** Bridges filter traffic based on MAC addresses.

✅ **Answer:** True – Operate at Layer 2 of the OSI model.

---

**13. (True/False)** Throughput represents the maximum theoretical bandwidth.

✅ **Answer:** False – Throughput is the _actual_ effective data rate.

---

**14. (True/False)** Physical Layer security risks include unauthorized cable tapping.

✅ **Answer:** True – Cable taps can intercept signals.

---

**15. (True/False)** Routers create separate broadcast domains at Layer 3.

✅ **Answer:** True – Each interface is a unique broadcast domain.

---

**16. (True/False)** The 80/20 rule states that 80 percent of traffic should be local.

✅ **Answer:** True – Classic LAN segmentation guideline.

---

**17. (True/False)** Baseline measurements are taken once and never again.

✅ **Answer:** False – They should be repeated periodically.

---

**18. (True/False)** A switch is faster and cheaper per port than a router.

✅ **Answer:** True – Switches provide wire-speed forwarding.

---

**19. (True/False)** Cloud service models include SaaS, PaaS, and IaaS.

✅ **Answer:** True – These are the three main delivery models.

---

**20. (True/False)** Scalability refers to a network’s ability to handle future growth.

✅ **Answer:** True – Key design goal for adaptability.

---

**21. (Matching)**

Functional Requirements → Translate business needs into specific network services

Non-Functional Requirements → Performance and scalability metrics

Baseline → Snapshot of current network performance

Op-Ex → Ongoing operational costs

Cap-Ex → Initial implementation costs

---

**22. List and briefly explain three key trade-offs a network designer must balance.**

✅ **Answer:**

• Cost vs Performance – Higher speed and redundancy raise costs.

• Security vs Accessibility – Tight controls can limit ease of use.

• Scalability vs Simplicity – Expandable designs increase complexity.

---

**23. Differentiate between physical and logical segmentation with one example of each.**

✅ **Answer:**

• Physical – Uses hardware separation (e.g., different switches for departments).

• Logical – Uses VLANs/subnets (e.g., VLAN 10 for HR, VLAN 20 for Finance).

---

**24. Describe the purpose of a Traffic Specification Document and three elements it contains.**

✅ **Answer:** Guides logical design based on data.

Includes traffic estimates, baseline measurements, CPU utilization stats, and recommended objectives.

---

**25. Explain connection-oriented vs connectionless protocols and give examples.**

✅ **Answer:**

• Connection-oriented – Establish session before data (TCP).

• Connectionless – No setup; packets sent directly (UDP).

---

**26. Identify three factors to evaluate when making Physical Layer design decisions.**

✅ **Answer:** Bandwidth and response time, reliability and redundancy, security and environmental conditions.

---

**27. Scenario:** Three buildings connected by fiber, moving apps to cloud, need high availability and security.

✅ **Answer:**

• Business Reqs – High availability, secure hybrid cloud.

• Logical Design – Redundant core switches, VLANs, VPN tunnels.

• Physical Design – Fiber uplinks, UPS, redundant links.

---

**28. Bonus:** Explain the Spiral Life Cycle and how it differs from Waterfall.

✅ **Answer:** Spiral is iterative and adaptive; loops through plan-design-test stages for continuous improvement. Waterfall is linear and sequential.

---

Would you like me to make a **print-ready version** (one page for questions, one for answers) so you can quiz yourself offline?