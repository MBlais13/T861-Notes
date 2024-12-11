
> [!Info] Modules Directory
> **Module 1**: Page 55
> **Module 2**: Page 133
> **Module 3**: Page 202
> **Module 4**: Page 280
> **Module 5**: Page 348
> **Module 6**: Page 409
> **Module 7**: Page 486
> **Module 8**: Page 562
> **Module 9**: Page 639
> **Module 10**: Page 691
> **Module 11**: Page 766
> **Module 12**: Page 823

> [!warning] Test Contents
> Test 1:
> Test 2:
> Final Test 3: 5, 9, 11 & 12

Just use ChatGPT or something to get the answers and explanation.

---

# Module 5
1. **Which of the following occurs when you encrypt a file using EFS within a domain environment?** (Choose all that apply.)  
   a. An asymmetric private key is generated and used to encrypt the file contents  
   b. A copy of the symmetric encryption key is stored within the file metadata and asymmetrically encrypted with your public key  
   c. A symmetric encryption key is generated and used to encrypt the file contents  
   d. A copy of the symmetric encryption key is stored within the file metadata and asymmetrically encrypted with the recovery agent’s public key  

2. **Only the NTFS filesystem supports all of the basic and advanced attributes for folders and files.** True or False?

3. **Which of the following can be used to set the compress attribute for an NTFS file?** (Choose all that apply.)  
   a. Set-ItemProperty
   b. cipher.exe  
   c. compress.exe  
   d. compact.exe  

4. **Which of the following basic NTFS/ReFS permissions allows you to delete a file?** (Choose all that apply.)  
   a. Full control  
   b. Modify  
   c. Write  
   d. Read and execute  

5. **You wish to grant a specific user the ability to view the read-only attribute on files within a particular folder on the system, but do not wish to grant any other access. What advanced permission should you assign to this user?**  
   a. Traverse folder/execute file  
   b. Read attributes  
   c. Read extended attributes  
   d. Read permissions  

6. **You can use the Set-ACL cmdlet within Windows PowerShell to configure entries within a DACL or SACL.** True or False?

7. **Your organization maintains a shared folder called PrivateHR that only the HumanResources-G and Domain Admins groups have access to. You wish to audit each time a member of the HumanResources-G group successfully modifies or deletes a file within this folder. What must you do?** (Choose all that apply.)  
   a. Configure an audit entry within the SACL of the PrivateHR folder that allows the Modify permission for the HumanResources-G group  
   b. Configure the audit attribute on the PrivateHR folder  
   c. Configure an audit entry within the SACL of the PrivateHR folder that audits the Modify permission for the HumanResources-G group  
   d. Enable success auditing for the system using an audit policy  

8. **Which of the following Windows logs stores auditing events?**  
   a. System  
   b. Application  
   c. Security  
   d. Auditing  

9. **You are about to move an EFS-encrypted file called SecureData.xml from a folder on an NTFS volume to a folder on a ReFS volume. Which of the following statements are true regarding the permissions and encryption on the file following the move operation?** (Choose all that apply.)  
   a. SecureData.xml will retain its original permissions following the move operation  
   b. SecureData.xml will remain encrypted following the move operation  
   c. SecureData.xml will inherit the permissions from the target folder following the move operation  
   d. The SecureData.xml will not be encrypted following the move operation  

10. **The View effective access tab within the Advanced Security Settings window for a folder or file can be used to view the groups that have access to a particular folder or file.** True or False?

11. **You have shared a folder using SMB and assigned members of the Accounting group Full Control shared folder permission. One of the members of the Accounting group complains that they get an access denied message when attempting to access files within the shared folder. What are two possible causes of this issue?** (Choose two answers.)  
   a. The shared folder is on an FAT32 or exFAT volume, and the DACL on the files denies access to a group to which the user belongs  
   b. The shared folder is on an FAT32 or exFAT volume, and the DACL on the files does not allow the user access  
   c. The shared folder is on an NTFS or ReFS volume, and the DACL on the files denies access to a group to which the user belongs  
   d. The shared folder is on an NTFS or ReFS volume, and the DACL on the files does not allow the user access  

12. **Windows systems that have the Client for NFS installed can access an NFS shared folder by browsing the network or specifying the shared folder’s UNC.** True or False?

13. **You would like to share a folder that uses the access-based enumeration feature. What must you do?**  
   a. Share the folder using SMB by accessing folder properties  
   b. Share the folder using SMB using Server Manager  
   c. Share the folder using NFS by accessing folder properties  
   d. Share the folder using NFS using Server Manager  

14. **Which of the following NFS shared folder permissions allows computers to access an NFS shared folder and modify content?**  
   a. Full Control  
   b. Change  
   c. Read-Write  
   d. Modify  

15. **Both NFS and SMB shared folders can be published to Active Directory.** True or False?

16. **You would like to provide a central shared folder that users can access to view all other shared folders within the organization. What must you do?** (Choose all that apply.)  
   a. Install the DFS Namespaces role and configure a DFS namespace  
   b. Configure a replication group  
   c. Add targets to the DFS namespace for each shared folder  
   d. Install the DFS Replication role on each file server  

17. **You are configuring a DFS replication group to synchronize folder contents between four file servers. To minimize the network bandwidth used by DFS replication, you should choose a Full mesh topology for your replication group.** True or False?

18. **You have a large number of users that access the same files within a shared folder that is replicated to another shared folder on the network using DFS replication. Users often report problems with missing content in the files that they access within the shared folder, and that changes take a long time to propagate from one shared folder to the other. What two actions can you take to address these issues?** (Choose two answers.)  
   a. Add a shared folder on a third file server to the replication group  
   b. Disable remote differential compression (RDC) on the connections within the replication group  
   c. Increase the size limit of the DFS staging folder for each member of the replication group  
   d. Modify the replication group settings to use a Full mesh topology for replication  

19. **Which of the following features are provided by the File Server Resource Manager server role?** (Choose all that apply.)  
   a. File screens  
   b. Access-based enumeration  
   c. Folder quotas  
   d. User quotas  

20. **You can use soft quotas to provide warnings to users that exceed folder quotas, while not restricting their ability to add content to a folder.** True or False?


# Module 9
1. **Which of the following is not considered a remote access technology?**  
   a. DirectAccess  
   b. L2TP  
   c. PPPoE  
   d. Remote Desktop  

2. **Split tunneling is used to ensure that all network traffic generated by a remote access client passes through a VPN to a remote access server.** True or False?

3. **Which of the following VPN protocols uses IPSec to encrypt network traffic?** (Choose all that apply.)  
   a. IKEv2  
   b. PPTP  
   c. SSTP  
   d. L2TP  

4. **What can you configure on a router to protect traffic destined for another network in the organization as it passes over the Internet?**  
   a. Port forwarding  
   b. Demand-dial interface  
   c. Reverse proxy  
   d. DirectAccess  

5. **The Remote Access role service in Windows Server 2019 provides for DirectAccess and VPN remote access, as well as RADIUS.** True or False?

6. **You have configured a remote access server in your DMZ for IKEv2 VPN access. Which ports on your NAT router must you configure for port forwarding to this remote access server?** (Choose all that apply.)  
   a. TCP port 1723  
   b. TCP port 1701  
   c. UDP port 500  
   d. UDP port 4500  

7. **Which of the following VPN authentication methods is considered the most secure?**  
   a. EAP  
   b. CHAP  
   c. MS-CHAPv2  
   d. PAP  

8. **Remote access servers can be configured as RADIUS clients.** True or False?

9. **What features does RADIUS provide for remote access connections?**  
   a. Centralized logging  
   b. Remote access policies  
   c. Centralized authentication  
   d. Centralized encryption  

10. **The user permission necessary for VPN remote access can be granted in the properties of a user account or remote access policy.** True or False?

11. **What section of a remote access policy contains characteristics that must be met for remote access, such as Session Timeout?**  
   a. Conditions  
   b. Criteria  
   c. Constraints  
   d. Settings  

12. **DirectAccess uses HTTPS to authenticate remote access users, and IPSec to create an encrypted tunnel for network traffic between the remote access client and server.** True or False?

13. **Which of the following network topologies should you choose if your DirectAccess remote access server is connected directly to the demarc, as well as to the DMZ?**  
   a. Edge  
   b. Connection Broker  
   c. Behind an edge device (with two network adapters)  
   d. Behind an edge device (with a single network adapter)  

14. **DirectAccess supports Windows 7 and later remote access clients by default.** True or False?

15. **Which of the following Remote Desktop Services role services uses HTTPS to provide encryption for all RDP packets?**  
   a. Remote Desktop Connection Broker  
   b. Remote Desktop Gateway  
   c. Remote Desktop Session Host  
   d. Remote Desktop Virtualization Host  

16. **The Remote Desktop Licensing role service cannot be installed on the same computer as the Remote Desktop Session Host service.** True or False?

17. **Which of the following must you configure to ensure that a particular group of remote access servers grants Remote Desktop access only to members of the Accounting group?**  
   a. RemoteAccess  
   b. RemoteApp  
   c. Collection  
   d. Connection Broker  

18. **At minimum, which Remote Desktop Services role services must you install to provide session-based desktop deployment across multiple remote access servers?** (Choose all that apply.)  
   a. Remote Desktop Session Host  
   b. Remote Desktop Connection Broker  
   c. Remote Desktop Licensing  
   d. Remote Desktop Virtualization Host  

19. **As a server administrator, which of the following actions can you perform on a Remote Desktop connection to provide interactive user support for the user of the session?**  
   a. Send Message  
   b. Disconnect  
   c. Duplicate  
   d. Shadow  

20. **Organizations that allow Remote Desktop sessions from remote access clients that are not licensed by the organization should choose a Per Device licensing mode when configuring Remote Desktop Services.** True or False?
# Module 11
1. **Group Policy settings apply to which of the following objects?** (Choose all that apply.)  
   a. Users  
   b. Computers  
   c. Groups  
   d. OUs  

2. **There are no GPOs created in an Active Directory domain by default.** True or False?

3. **You have created a new Group Policy Object (GPO). To which of the following objects can this GPO be linked?** (Choose all that apply.)  
   a. OU  
   b. Group  
   c. Site  
   d. Domain  

4. **Group Policy preferences can be used to configure Windows features, but are only interpreted by Windows 7, Windows Server 2008, and later computers by default.** True or False?

5. **You wish to configure a GPO that allows users in your organization to install a package using the Programs and Features section of Control Panel. Which software deployment method should you choose when configuring the Software Settings section of a GPO?**  
   a. Publish the software in the User Configuration  
   b. Assign the software in the User Configuration  
   c. Publish the software in the Computer Configuration  
   d. Assign the software in the Computer Configuration  

6. **Which section of a GPO contains the most security-related settings for the Windows operating system?**  
   a. User Configuration, Windows Settings  
   b. Computer Configuration, Windows Settings  
   c. User Configuration, Administrative Templates  
   d. Computer Configuration, Administrative Templates  

7. **You can import administrative template files into a GPO to allow Group Policy to configure third-party software settings.** True or False?

8. **Which of the following is not included in a certificate?**  
   a. Public key  
   b. Private key  
   c. Digital signature  
   d. CRL location  

9. **Which term refers to the process whereby a user or computer obtains a certificate from a CA?**  
   a. PKI  
   b. Enrollment  
   c. Revocation  
   d. Hashing  

10. **Group Policy can be configured to auto-enroll certificates for users and computers based on the permissions in a certificate template on an enterprise CA.** True or False?

11. **Which certificate template permissions must you grant to a user or computer before they are auto-enrolled for a certificate using Group Policy?** (Choose all that apply.)  
   a. Read  
   b. Write  
   c. Enroll  
   d. Autoenroll  

12. **Only schema version 1 certificate templates can be configured for auto-enrollment.** True or False?

13. **In an 802.1X Wireless configuration, which component generates the encryption keys used for WPA?**  
   a. WAP  
   b. Wireless client  
   c. RADIUS server  
   d. Domain controller  

14. **You must enroll each WAP for a certificate based on the RAS and IAS Server certificate template before they can be configured for 802.1X Wireless.** True or False?

15. **Which of the following statements regarding the functionality of WSUS are true?** (Choose all that apply.)  
   a. WSUS prevents Microsoft Update traffic from saturating the bandwidth on an organization’s Internet connection.  
   b. Group Policy is used to direct domain computers to a WSUS server for updates.  
   c. Updates can be manually or automatically approved for distribution on a WSUS server.  
   d. A WSUS server can be configured to remove updates from computers that have installed them.  

16. **To reduce the amount of storage that is consumed by updates on a WSUS server, you should configure the WSUS server to only synchronize updates for products that are deployed in your organization.** True or False?

17. **Which of the following port numbers is used to obtain updates from a WSUS server using HTTPS?**  
   a. 80  
   b. 443  
   c. 8530  
   d. 8531  

18. **Firewall profiles contain a series of firewall rules that apply to a computer when it is connected to a particular type of network (public, private, domain).** True or False?

19. **Which of the following Windows Defender features can be used to limit the files, folders, and processes that ransomware can modify?**  
   a. Core isolation  
   b. Memory integrity  
   c. Controlled folder access  
   d. Secure boot  

20. **What can you configure in the Windows Defender Firewall with Advanced Security tool to automatically protect network traffic between computers using IPSec?**  
   a. Firewall profiles  
   b. Connection security rules  
   c. IPSec rules  
   d. Security Associations  
# Module 12
1. **On which part of the maintenance cycle do server administrators spend the most time?**  
   a. Monitoring  
   b. Proactive maintenance  
   c. Reactive maintenance  
   d. Documentation  

2. **Many organizations store system documentation in help desk ticketing software.** True or False?

3. **Which of the following steps is not a common troubleshooting procedure?**  
   a. Test possible solutions  
   b. Isolate the problem  
   c. Delegate responsibility  
   d. Collect information  

4. **A baseline is a set of performance information for a system during normal times of operation.** True or False?

5. **Which of the following can be easily identified on the Processes tab of Task Manager?** (Choose all that apply.)  
   a. Rogue processes  
   b. The number of bytes a process is sending to and from the network  
   c. The files that a process is using  
   d. Memory leaks  

6. **Committed memory refers to the memory that is used by the Windows kernel and device drivers.** True or False?

7. **Which task should you perform in Task Manager before stopping a problematic process for a program that was created by your organization?**  
   a. Right-click the process and click Create dump file  
   b. Right-click the process and click Search online  
   c. Right-click the process and click Analyze wait chain  
   d. Right-click the process and click UAC virtualization  

8. **Resource Monitor allows you to identify the storage devices and files that a single process is accessing.** True or False?

9. **Which of the following components represents a specific hardware device or software component that can be monitored?**  
   a. Performance object  
   b. Performance alert  
   c. Performance counter  
   d. Instance  

10. **Which of the following performance counters can be used to identify jabbering hardware?**  
   a. Pages/sec  
   b. % Interrupt Time  
   c. Committed Bytes  
   d. Bytes Total/sec  

11. **Each server role and feature that is added to a Windows Server 2019 system also adds additional performance objects and counters.** True or False?

12. **Which two tools are commonly used to create performance baselines?** (Choose two answers.)  
   a. Performance Monitor  
   b. Task Manager  
   c. Data Collector Sets  
   d. Event Viewer  

13. **Performance baselines are typically created only after installing a new Windows Server 2019 system.** True or False?

14. **Which of the following can be included in a data collector set?** (Choose all that apply.)  
   a. Performance counter  
   b. Dump files  
   c. Event trace provider  
   d. Windows Registry key  

15. **There are five event levels available in an event log: Information, Warning, Error, Audit Success and Audit Failure.** True or False?

16. **What can you create in Event Viewer to display specific types of events from one or more event logs?**  
   a. Event filter  
   b. Custom view  
   c. Data collector set  
   d. Event alert  

17. **Reliability Monitor displays a system stability index value for each day based on the values of specific performance counters.** True or False?

18. **Which of the following actions can be performed to solve a performance problem?** (Choose all that apply.)  
   a. Stop and disable unnecessary services  
   b. Move applications to other systems  
   c. Add additional hardware  
   d. Upgrade hardware devices with bus mastering versions  

19. **Searching an event description or event ID online can generate a list of possible causes and associated solutions for a problem.** True or False?

20. **Which of the following options on the Advanced Boot Options menu can be used to start a system that failed to boot previously due to incorrect settings in the Windows Registry, or a recently added device driver?**  
   a. Safe Mode  
   b. Debugging Module  
   c. Disable Driver Signature Enforcement  
   d. Last Known Good Configuration  


---
