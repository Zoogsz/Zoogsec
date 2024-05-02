# Common Active Directory Network Technologies

## Netbios over TCP/IP (NBT-NS)

```
Ports used: 137/UDP 
```

_Technically_ NetBIOS provides 3 distinct services.&#x20;

1\) The name service for name registration/resolution (mentioned above).&#x20;

2\) Datagram distribution service for connectionless communication (138/udp)

3\) Session service for connection-oriented communication (139/tcp)



But what is relevant for us here we care about the first mentioned. NBT-NS is both the precursor and an essential part of LLMNR and translates the local IP to a NetBIOS name on a local network. Essentially, it is local DNS. Each machine is assigned a NetBIOS name by the NBT-NS service that works on the aforementioned 137/UDP port.

## Link-Local Multicast Name Resolution

The easy route of every AD Pentest.

```
Port used: 5355/UDP
```

Link Level Multicast Name Resolution (LLMNR) is essentially a local "crowd-sourcing" of local domain names. It allows name resolution (Hostname to a given IP) locally without the need for a DNS server. Picture a user searching for a specific network share named \\\2024\_Reports (I promise this will be relevant) and it the DNS server doesn't know where this domain came from. The requesting machine will then send out a request across the environment also known as a **Multicast Request** saying&#x20;

"Well do any of you know who has \\\2024\_Reports"?

This stage is where an attacker could poison LLMNR but we will get to that in a bit. Essentially LLMNR exists to cover potential gaps within the local DNS policy.



**Note: LLMNR use in itself can immediately be considered a finding. Microsoft has encouraged migration from use of LLMNR/NetBios in favor of mDNS since April 2022**



## Multicast DNS

```
Port used: 5352/udp
```

Multicast DNS is a protocol aimed at helping with name resolution in networks. This protocol was originally created by Apple to help with setup of devices via the Bonjour service - now it has extended to all sorts of Windows and IOT systems. This exists as a replacement for both NetBios and LLMNR and works in a very similar way.&#x20;



MDNS just like LLMNR sends out packets to other hosts to attempt to locally crowd-source "what is the name for this IP here".&#x20;





