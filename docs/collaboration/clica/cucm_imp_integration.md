# CUCM & IMP Integration

***CUCM Side***

PS: All UC components (CUCM,CUP) `Host-A`, `PTR`, `SRV` record must be made. 

```
hqcucmpub.cciecollab.com (HOST-A)
hqcuppub.cciecollab.com (HOST-A)
_cisco-uds._tcp.cciecollab.com (SRV)
```

* Step 1 - Add IMP ip address to CUCM as a server.

![](images/2023-05-11-22-15-44.png)
![](images/2023-05-11-22-17-25.png)


* Step 2 - While the installation is runnig backstage, create `SIP TRUNK SECURITY PROFILE` for trunk.

System -> Security -> Sip Trunk Security Profile then `add new` 

![](images/2023-05-11-22-48-18.png)

* Step 3 - Create `TRUNK` for cup server

Device -> Trunk then `add new`

![](images/2023-05-11-22-54-30.png)

Configure `TRUNK` parameters

![](images/2023-05-11-22-56-09.png)
![](images/2023-05-11-23-01-44.png)

* Step 4 - Use previous trunk for Service parameter

System -> Service Parameters

![](images/2023-05-11-23-05-52.png)

![](images/2023-05-11-23-07-24.png)

* Step 5 - Create `UC SERVICES` for 'CTI' and 'CUP Services'

User Management -> User Settings -> UC Services then `add new`

![](images/2023-05-11-23-14-33.png)
![](images/2023-05-11-23-15-25.png)

* Step 6 - Create `SERVICE PROFILE` for Jabber Devices.

User Management -> User Settings -> Service Profile then `add new`

![](images/2023-05-11-23-22-42.png)
![](images/2023-05-11-23-23-14.png)

* Step 7 - Create `Access Control Group` for Jabber User

User Management -> User Settings -> Access Control Group

![](images/2023-05-12-11-38-19.png)
![](images/2023-05-12-11-39-50.png)

* Step 8 - Enable `LDAP Server` on cucm

System -> Ldap -> Ldap System

![](images/2023-05-12-19-06-38.png)

* Step 9 - Add `LDAP Directory` from 

System -> Ldap -> Ldap Directory then `add new`

![](images/2023-05-12-19-14-34.png)
![](images/2023-05-12-19-15-33.png)

then configure `LDAP Authentication` for enduser authentication

![](images/2023-05-12-19-34-08.png)

* Step 10 - Pull User for Ldap

![](images/2023-05-12-19-17-29.png)

* Step 11 - Use `Service profile`  and `Access Control Group` ,which are created previous steps, to user who use jabber device

![](images/2023-05-12-19-19-19.png)
![](images/2023-05-12-19-20-26.png)

 * Step 12 - Create Jabber Device with this user

![](images/2023-05-12-19-35-26.png)
![](images/2023-05-12-19-35-59.png)
![](images/2023-05-12-19-36-25.png)

under line configuration

![](images/2023-05-12-19-37-23.png)

* Step 13 - Add device to User under `End User` configuration

![](images/2023-05-12-19-38-54.png)

***CUP Side***

* Step 1 - Complate `CUP` server console configuration like below

![](images/2023-05-11-22-25-55.png)
![](images/2023-05-11-22-26-44.png)
![](images/2023-05-11-22-27-29.png)
![](images/2023-05-11-22-28-45.png)
![](images/2023-05-11-22-29-12.png)
![](images/2023-05-11-22-29-36.png)
![](images/2023-05-11-22-30-03.png)
![](images/2023-05-11-22-32-10.png)
![](images/2023-05-11-22-34-01.png)
![](images/2023-05-11-22-34-44.png)
![](images/2023-05-11-22-36-49.png)
![](images/2023-05-11-22-37-42.png)
![](images/2023-05-11-22-38-13.png)
![](images/2023-05-11-22-38-42.png)
![](images/2023-05-11-22-39-32.png)
![](images/2023-05-11-22-40-22.png)
![](images/2023-05-11-22-40-46.png)

* Step 2 - After installation is finished activate `CUP` services from CUCM

Cisco Unified Servicebility -> Tools -> Service Activation and Check all Services

![](images/2023-05-12-11-23-33.png)
![](images/2023-05-12-11-29-35.png)

* Step 3 - Check sip trunk which is created on CUCM from 

Presence -> Settings -> Standard Configuration

![](images/2023-05-12-11-42-11.png)

* Step 4 - Add CUCM as gateway to CUP Server from

Presence -> Gateway then `add new`

![](images/2023-05-12-11-45-40.png)

* Step 5 - Configure `Default Cisco SIP Proxy TCP Listener` as a preferred proxy listener 

![](images/2023-05-12-11-47-29.png)

* Step 6 - Create `CCMCIP Profile` from 

Application -> CCMCIP Profile then `add new` configure cucm pub and sub

![](images/2023-05-12-11-51-00.png)

* Step 7 - Reboot `CUP Server` gracefully

