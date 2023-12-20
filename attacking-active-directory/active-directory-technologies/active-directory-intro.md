# Active Directory - Intro

Active Directory is a service developed by Microsoft to manage Windows domain networks. It stored information related to objects like computers, users, printers etc.



The big difference between exploiting AD vs other devices is we aren't exploiting patch-able vulnerabilities. AD attacks focuses on abusing features, trusts, components etc.



{% hint style="info" %}
This section focuses on PHYSICAL active directory attacking. These machines can be virtualized or cloud hosted but are fundamentally different from something like Azure Active Directory (AAD)
{% endhint %}



## Physical Active Directory at a high level

### Domain Controllers

A server with the Active Directory DS server role installed that has been specifically promoted to a domain controller.

All Domain controllers

* Host a copy of the AD DS directory store
  * The AD Directory Data store contains a file known as "Ntds.dit"
  * This is stored by default in the %SystemRoot%NTDS folder on all domain controllers
  * This stores user data, password hash's and directory information
  * It is only accessible through the domain controller processes and protocols
* Provide authentication and authorization services
* Replicate updates to other domain controllers in the domain and forest
* Allow administrative access to manage user accounts and network resources

## Logical AD Components

#### AD DS Schema

* Defines every type of object that can be stored in the directory
* Enforces rules regarding object creation

Domains

* Domains are used to group and manage objects in an organization
  * An administrative boundary for applying policies to groups of objects
  * A replication boundary for replicating data between domain controllers
  * An authentication and authorization boundary that provides a way to limit the scope of access to resources

#### Trees

* A domain tree is a hierarchy of domains in AD DS
  * All domains in the tree
    * Share a contiguous namespace with the parent domain
    * Can have additional child domain
    * By default create a 2 way transitive trust with other domains

#### Forest

* A collection of one or more domain tree
  * All forests
    * Share a common schema
    * Share a common configuration partition
    * Share a common global catalog to enable searching
    * Enable trusts between all domains in the forest
    * Share the enterprise Admins and Schema Admins groups



## Active Directory - Objects

The core of any Windows Domain is the Active Directory Domain Service (AD DS). This is the catalogue that holds all information about the other objects in the network. Object types include

* Users - The most common group in AD. Users are one of the objects known as security principals aka that they are authenticated by the domain and can be assigned privileges. User's can further be subdivided into 2 categories
  * People - Employees, organizational staff that needs access to the network
  * Services - Defined to be used by services like IIS or MSSQL. Every service requires a user to run, but service user's are different as in they will only have privs needed for that specific service.
* Machines - For every computer that joins an AD domain a machine object will be created. Machines are also considered "security principals" and are assigned an account just as any regular user. This account has somewhat limited rights within the domain itself. The machine accounts themselves are local admins on the assigned computer and are not generally supposed to be accessed beyond the computer itself. This being said, a password is password.
  * The stipulation is machine accounts are automatically rotated out and are comprised of 120 random characters.
  * The machine account name is the computers name followed by a dollar sign aka DC01 = $DCO1
* Security Groups - These allow you to define user groups to access rights to files or other resources. Any users added to an existing group will automatically inherit all of the group's privileges. With this, security groups are also considered security principals and can have privileges over resources on the network.
  * These groups can have both users and machines as members.
    * Domain Admins - Users of this group have admin privs over the entire domain. By default they can administer any computer on the domain including DC's.
    * Server operators - Can admin Domain controllers but cannot change any administrative group membership
    * Backup Operators - Users in this group can access any file and are able to perform backups of data on computers
    * Account Operators - Can create/Modify other accounts in the domain
    * Domain Users - All existing user accounts
    * Domain Computers - All existing computers
    * Domain Controllers - All existing DCs

## Organizational Units vs Security Groups

* OUs are useful for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. User's can only be a member of a single OU at a time
  * There are a handful of default OU's setup by windows
    * Builtin: Default groups available to any Windows host
    * Computers: Any machine joining is put there by default
    * Domain Controllers: OU for DC's
    * Users: Default users and groups that apply to a domain-wide context
    * Managed Service Accounts: Holds all service accounts
* Security groups instead are used to grant permissions over resources. You will use groups if you want to allow some users to access a shared folder or a network printer. A user can be part of many groups which is needed to grant access to multiple resources.



