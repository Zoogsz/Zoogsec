---
description: God save on prem
---

# Simple Network Management Protocol

#### Obligatory "Who I ripped this info from"

Hacktricks <3

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp" %}

Exploit Notes

{% embed url="https://exploit-notes.hdks.org/exploit/network/protocol/snmp-pentesting/" %}

And of course, wikipedia.



## Intro

What is SNMP? Simple Network Management Protocol is used to monitor different devices within a network. It is an IP standard protocol for collecting and organizing information about managed devices on IP networks and modifying that information to change certain device behavior.&#x20;



Typically you will see open SNMP ports on the following devices

* Modems
* Printers (One person's nightmare is our dream)
* Routers
* Switches
* Servers
* Workstations&#x20;
  * And so so much more!

## SNMP Versions

#### SNMPv1/v2/v2c

This is still the most frequently used, the authentication is based on a community string that travels in plain text. Version 2 and 2c send the traffic in plaintext and also uses a community string as authentication

#### SNMPv3

Uses a better authentication form and the information travels encrypted. Could still run a dir attack against it but itll be more difficult

## MIB

One of the fundemental parts of SNMP is the Management Information Base (MIB). A large issue with how varying the devices and manufactures are when it comes to what needs SNMP to function, and MIB is the solution.

MIB is used to standardize access across manufacturers with different client-server combos. Simply put, its a text file in which all query-able SNMP objects of a device are listed in a standardized tree hierarchy .

Each of these will always contain at least one **Object Identifier (OID)** which will have a unique address, name, type, access rights, and description.

These files are written in **Abstract Syntax Notation One (ASN.1)** based ASCII text format. The MIBs do not contain data, but they explain where to find which information and what it looks like which will return the values for the specific OD.



## OIDs

Object Identifiers are used to uniquely identify managed objects in a MIB hierarchy. This can be depicted as a tree, the levels of which are assigned by different organizations. Top level MIB object IDs (OIDs) belong to different standard organizations. Vendors define private branches including managed objects for their own products

{% embed url="https://www.netadmintools.com/snmp-mib-and-oids/" %}
Way better resource
{% endembed %}

Let us take the example of an OID here.

1 . 3 . 6 . 1 . 4 . 1 . 1452 . 1 . 2 . 5 . 1 . 3. 21 . 1 . 4 . 7

Here is a breakdown of this address.

* 1 – this is called the ISO and it establishes that this is an OID. This is why all OIDs start with “1”
* 3 – this is called ORG and it is used to specify the organization that built the device.
* 6 – this is the dod or the Department of Defense which is the organization that established the Internet first.
* 1 – this is the value of the internet to denote that all communications will happen through the Internet.
* 4 – this value determines that this device is made by a private organization and not a government one.
* 1 – this value denotes that the device is made by an enterprise or a business entity.

These first six values tend to be the same for all devices and they give you the basic information about them. This sequence of numbers will be the same for all OIDs, except when the device is made by the government.

Moving on to the next set of numbers.&#x20;

* 1452 – gives the name of the organization that manufactured this device.
* 1 – explains the type of device. In this case, it is an alarm clock.
* 2 – determines that this device is a remote terminal unit.

The rest of the values give specific information about the device.

* 5 – denotes a discrete alarm point.
* 1 – specific point in the device
* 3 – port
* 21 – address of the port
* 1 – display for the port
* 4 – point number
* 7 – state of the point



