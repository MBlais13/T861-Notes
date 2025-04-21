# raw
Net sec test 2?
Load balancing - hardware and software
Firewall
- Rule based firewall
- Policy based firewall
- Content/url filtering firewall 
———
Allow
Bypass
Deny
Force allow
Log only
———
Honeypot
honeynet
IDS & IPS
Air-gapped network
NAC (network access control) - (clearpass)
==== Exam ====
Rouge AP
Evil twin attack (similar ssid, fake network)
RF jamming
Pin method - push button method, no lockout method for pins
WPA uses TKIP for encryption now depreciated
WPA2 uses AES which is stronger and secure
Load balancing 
—
Saas - software as a service
iaas - infostructure as a service
Paas platform as a service
Xaas - anything as a service
—
Hypervisor
Type one & two
————
Active scanning
Passive scanning
Internal vulnerability scan
External vulnerability scan
Identifying at-risk systems
—
False positive
False negative
—
Audits
—
Passive reconnaissance 
—
Business	continuity
Business	continuity planning
- A document for a company to maintain its operations and services during and after a disaster or disruption.
Disaster recovery plan (DRP)
Uninterruptible power supply (UPS)
Off-line UPS - switches to battery when primary fails
On-line UPS - battery always on
—
Hot site - fully equipped
Warm site - has equipment but does not have current active internet or data
Cold site - provides space but client must still provide and install the equipment 
—
degaussing
Sanitize HDD
—
Change management 
Risk management (exposure to different types of danger)
Risk awareness
—
Note the difference between
- Qualitative risk assessment
	educated guess
- Quantitative risk assessment
	hard facts
—
ARO - annualized rate of occurrence
ALE
SLE
—


---
# LLM outline

#### 1. Network Security Fundamentals & Technologies

*   **Firewalls:**
    *   **Rule-Based Firewalls:** How rules are evaluated (top-down, first match wins). Importance of rule order.  Potential exam question: "Describe how a rule-based firewall processes traffic and why rule order is critical."
    *   **Policy-Based Firewalls:** More flexible than rule-based; can apply policies based on user, application, or other criteria. Understand the difference in complexity and capabilities.
    *   **Content/URL Filtering Firewalls:**  Inspects content (HTTP, HTTPS) to block access to specific websites or categories of sites. How does it work? What are its limitations (HTTPS)?
    *   **Firewall Actions:** *Crucially understand these!*
        *   **Allow:** Permits traffic.
        *   **Deny:** Blocks traffic.
        *   **Log Only:** Records traffic without blocking or allowing.  Useful for monitoring and analysis.
        *   **Bypass:** Traffic is sent directly to the destination, bypassing the firewall (usually used in specific circumstances).
        *   **Force Allow:** Allows traffic regardless of other rules (use with extreme caution!).
    *   Potential Exam Question: "Explain the difference between 'Log Only' and 'Deny' actions in a firewall. When would you use each?"

*   **IDS & IPS (Intrusion Detection System / Intrusion Prevention System):**
    *   **IDS:** Detects malicious activity and alerts administrators. *Passive*.
    *   **IPS:** Detects *and prevents* malicious activity by blocking or modifying traffic. *Active*.  Understand the difference in their roles.
    *   Signature-based vs. Anomaly-based detection.
    *   Potential Exam Question: "What is the key distinction between an IDS and an IPS? Give an example of how each might respond to a detected attack."

*   **Honeypots & Honeynets:**
    *   **Honeypot:** A single decoy system designed to attract attackers.  Purpose: gather information about attacker techniques, divert them from real systems.
    *   **Honeynet:** A network of honeypots. More complex and provides a more realistic environment for observing attacker behavior.
    *   Potential Exam Question: "Explain the purpose of a honeypot and how it can be used to improve network security."

*   **Air-Gapped Networks:**  Networks physically isolated from other networks (including the internet). Extremely secure but difficult to manage. Why are they used? What are their limitations?

*   **NAC (Network Access Control) - ClearPass Focus:**
    *   Controls access to a network based on device posture, user identity, and security policies.
    *   ClearPass is a popular NAC solution – understand its general functionality (authentication, authorization, accounting).  Focus on the *concept* of NAC rather than specific ClearPass configuration details unless otherwise specified.

#### 2. Wireless Security & Attacks

*   **Rogue AP:** Unauthorized access point connected to the network. A major security risk.
*   **Evil Twin Attack:** Attacker creates a fake Wi-Fi hotspot with a similar SSID to a legitimate one, tricking users into connecting.  How can you detect and prevent this?
*   **RF Jamming:** Disrupts wireless communication by transmitting interfering signals.
*   **PIN Method (Wireless Authentication):** Understand the vulnerabilities of push-button methods without lockout mechanisms.
*   **WPA/WPA2 Encryption:**
    *   **WPA (TKIP):**  Deprecated and insecure. *Know this!*
    *   **WPA2 (AES):** Stronger, more secure encryption standard.  Focus on AES as the preferred method.

#### 3. Cloud Computing & Service Models

Pay very close attention to the wording of these questions.
*   **SaaS (Software as a Service):** Users access software over the internet (e.g., Salesforce, Google Workspace).
*   **IaaS (Infrastructure as a Service):** Provides virtualized computing resources (servers, storage, networking) (e.g., AWS EC2, Azure Virtual Machines).
*   **PaaS (Platform as a Service):**  Provides a platform for developing and deploying applications (e.g., Google App Engine, Heroku).
*   **XaaS (Anything as a Service):** A broad term encompassing all cloud service models.

#### 4. Hypervisors

*   **Hypervisor:** Software that creates and manages virtual machines.
	*   **Type 1 (Bare-Metal):** Runs directly on the hardware (e.g., ESXi, Proxmox). More efficient.
	*   **Type 2 (Hosted):** Runs on top of an existing operating system (e.g., VMware Workstation, VirtualBox). Easier to set up but less performant.

#### 5. Vulnerability Scanning & Risk Assessment

*   **Active vs. Passive Scanning:**
    *   **Active:** Sends probes and attempts to exploit vulnerabilities.  More thorough but can be detected.
    *   **Passive:** Monitors network traffic without actively probing systems. Less intrusive, harder to detect, but may miss some vulnerabilities.
*   **Internal vs. External Scanning:** Understand the different perspectives and potential findings of each type of scan.
*   **Identifying At-Risk Systems:**  Prioritizing vulnerabilities based on severity, exploitability, and business impact.

#### 6. Security Principles & Practices

*   **False Positive:** An event flagged as malicious that is actually benign.
*   **False Negative:** A malicious event that is not detected. *This is more dangerous!*
*   **Audits:**  Systematic evaluations of security controls and practices.
*   **Passive Reconnaissance:** Gathering information about a target without directly interacting with it (e.g., using search engines, social media).

#### 7. Business Continuity & Disaster Recovery

*   **Business Continuity Planning (BCP):** A comprehensive plan to maintain business operations during and after disruptions.  Focus on *processes*.
*   **Disaster Recovery Plan (DRP):** A subset of BCP focused specifically on restoring IT systems and data. Focus on *technology*.
*   **UPS (Uninterruptible Power Supply):** Provides backup power in case of a power outage.
    *   **Offline UPS:** Switches to battery when primary fails – brief interruption.
    *   **Online UPS:** Battery always active – no interruption.
*   **Hot Site, Warm Site, Cold Site:** Understand the differences in readiness and cost.

**Example Exam Question:** "A company experiences a major power outage that disrupts its operations. Describe how a Business Continuity Plan and Disaster Recovery Plan would work together to minimize downtime and ensure business resilience."


---
**IMPORTANT NOTES:**
*   **Scenario-Based Questions:** Be prepared for scenario questions and ask you to choose the best course of action or explain why one approach is better than another. (there shouldn't be any short answers, but you should understand the concepts).
*   **Key Areas:** Wireless security, firewalls (especially actions), BCP/DRP, and cloud service models are likely to be heavily emphasized.
*   **Review Deprecated Technologies:**  Pay attention to deprecated technologies like TKIP – understanding *why* they're deprecated is important.
*   **Review Practice Questions:** Find my review questions in the other documents

