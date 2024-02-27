---
layout: post
title:  "FortiGate and Mikrotik Site to Site VPN  "
subtitle: "Site to Site VPN "
tags: [Networking]
---

#### Configuration - FortiGate to Mikrotik IPsec VPN

### Diagram 

![ace](/img/IPSec%20VPN/HighLevel.png)

IP Address Information 
```
172.17.1.1/24        Fortigate Server Farm 
172.17.10.1/24       Mikrotik Server Farm 

```

FortiGate IPsec VPN Config 

```
Go to VPN >> Click IPsec VPN Tunnel 
Create IPsec VPN 
```
![ace](/img/IPSec%20VPN/FW_IPsec.png)

```
Name : IPsec
IP Address : Remote Site Public IP Address 
Interface : WAN 
NAT Traversal : Disable 
```

Authentication and Phase 1 Proposal 

![ace](/img/IPSec%20VPN/FW_Phase1.png)

```
Method : Pre-Shared Key
Pre-shared Key : 123456789
Mode : Aggressive 
Phase 1 Proposal 
Encryption : AES128
Authentication : SHA256 
Diffie-Hellman Group : 2 

```

Phase 2 Selectors

![ace](/img/IPSec%20VPN/FW_Phase2Selectors.png)

```
Name : Sample
Local Address : 172.17.1.1/24
Remote Address : 172.17.10.1/24  

```

IPsec VPN Policy

```
Go to Firewall Policy  >> Create New   
Name : IPsec-VPN 
Incoming Interface : LAN
Outgoing Interface : IPsec
Source : All 
Destination : All 
Service : All 
NAT : Disable 

```


### Mikrotik Configuration 

Create IPSec Profile 

```
Go to IP >> IPSec
Select Profiles 

```
![ace](/img/IPSec%20VPN/FW_Phase2Selectors.png)

```
Name : TO-DC
Encryption Algorithm : aes- 128 
DH Group : modp 1024 
DPD : 5 

```

Create IPSec Peers

```
Go to IP >> IPSec
Select Peers

```
![ace](/img/IPSec%20VPN/FW_Phase2Selectors.png)

```
Name : peer-Tunnel
Address : Remote Gateway Address 
Profile : TO-DC

```

Create IPSec Identities 

```
Peer : peer-Tunnel
Auth Method : Pre Shared Key  
Secret : 12345678

```

Create IPSec Proposal 

```
Auth Algorithms : Sha256
Encr Algorithms : aes-128 cbc


```

Create IPSec Policy 

```
Peer : peer-Tunnel
Src Address : 0.0.0.0/0
Dst Address : Remote Gateway Address 


```