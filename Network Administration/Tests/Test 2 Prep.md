# Test prep & possible questions that could possibly be on the test

Domain controller with physical entry concerns what should it be
=Read only

What is the modern XML print standard used by windows server
=XPS

What allows a client to send a print job directory to a network printer, reducing WAN traffic to the print server
=Branch Office Direct Printing

If users report that a printer is outputting garbled text what is the most likely cause
=corrupt printer driver

What prevents users from saving certain file types like .exe… etc
=File Screening

What monitors/alerts admins but does not prevent users from saving certain file types like .exe… etc
=soft file screening

Which FSMO role acts as the primary time source for the domain and processes password changes?
=PDC Emulator

If a user is granted "Modify" NTFS permissions through one group, but "Deny Write" through another, what is their effective ability?
=deny overrides allow (the test will want a direct answer & the most restrictive permission always wins)

Company A just acquired company B. Both have their own separate AD forests. 
You need to set up a relationship so that employees at Company A can log in to specialized servers over at Company B. However, for security reasons, employees at Company B should not have any access to Company A's resources.
=Company B is trusting, Company A is trusted (test will want a DIRECT answer like what kind of trusting group..etc)

What happens if the RID master role goes offline for an extended period of time. What is the first impact to the domain
=DC’s will be unable to create new security objects

To apply a folder quota on your file server, which specific step must be completed first?
=Install the “file server resource manager” role using server manager (they want the LITERAL first step…)

Which command will allow you to see these hidden objects?
=`Get-ChildItem -hidden` (there will be multiple options that look VERY similar to each other)

Which group scope can contain members from any domain in the forest and be used to assign permissions to resources in any domain?
=Universal (global from own domain - universal from any domain)

Which role must be contacted to modify the Active Directory schema?
=Schema Master (1 per forest) (question was similar)

Why enable UGMC in a branch office?
=To allow fast logons in sites that do not have a Global Catalog server.

Which FSMO role handles cross-domain object references - (ie; updating a users name in a different domain)
=Infrastructure master

What happens to the "Archive" bit after a successful backup?
= the backup software clears the archive status

What is required for one printer to send jobs to multiple physical devices?
=the print devices must use the same printer driver

—
## Notes
There were some other UGMC, FSMO, RID questions but I honestly dont remember those questions or material.
—
## Review
Active Directory Group Scopes
Global = objects located within the same domain and the global group
Domain local = objects located within any domain in the forest (only the domain where the local group resides)
Universal = objects located within any domain in the forest

#### Active Directory
Big shared database for a company network:
- Users
- Computers
- Passwords
- Groups
- Permissions
Multiple domain controllers hold copies of this database so the network keeps working even if one controller fails.
Some things require special handling and thats where FSMO and UGMC come in.

Active Directory Group Scopes
Global = objects located within the same domain and the global group
Domain local = objects located within any domain in the forest (only the domain where the local group resides)
Universal = objects located within any domain in the forest

——

FSMO
Flexible single master operations
- This is a special responsibility given to one domain controller.
Even though Active Directory usually lets all domain controllers update the database, some operations must only happen on one server to prevent conflicts.

THINKING:
Imagine a google doc with 10 editors.
Most edits can be done by everyone
Some tasks like deciding company structure require authority. Like a FSMO role holder.

5 Roles:
**Forest Wide**
	Schema master
        - Controls changes to the structure of AD
        - Ex: adding new attributes for applications
	Domain naming master
		- controls adding/removing domains in the forest
**Domain Wide**
	RID Master
		- assigns a unique ID to users and computers
	PDC Emulator
		- Handles password updates and time sync
		- If a login fails due to replication delay, DC’s check this server
	Infrastructure Master
		- keeps group membership references updated between domains

UGMC
Universal group membership caching

———

A windows server that has not joined a domain is called a member server.
Objects within the Active Directory that represent a user, group or computer account, are called leaf objects.
MMC
- MMC Snap-in for adding local users and groups = MMC - microsoft management console
- Open by executing mmc.exe

——
### Printer Stuff
The Spooler: Documents are stored in C:\Windows\System32\spool\PRINTERS.
Branch Office Direct Printing: Client sends the job directly to the printer IP, skipping the server’s spooler to save WAN bandwidth
Print Pooling: One "logical" printer icon sending jobs to multiple physical print devices (must use the same driver).
Permissions: "Manage Documents" lets you pause/delete anyone's job. "Print" only lets you manage your own.

——
Symbols that cannot be used in an account name:
```
[ ] ; : , . 5 , 1 / \ | .
```

