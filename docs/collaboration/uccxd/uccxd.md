# UCCXD - Deploying Cisco Unified Contact Center Express

## Introduction to UCCX

![](images/2023-07-05-11-03-36.png)

Features 

1. (ACD) Automatic Call Distribution : Route calls, skills based route call
2. IVR Interactive voice responder : Interact with customer. Customer manage IVR with pressing button. 

    1 for Sales, 
    2 for Human Resource,
    3 for Information

3. DB Information : UCCX interract with DB and pull information about customer and agent response to customer with this information.  

There are four types of `Contact Center` ,

Unified Contact Center Express        : 400 Agent

Packaged Contact Center Enterprise    : 12000 Agent

Unified Contact Center Enterprise     : 24000 Agent

Webex Contact Center                  : Cloud Based Contact Center.

**UCCX Terminology**

Computer Telephony Integration (CTI) :

CTI Route Points : When you create `Application` on UCCX, CTI route point created automatically

![](images/2023-07-05-12-12-27.png)

Call Control Group : CCG is a group of concurrent port which is configure by manually.

![](images/2023-07-05-11-51-37.png)
![](images/2023-07-05-11-54-21.png)

CTI Ports : When you configure `Call Control Group`, UCCX create `CTI PORTS` on Cucm due to API access.

![](images/2023-07-05-11-58-41.png)

Contact Service Queue (CSQ) : CSQ represents agent group. 

![](images/2023-07-05-13-11-05.png)

JTAPI Application User : JTAPI user manage CTI ports and CTI route point

![](images/2023-07-05-12-23-39.png)

RmCm Application User : Resource manager  is about `Agent` - Contact manager is about `queue`

![](images/2023-07-05-12-54-42.png)

Resource : Agents who can be used on CSQ etc

![](images/2023-07-05-12-52-50.png)

Skills : Used for speciality like language or expret level etc

![](images/2023-07-05-13-05-37.png)

Resource Group : RG used for grouping the agents. After creation you can assign agent to RG.

![](images/2023-07-05-12-58-38.png)
![](images/2023-07-05-13-03-22.png)

Teams : Used for supervisors. Supervisors responsible the agents. Agents who belong to `Team`, managed by same supervisor.

![](images/2023-07-05-13-09-36.png)

**UCCX Call Flow**

![](images/2023-07-05-14-15-17.png)

1 Step - `CUBE` accept call from ITSP.

2 Step - Call distribute from `CUBE`router with `dial-peer` to CUCM.

3 Step - There is a CTI route point on CUCM, call goes to `CC` from CTI route point over CTI ports.

4 Step - Contact Center accept call from trigger number and distribute to agent that you configure.

**Automatic Call Distribution (ACD)**

`Resource groups` are a static group of agents that can be assigned to one or more queues.

 `Skills` based routing can be configured to require an agent to be assigned one or more skills, and at a minimum level, before calls can be routed to them, and route the calls to agents based on the skill level assigned to them. Queues can be configured to route based on a number of functions based on the agent’s skill level, high to low, low to high, and based on weighting.

 In UCCX, skills are a simple text tag, and a skill level from 1 to 10. Agents can be assigned skills, and queues can be configured to require them.

 **Resource Group**
 
 ---

`Resource Group` based queuing is much more like traditional hunt group routing, where a fixed group of resources (agents) is selected from. You lose flexibility compared to Skills Based routing, but gain some simplicity. 

`Longest Idle` the person who has been off the phone the longest gets the next call

`Linear` Agent 1 always gets the call if the are available, if not, agent 2 gets the call. If neither are available, the call is delivered to agent 3, etc.


`Circular` Agent 1 gets a call, agent 2 gets the next one, and so on, unless the next scheduled agent is not available, when is skips to the next available agent in the ordered line.

Most Handled Contacts & Shortest Average Handle Time, (the system dynamically reorders the list based on efficiency metrics)

![](images/2023-07-10-22-42-44.png)

## CUCM & UCCX Integration

* Step 1 - Create `Access Control Group` for UCCX.

![](images/2023-07-03-10-15-33.png)

* Step 2 - Add `Standard AXL API Access` role to `ACG` which is created in Step 1.

![](images/2023-07-03-10-17-25.png)

* Step 3 - Create `Application User` with this `Access Control Group`

![](images/2023-07-03-10-18-43.png)

* Step 4 - On UCCX GUI, fill the information about `CUCM`

![](images/2023-07-03-10-19-42.png)

* Step 5 - This exception begun with version 12.5. You should upload `Tomcat Trust` certificate to `UCCX tomcat trust store`

![](images/2023-07-03-10-21-37.png)

* Step 6 - There are four `Tomcat Trust` certificate. Choose which belogs to `CUCM`.

![](images/2023-07-03-10-24-02.png)

* Step 7 - Download `Tomcat Trust` certificate as a .pem format, then upload it to `UCCX`. Then restart `UCCX` from cli with `utils system restart` command.

![](images/2023-07-03-10-26-19.png)

* Step 8 - Choose license type. For testing use `NFP` (Not for production).

![](images/2023-07-03-10-27-34.png)

* Step 9 - You can change license type on this page otherwise click `next` to continue.

![](images/2023-07-03-10-31-20.png)

* Step 10 - waiting for activating license then click `next`

![](images/2023-07-03-10-32-23.png)
![](images/2023-07-03-10-32-46.png)

* Step 11 - Click `next`

![](images/2023-07-03-12-43-49.png)

* Step 12 - Enter `cti` and `rmcm` user credential for managing agent and phones.

![](images/2023-07-03-12-44-47.png)

* Step 13 - Choose agent number then click `click`

![](images/2023-07-03-12-46-18.png)

* Step 14 - Choose language then click `next`

![](images/2023-07-03-12-47-09.png)

* Step 15 - Choose adminbetween users.

![](images/2023-07-03-12-57-54.png)

* Step 16 - Firstly you should assign extension as a `IPCC` Extension.

![](images/2023-07-03-12-58-53.png)

* Step 17 - Now you will see user as a resource in UCCX `Subsystems / RmCm /Resources`

![](images/2023-07-03-13-00-10.png)

* Step 18 - Now create skill and assign it `Subsystems / RmCm / Skill` and add new

![](images/2023-07-03-13-01-16.png)

* Step 19 - Add `Skill` to `Resource`

![](images/2023-07-03-13-02-07.png)

* Step 20 - Now assign supervisor capability `Wizard / RmCm Wizard / Add Supervisor` By default all users as agent capabilit. Then click `Next`

![](images/2023-07-03-13-03-51.png)

* Step 21 - Step build `Contact Service Queues` then click `Next`

![](images/2023-07-03-13-05-03.png)

- Automatic wrap UP
- Wrap up time

* Step 22 - Choose `Skill` and `Resource Selection Criteria`

![](images/2023-07-03-13-06-32.png)

* Step 23 - Congratulations you created a CSQ.

![](images/2023-07-03-13-07-18.png)

* Step 24 - Lets configure `Call Control Group`. Subsystems / Cisco Unified CM Telephony / Call Control Group then click `Add`.

![](images/2023-07-03-13-08-35.png)

* Step 25 - Check it on UCCX

![](images/2023-07-03-13-09-09.png)

and from CUCM site

![](images/2023-07-03-13-09-40.png)

## UCCX Creating Script

For creating script, we need script editor. You can download it from uccx plugin page like below.

![](images/2023-07-05-14-48-58.png)

It is easy to install. a couple of `next` `next`

![](images/2023-07-05-14-54-26.png)

* There are four sites of `script editor`.Script editor has drop-down machanism, you dont need to know any scripting language.

![](images/2023-07-05-16-04-47.png)

* example diagram

![](images/2023-07-05-17-03-27.png)

## LABS

**LAB 01 - Play prompt**

Purpose: 

Caller calls the trigger number, listen prompt and hang up line automatically. Use P_101.waw as a prompt.


Answer:

![](images/2023-07-05-17-24-53.png)

**LAB 02 - Real Scenarios**

Purpose:

Caller calls the trigger number then listen prompt, prompt says in turkish "BT Egitim'e hoşgeldiniz muhasebe için 1'e, insan kaynakları için 2'ye, satış için 3'e, teknik destek için 4'e basın". Test every option and its call routing. Use P_201.waw as a prompt. In order of options:

1. Muhasebe (1021)

2. Insan Kaynakları (1022)

3. Satış (1023)

4. Teknik Destek (1024)

Answer:

![](images/2023-07-06-11-41-33.png)

**LAB 03 - Using SET in Script Editor**

Purpose:

Use `SET` item for LAB-02 scenario. In `timeout` listen greeting prompt again and again.

Answer:

![](images/2023-07-07-12-19-08.png)

**LAB 04 - Multi-Language Usage**

Purpose:

Use `English` as a second language in same scenario. 

Answer:

![](images/2023-07-07-12-32-44.png)

**LAB 05 - Calendar Usage in UCCX Script**

Purpose:

Use `calendar` in script for arranging propt and listen off business hours prompt to caller.

Answer:

First of all, you should arrange business hours / non-business hours on UCCX GUI `Calendar Management`. 

![](images/2023-07-08-10-27-37.png)

Is there any special days cnofigure them on `schedule Custom Business Days` line below

![](images/2023-07-08-10-30-45.png)

In third step, you can schedule holidays,

![](images/2023-07-08-10-31-48.png)

PS : Earlies version of 12.X you shoud use `Day of week` and `time of day`.

![](images/2023-07-08-10-57-57.png)

**LAB 06 - Get digit String**

Purpose:

In addition to previous labs, If caller know the extensions, call is redirected the Auto Attendant. 

Answer:

We should use `switch` and `get digit String` in this scenarios 

![](images/2023-07-08-11-12-03.png)

![](images/2023-07-11-23-26-46.png)

**LAB 07 - CSQ Usage**

Purpose:

Configure `CSQ` on uccx then set this `CSQ` on script.

Answer:

![](images/2023-07-08-11-28-44.png)

**LAB 08 Usage of Increment**

Purpose:

If you want to do something exact times you can use `increment` for counting and `if` for conditional routing.

Answer:

![](images/2023-07-08-14-19-16.png)

**LAB 09 Position of Queue**

Purpose:

Configure script and say caller that the `Position of the queue` with dynamically.

Answer:

Use `Get Reporting Statistic` for getting position, then use it in prompt.

![](images/2023-07-09-19-14-51.png)

**LAB 10 Estimated Wait Time**

Puspose:

In LAB 09 add `estimated wait time` to script. Caller lissten estimated wait time. Maybe he/she will wait maybe not. 

Answer:

![](images/2023-07-09-19-55-03.png)

PS: If there is no enough data for calculating estimated wait time, script output will -1. Thats mean not an error. 

## Database Integration

UCCX can be `READ / WRITE` to external database. For this procedure, UCCX database subsystem should be runing that is under ccx engine.

![](images/2023-07-09-20-29-27.png)

and your license must be `Premium`

![](images/2023-07-09-20-31-33.png)

You should check which database or which version is sutiple for your UCCX version. For example for uccx 12.5.1 compatibility documantation is [UCCX 12.5 Compatibility](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/crs/express_compatibility/matrix/uccxcompat12_0_5_SU2.html)

In this document

![](images/2023-07-09-20-40-06.png)

In this course we use MS SQL. We need also `jbdc` driver for connection can be [download](https://jtds.sourceforge.net/) this page. Use newer version and dowsload `jtds-x.x.x-dist` file. That is zip file extract it then use.

add driver to uccx

![](images/2023-07-09-23-06-31.png)
![](images/2023-07-09-23-04-38.png)

then add SQL server as a `database source`

![](images/2023-07-09-23-08-12.png)
![](images/2023-07-09-23-15-22.png)

 we should see `Successful Test Connection` like below

 ![](images/2023-07-09-23-16-59.png)

 ## LAB - Database Integration

 Purpose:

 Set script on script editor. When customer input their customer number, script check customer number on database then return to script customer name surname, customer number and their support is gold or not. At the same time if customer has gold support, agents will deal this customer as soon as possible.

 Answer:

first of all use `DB Read` with this configuration

![](images/2023-07-12-20-57-53.png)

Field Selection is the most impotant part of this

![](images/2023-07-10-01-03-10.png)

Next step is `DB Get`. In this stage we will pair the values

![](images/2023-07-10-01-07-14.png)

If `b_gold` is True, set `Priority` higher then default

![](images/2023-07-10-01-13-29.png)

and then close connection with `DB Release`

![](images/2023-07-10-01-08-46.png)

At the same time. We will display this values to agent finesse screen with `Set Enterprise Call Info` like below.

![](images/2023-07-10-01-15-42.png)

## Finess Desktop

Cisco Finesse is a web-based application and user interface framework developed by Cisco Systems. It is designed to provide a comprehensive `agent` and `supervisor` desktop for contact center environments. Finesse enables agents and supervisors to handle customer interactions across various communication channels, such as voice calls, email, web chat, and social media, all from a single interface.

**Key features of Cisco Finesse include**


`Multi-channel support:` Finesse allows agents to manage customer interactions from different channels, ensuring a consistent experience across various communication mediums.

`Call control:` Agents can handle inbound and outbound voice calls using features like call transfer, hold, conference, and call recording.

`Integrated agent desktop:` Finesse provides a unified view of customer information, including their interaction history, allowing agents to deliver personalized and efficient service.

`Collaboration tools:` Finesse supports collaboration among agents and supervisors through features like chat, team messaging, and supervisor monitoring capabilities.

`Customization and integration:` Finesse can be customized and integrated with other applications to meet specific business needs. It provides APIs and development tools for building custom workflows and integrations.

`Reporting and analytics:` Finesse offers reporting and analytics capabilities to track contact center performance, monitor agent productivity, and gather insights for continuous improvement.

Finesse Desktop URL : https://<fqdn-of-uccx>:8445

> ***PS :*** Agent phone must add to RmCm Application User controled device.

![](images/2023-07-11-23-43-57.png)

**Finesse Administration**

**Disable chat**

```xml
          <!--
	        <headercolumn width="50px">
                <component id="chat">
                    <url>/desktop/scripts/js/chat.component.js</url>
                </component>
            </headercolumn>
          -->
```
![](images/2023-07-12-00-19-51.png)

**Add Title**

You can edit the title with changing this parameter:

```xml
<config key="title" value="Cisco Finesse"/>
```
![](images/2023-07-12-00-17-01.png)

**Add Logo**


For adding `LOGO` you need `3rd party gadget` credential. Firtly you should reset this user with below command

```
utils reset_3rdpartygadget_password
```
after this, connect `UCCX` with this user over winSCP and upload `logo` to directory. (jpeg,png)

![](images/2023-07-12-00-46-22.png)

then, customize the XML file like below

```xml
<config key="logo" value="/3rdpartygadget/files/50logo.jpeg"/>
```

**Workflow**

Firstly configure pop-up URL on `workflow` Finnesse Admin panel on UCCX. 

![](images/2023-07-12-22-51-23.png)

then, determine the condition for pop-up

![](images/2023-07-12-22-54-11.png)

lastly add this flow to team

![](images/2023-07-12-22-56-26.png)

**Finnesse Supervisor Screen**

Enable `advanced capabilities` on Finnesse Administrator screeen.

```xml
<!--
			The following gadget provides Supervisor with advanced capabilities. 
			Using this gadget, supervisors can manage Queues, Prompts, Calendars, and so on. 
			Before including this gadget in Desktop Layout, 
			ensure that the advanced capability is enabled in Unified CCX Administration.
-->
            <tab>
                <id>ASCGadget</id>
                <icon>admin</icon>
                <label>finesse.container.tabs.supervisor.advancedcapabilities</label>
                <columns>
                    <column>
                        <gadgets>
                            <gadget>https://localhost:8445/ascgadget/gadgets/ascgadget.xml</gadget>
                        </gadgets>
                    </column>
                </columns>
            </tab>
```

then give permission to `Supervisor` for manage prompt, application or calendar...

![](images/2023-07-13-13-11-31.png)

## CUIC (Reporting)

## Troubleshoot of UCCX

some `cli commands` which help to troubleshoot:

```bash
file dump install system-history.log
show network eth0 details
show tech network hosts
utils diagnose test
show process load
```










































