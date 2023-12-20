# Active Directory Overview

Active Directory is a service developed by Microsoft to manage Windows domain networks. It stored information related to objects like computers, users, printers etc.



The big difference between exploiting AD vs other devices is we aren't exploiting patchable vulnerabilities. AD attacks focuses on abusing features, trusts, components etc.



{% hint style="info" %}
This section focuses on PHYSICAL active directory attacking. These machines can be virtualized or cloud hosted but are fundamentally different from something like Azure Active Directory (AAD)
{% endhint %}



## Physical Active Directory at a high level

### &#x20;Domain Controllers

A server with the Active Directory DS server role installed that has been specifically promoted to a domain controller.

All Domain controllres

* Host a copy of the AD DS directory store
  * The AD Directory Data store contains a file known as "Ntds.dit"
  * This is stored by default in the %SystemRoot%NTDS folder on all domain controllres
  * This stores user data, password hash's and directory information
  * It is only accessible through the domain controller processes and protocols
* Provide authenticaiton and authorization services
* Replicate updates to other domain controllers in the domain and forest
* Allow administrative access to manage user accounts and network resources



