# CUCM & Expressway Integration

* Step 1 - Deploy .ova template. Ova template helps you to configure basic network parameters like :

    Ip address
    Network Mask
    Gateway
    DnS server
    NTP Server
    Hostname

    ![](images/2023-05-13-12-40-52.png)
    ![](images/2023-05-13-12-41-51.png)

* Step 2 - Deploy .ova template again for expressway-e with same procedure.
* Step 3 - Create `Host-A`record for expc and expe

![](images/2023-05-15-16-07-43.png)

* Step 4 -  After power on the virtual machine configure roo and admin password from colsole for expc and expe

![](images/2023-05-15-16-19-55.png)

* Step 5 - Login on `GUI` secure connection with admin user and password.

![](images/2023-05-15-16-22-13.png)

* Step 6 - Choose `type` and `Service` for node. Chose `Exressway-C` for expc and `expressway-E` for expe as a type, `Mobile and Remote Access including Meeting Server Web Proxy` for both device.

![](images/2023-05-15-16-23-10.png) 

* Step 7 - Check configuration for any mistake. This area is configured at while .ova template deployment.

![](images/2023-05-15-16-27-41.png)

* Step 8 - finish intial configuration and restart servers.

![](images/2023-05-15-16-28-58.png)

* Step 9 - Configure `System Name` on expc and expe

![](images/2023-05-15-16-49-53.png)

* Step 10 - Generate CSR fron expc and expe

Mainteance -> Security -> Server Certificate

![](images/2023-05-15-17-12-42.png)

* Step 11 - Sign CSR on CA with configured certificate template (web and client authentication). Download certificate with Base 64 encoded.

![](images/2023-05-15-18-58-18.png)
![](images/2023-05-15-18-56-19.png)

* Step 12 - Download ca root certificate and upload to server for trusted CA certificate.
Mainteance -> Security -> Trusted CA certificate

![](images/2023-05-15-19-02-19.png)
![](images/2023-05-15-19-03-07.png)
![](images/2023-05-15-19-04-31.png)

* Step 13 - Upload signed certificate to expc and expe
Mainteance -> Security -> Server Certificate

![](images/2023-05-15-19-07-45.png)

* Step 14 - Repeat this all procedures for expe
* Step 15 - Enable `SIP` TCP / UDP / TLS on expc and expe

Configuration -> Protocols -> SIP

![](images/2023-05-16-10-32-33.png)

* Step 16 - Enable `MRA` from expc and expe
Configuration -> Unified Commnications -> Configuration

![](images/2023-05-16-10-43-42.png)
![](images/2023-05-16-10-44-14.png)

* Step 17 - Create `Domain`

Configuration -> Domains

![](images/2023-05-16-10-49-00.png)
![](images/2023-05-16-10-50-07.png)

* Step 18 - Add CUCM to expc
Configuration -> Unified Commnications -> Configuration -> Unified CM Servers

![](images/2023-05-16-10-58-53.png)

* Step 19 - Add IMP to expc
Configuration -> Unified Commnications -> Configuration -> IMP

![](images/2023-05-16-11-02-51.png)

* Step 20 - Create user on Local database on expe
Configuration -> Authentication -> Local Database

![](images/2023-05-16-11-09-17.png)
![](images/2023-05-16-11-09-54.png)

* Step 21 - Create `zone` on expe for expc
Configuration -> Zone -> Zones

![](images/2023-05-16-11-13-27.png)

* Step 22 - Create `zone` on expc
Configuration -> Zone -> Zones

![](images/2023-05-16-11-16-46.png)
![](images/2023-05-16-11-17-34.png)

* Step 23 - Check Connection between expc and expe

![](images/2023-05-16-11-19-23.png)
![](images/2023-05-16-11-22-41.png)










 