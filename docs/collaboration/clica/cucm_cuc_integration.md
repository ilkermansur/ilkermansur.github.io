# CUCM & Unity Integration

* Step 1 - Install Unity Connection like CUP or CUCM server. It is classic deployment like next next
* Step 2 - First of all configure Authentication rule that is below `System Settings`

![](images/2023-06-06-20-24-07.png)
![](images/2023-06-06-20-26-04.png)
![](images/2023-06-06-20-27-54.png)

* Step 3 - Configure `User Templates`

![](images/2023-06-06-20-35-51.png)
![](images/2023-06-06-20-54-24.png)

* Step 4 - Change `Password Settings`

![](images/2023-06-06-21-01-08.png)

* Step 5 - Set `Change Password`

![](images/2023-06-06-21-03-15.png)
![](images/2023-06-06-21-05-36.png)

**For SIP integration**

* Step 6 - Configure SIP Trunk Security Profile and 3 `accept` and use in to `SIP Trunk`.

![](images/2023-06-06-21-12-58.png)
![](images/2023-06-06-21-14-23.png)
![](images/2023-06-06-21-18-21.png)
![](images/2023-06-06-21-20-28.png)
![](images/2023-06-06-21-21-19.png)

* Step 7 - Create `Route pattern` for voice mail pilot number.

![](images/2023-06-06-21-24-01.png)

* Step 8 - Configure `Voice Mail Pilot`

![](images/2023-06-06-21-27-32.png)
![](images/2023-06-06-21-28-24.png)

* Step 9 - Configure `Voice Mail Profile`

![](images/2023-06-06-21-29-26.png)
![](images/2023-06-06-21-31-19.png)

* Step 10 - In CUC site, Create `Phone System` or use default. If you create new one edit `User Template`. Dont Forget

![](images/2023-06-06-21-57-21.png)
![](images/2023-06-06-21-57-49.png)

also add `AXL User` for Pull User from CUCM. Use CUCM as a AXL user.

![](images/2023-06-06-22-03-19.png)
![](images/2023-06-06-22-05-37.png)

* Step 11 - Configure `Port Group`

![](images/2023-06-06-22-07-36.png)
![](images/2023-06-06-22-10-46.png)

* Step 12 - Configure `Port`


![](images/2023-06-06-22-14-27.png)
![](images/2023-06-06-22-15-18.png)

After Port creation, you should reset `Port Group`. Dont Forget.

* Step 13 - After this, Add user with using `AXL`

![](images/2023-06-06-22-28-29.png)

PS: User must have `Primary Extension` for to be found by AXL.

* Step 14 - Create `UC Service` for Jabber User `Service Profile`

![](images/2023-06-06-22-33-08.png)

* Step 15 - Add UC service which is created in previous step to `Service Profile`

![](images/2023-06-06-22-35-01.png)

* Step 16 - Configure Phone for voice mail and test it.

***Call Handler***

* Step 1 - Create `CTI Route Point` for redirection of calling and configure line then `forward all` to voice mail

![](images/2023-06-07-22-36-56.png)
![](images/2023-06-07-22-37-55.png)
![](images/2023-06-07-22-38-20.png)

* Step 2 - Create `System Call Handler` with extension. Upload `voice sample` which is 8bit, mono, ulaw

![](images/2023-06-07-22-40-16.png)
![](images/2023-06-07-22-42-52.png)

* Step 3 - Configure `transfer rule` uncheck `Play prompt ...`

![](images/2023-06-07-22-45-58.png)

* Step 4 - Configure `Caller input` for your scenario.

![](images/2023-06-07-22-47-49.png)

**PS:** If you need, configure schedule and holiday.