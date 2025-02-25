# CMS Deployment

**Database:** Allows some configuration, such as dial plan, spaces, and users to be aggregated. Supports clustering for high availability only (single master).<br>
**Call Bridge:** The audio and video conferencing bridge, including all call control and media processing. Supports clustering for high availability and scalability.<br>
**XMPP server:** Registration & authentication for CMA and WebRTC clients as well as inter-component signaling. Can be clustered for high availability only.<br>
**Web Bridge:** Provides access for WebRTC clients<br>
**Web Admin:** Administration GUI and API access, including for Unified CM ad-hoc conferencing<br>
**Recording & Streaming:** Call recording and streaming functionality

**Configuration Modes**

**Command Line (CLI):** The command-line interface, known as the MMP (or Mainboard Management Processor, from the Acano appliance days), for initial configuration tasks and certificates.<br>
**Web Admin:** Primarily for CallBridge-related configuration, especially when configuration a single, non-clustered server.<br>
**REST API:** Used for most advanced configuration tasks and those that involve a clustered database.

In addition, the SFTP protocol is used to transfer files - typically licenses, certificates, or logs - to and from the CMS server. While there may be tools that can configure much of this, it is imperative for administrators to understand and be comfortable with each of these methods of access and the type of information each provides.

**Prerequests:**

1. DNS Host-A record for all cms node

![](images/2023-09-14-21-27-53.png){height="60%" width="60%"}

do same record for all CMS nodes

![](images/2023-09-14-21-31-22.png){height="60%" width="60%"}

**Step 1 - Configure password**

Configure connectiom credential on console connection. CMS forces you to change password. Default username is `admin` and default password is also `admin`. Change password to for example `cisco`.

![](images/2023-09-14-21-52-44.png)


**Step 2 - Configure Hostname and IP address**

For your reference, the following command was used to configure the IP address on the CMS1 server:

```
CMS> hostname cms1
A reboot is required for the change to take effect
!
ipv4 a add 192.168.80.151/24 192.168.80.254
!
!
CMS> ipv4 a
IPv4 configuration:
    address         192.168.80.151
    default         true
    dhcp            false
    enabled         true
    gateway         192.168.80.254
    macaddress      00:50:56:BC:FC:7D
    prefixlen       24
IPv4 observed values
Addresses:
192.168.80.151/24
Routes:
    source          destination     gateway         global
    0.0.0.0         192.168.80.151  0.0.0.0         false
    0.0.0.0         192.168.80.0    0.0.0.0         false
    0.0.0.0         192.168.80.0    0.0.0.0         false
    0.0.0.0         192.168.80.255  0.0.0.0         false
    0.0.0.0         0.0.0.0         192.168.80.254  true
CMS>
```
**Step 3 - Installation CMM**

CMM configuration assistant getting easy to CMS configuration DNS, Certification, NTP, Timezone, LDAP etc...

![](images/2023-09-15-12-16-22.png){height="60%" width="60%"}

![](images/2023-09-15-12-18-46.png){height="60%" width="60%"}

After initial deployment, CMM generate random password for GUI

![](images/2023-09-15-12-22-47.png){height="60%" width="60%"}

**Step 4 - Configuration CMM**

* renew password

![](images/2023-09-15-12-30-49.png){height="60%" width="60%"}

* Configure CDR for CMS servers

![](images/2023-09-15-12-32-30.png){height="60%" width="60%"}

* Configure NTP

![](images/2023-09-15-12-35-39.png){height="60%" width="60%"}

then restart for applying configuration.

**Step 4 - Add CMSs to CMM**

![](images/2023-09-15-12-42-32.png)

* Enter CMS creadentials and add

![](images/2023-09-15-12-44-03.png)

* choose deployment what you want to configuration Role 

![](images/2023-09-15-12-44-31.png)

* choose certificate parameter which you desired then click next

![](images/2023-09-15-12-47-17.png)

* Configure FQDN and SIP domain. It is very important for certification. If you want to change this parameter later, you should regenerate certification.

![](images/2023-09-15-12-50-40.png)

* Download CSR

![](images/2023-09-15-12-52-29.png)

* Sign CSR on CA server with suitable template

![](images/2023-09-15-12-56-44.png)

* Download signed certificate and root certificate with Base-64 format

![](images/2023-09-15-12-58-12.png)

![](images/2023-09-15-13-00-51.png)

* Add cms certificate and root certificate of CA server

![](images/2023-09-15-13-02-18.png)

* Configure NTP, Timezone, DNS and Web Admin port

![](images/2023-09-15-13-05-03.png)

* Configure call bridge what you want

![](images/2023-09-15-13-07-21.png)

* Next this with default parameter

![](images/2023-09-15-13-08-05.png)

* Enter LDAP or LDAPS credentials

![](images/2023-09-15-13-13-20.png)

* Check summary configuration then if everything is ok, push configuration to CMS

![](images/2023-09-15-13-14-54.png)

![](images/2023-09-15-13-17-56.png)

* After pushing configuration add CMS to CMM again but in this time choose `configured server`

![](images/2023-09-15-13-19-16.png)

![](images/2023-09-15-13-20-12.png)

All this configuration for CMS1 then repeate Step 4 for all CMS servers

![](images/2023-09-15-13-20-47.png)




