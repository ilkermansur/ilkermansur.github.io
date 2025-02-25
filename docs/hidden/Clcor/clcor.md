---
theme: "Simple"
title: CLCOR
customTheme: "my_custom_style"
slideNumber: true
transition: "zoom"
enableTitleFooter: true
---
# CLCOR
<br><br><br><br><br><br><br><br><br><br>
ilker MANSUR<br>
CCIE-Collaboration #63555<br>
mail: imansur\@btegitim.com<br>
mobile: 544 208 44 97

---

### Introduction to Concepts

- Role of PBX
- What is CUCM and its components
- General Architecture of collaboration (Cloud or Onpremise)

---

### Role of PBX

Is it possible for one SIP endpoint to call another SIP endpoint without any additional equipment?

```mermaid
flowchart LR
A[Alice Sip Endpoint]
B[Bob Sip Endpoint]

A -- sip call --> B
A -- h323 call --> B

```

---

### Role of PBX

- Call Privilege
- Corporate Directory
- Time Based Operation
- Call Forward 
- Call Detailed Record & Call Management Record
- Hunt Group, Conference etc.

---

### CUCM Components

```mermaid
graph TD

A[CUCM] -- XMPP --> B[CUP]
A -- SIP --> C[CUC]
A -- Jtapi --> D[UCCX]
A -- SIP --> E[CMS]
A -- SIP --> F[Expressway C]
A -- SIP / H323 --> G((Voive-Gw))

```

---

### General Architecture of Collaboration

```mermaid
graph LR

A[Collaboration] --> B[Cloud]
A --> C[On Premise]
B --> D[WebEX]
C --> E[CUCM]
D --> F[WebEX Meeting]
D --> G[WebEX Calling]
D --> H[WebEX CC]
C --> I[CMS]
C --> J[UCCX, UCCE]
```

---

### CUCM Architechture

- Important Network Protocols (TFTP, DHCP, NTP, RTP)

- [Used Port](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cucm/im_presence/configAdminGuide/11_5_1/cup0_b_config-and-admin-guide-1151su5/cup0_b_imp-system-configuration-1151su5_chapter_0100000.pdf)

---

### Publisher 

- Cisco Database Layer Monitor (DBL)
- Cisco DRF Master (Disaster Recovery Framework Master)
- Extension mobility

**User-facing Features :** Call Forward All(CFA), Message Waiting Indication (MWI), Do Not Disturb, Hunt Group logout, Device Mobility. 


---


### Subscriber

- Cisco CallManager (CCM)
- Cisco TFTP
- Cisco Computer telephony Integration Manager (CTI)
- Cisco Administrative XML Web Service (AXL)
- Cisco IP Voice Media Streaming App
	

---

### DB Replication

![](images/db_replication.png)

---

### Database Access Control

Database access between members of af a cluster is protected:

- By Internet Protocol (IP) access control
- By security Password

![](images/access_control.png)

---

### CUCM Signaling and Media Path

![](images/signaling.png)

---

### Deployment Options

There are three kind of deployment model acording to your company and number of **IPT**

==**Models :**==

- Single-site Deployment
- Multisite WAN centralize call process
- Multisite WAN with distributed call Process

---

### Single-Site Deployment
- CUCM servers, applications, DSP resource are at the same physical location.

![](images/single-site.png)

---

### Multisite WAN with Centralized Call Processing
- CUCM at the central site, DSP sources distributed.

![](images/multi-site-ccp.png)

---

### Multisite WAN with Distributed Call Processing
- CUCM servers and DSP resources distributed

![](images/multi-site-dcp.png)

---

### Clustering over the IP WAN

- IP carries ==intracluster== server communication.

![](images/80ms.png)

---

### Redundancy Design 
- (1:1 or 2:1)

![](images/redundancy.png)

---

### CUCM Panel

- Application User
- Administrator User

![](images/cucm_panel.png)

---

### Enterprise Parameters

- It affects all cluster parameters

![](images/enterprise_p.png)

---

### Service Parameters

- It affects specific servers

![](images/services_p.png)

---

### Day 0 Configuration

- Don't forget ==service activation!==
- Change server info from name to ip
- Change Enterprise p from name to ip
- Enable CDR for every server
- Change Max Ad-Hoc conference
- Adjust T302 inter-digit timeout

---

### User Management

```mermaid

graph TD

A[Privilege]
B[Users]
C[Application Users]
D[End Users]
E[Special users]
F[AXL-JTAPI]
G[Phone Admin]
A --> B
A --> C
B --> D
B --> E
C --example--> F
E --example--> G
```

---

### LDAP For Users

```mermaid
flowchart LR

A[LDAP server]
B[CUCM]

B --  TCP 389 or TLS 636 .--> A
A --  TCP 389 or TLS 636 .--> B
```
<br>

- Enable Syncronizing from LDAP Server
- Configure LDAP Directory (for User)
- Configure LDAP Directory (for Authentication)
- Configure LDAP Filter (for filtering)

---

### LDAP Filter

Ldap filter should be used for creating special corporate Directory.

==Example Base DN :==

```
OU=NetworkUsers, DC=example, DC=com
```

==Example Attribute :==
```
(objectClass=User,Computer,Group)
(telephonyNumber=*)
(mail=*)

```





---

### Bulk Administration Tool

- For bulk process you should use BAT or AXL

![alt text](images/bulk.png)

---

### Phone Registeration Process

```mermaid
sequenceDiagram

Phone ->> Switch : What is voice-vlan ID
Switch ->> Phone : <response> 
Phone ->> DHCP : What is option 150? (TFTP Server)
DHCP ->> Phone : <response>
Phone ->> TFTP Server : Give me <SEP_or_SIP>mac_address.cnf.xml
TFTP Server ->> Phone : Send configuration file or default configuration file
Phone ->> CUCM : Register to cucm if it has conf file or auto-registration is enable 

---

### Auto Registration

![](images/auto_registration.png)

---

### Deployment

| Feature | Single Site | Multi Site |
|--|--|--|
| Call Manager Group | high | high |
| Date Time Group | low | high |
| Region | low | high |
| Location | low | high |
| Phone Button Template | high | high |
| Softkey Template | high | high |
| Phone Security Profile | high | high |

---

### Call Privilege

![](images/call_privilege.png)

---

### Phone Button Template

![](images/pbt.png)

---

### Softkey Template

![](images/softkt.png)

---

### Phone Configuration

![](images/phoneconf.png)

