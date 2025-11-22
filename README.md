## ENTERPRISE SECURITY AND MONITORING LAB 

#Enterprise Security and Monitoring Lab with AD, LDAP, Wazuh, Zabbix, GLPI, and Kali Linux

## Lab Setup Overview

My homelab is designed to mirror how a real company organizes its network, security tools, and authentication systems. 
Each virtual machine has a specific role that helps me practice enterprise concepts such as identity management, monitoring, threat detection, and firewall security. 
This setup allows me to build realistic SOC and IT workflows inside a fully controlled environment.

<img width="363" height="428" alt="Lab setup" src="https://github.com/user-attachments/assets/f217f72c-b8c1-45ca-a2af-1bc3620e113f" />

-Windows Server 2022

This machine serves as my domain controller. It manages Active Directory, DNS, user accounts, groups, and authentication across the network. 
It is the backbone of identity based security in my homelab and supports LDAP and future integrations such as FSSO.

-Windows 10

My Windows 10 virtual machine represents a standard employee workstation.
I use it to test domain logins, Group Policy behavior, endpoint monitoring, and normal user activity inside a corporate network.

-Windows 7

This VM acts as a vulnerable legacy workstation. I use it to simulate outdated systems, test exploit behavior, and generate risky activity.
It allows me to observe how my monitoring and SIEM tools respond to real threats.

-Debian (Wazuh SIEM Server)

This Debian server runs Wazuh, which acts as the central SIEM and endpoint security platform. 
It collects logs from every machine, analyzes activity, and alerts on suspicious events. 
It helps me practice SOC tasks such as threat detection, alert triage, and incident response.

-Ubuntu Server (GLPI and Zabbix)

This Ubuntu Server hosts GLPI for IT asset management and helpdesk operations, and Zabbix for infrastructure monitoring. 
It allows me to simulate how enterprises track devices, manage tickets, and monitor system performance and availability.

-Ubuntu (Client Machine)

I use this Ubuntu desktop VM as an additional client workstation. 
It helps me test cross platform authentication, log collection, agent deployment, and monitoring from a Linux endpoint.

-Kali Linux

Kali is my attacker machine. I use it to generate controlled attacks such as scans, brute force attempts, and exploit activity, 
allowing me to observe how my SIEM, firewall, and monitoring tools detect and respond to real threats.

-FGT HQ (Primary FortiGate)

This is the main FortiGate firewall that secures the entire lab. It handles routing, NAT, security profiles, identity based policies, and traffic inspection. 
It represents the core enterprise firewall in my environment.

-FGT HQ2 (Secondary FortiGate for HA)

This FortiGate is dedicated to High Availability testing. I pair it with the primary firewall to build an Active Passive HA cluster.
It helps me test redundancy, failover behavior, heartbeat communication, and configuration synchronization.


## MISSION CONTEXT
This project recreates a realistic enterprise network designed to integrate identity services, firewall security, SD WAN connectivity, high availability, endpoint monitoring, and threat detection into one unified ecosystem. 
The objective is to build and operate a multi platform environment where Windows and Linux clients authenticate through centralized identity infrastructure, security events are collected and analyzed through SIEM and monitoring tools, and FortiGate firewalls enforce segmentation and protect network traffic. This lab mirrors how modern SOC and network engineering teams collaborate to manage authentication, system performance, monitoring workflows, and incident detection across a fully functional enterprise environment.

## IMPLEMENTATION SUMMARY

Core Infrastructure

• Deployed a Windows Server as the Active Directory domain controller providing DNS, DHCP, and user management.

• Joined a Windows 10 workstation to the domain and added an Ubuntu desktop to represent a Linux client.

• Created an LDAP environment for Linux authentication and enabled FSSO to map domain users to firewall policies.

FortiGate Security, SD WAN, and HA

• Deployed two FortiGate firewalls in VMware to build a high availability cluster.

• Configured SD WAN by assigning Port1 as a bridged WAN link and Port2 as a NAT based WAN link, allowing the firewall to test path quality and select the best route.

• Integrated the FortiGate cluster with Active Directory using LDAP and FSSO to apply identity based firewall policies and monitor user activity.

• Created internal segmentation and enforced controlled access between systems, monitoring all sessions through FortiView and firewall logs.

Security Monitoring and IT Management

• Installed a Debian based Wazuh server to collect logs from Windows, Linux, and FortiGate systems.

• Deployed Zabbix on Ubuntu Server for SNMP based monitoring of devices and system performance.

• Installed GLPI for asset inventory, ticket management, and IT documentation, creating a realistic IT operations workflow.

Threat Simulation and Detection

• Used Kali Linux to perform controlled attacks such as network scanning, credential attempts, and enumeration.

• Verified detection and alert generation through Wazuh, Windows logs, FortiGate security events, and Zabbix monitoring dashboards.

• Validated user mapping, event correlation, and incident triage across the environment.

## SKILLS DEMONSTRATED

• Windows Server administration, Active Directory structure design, user and device management, DNS and DHCP setup.

• FortiGate deployment with SD WAN configuration, high availability setup, and identity based firewall rules using LDAP and FSSO.

• Linux system deployment across Ubuntu and Debian, including service installation and authentication integration.

• SIEM log collection, alerting, and event correlation through Wazuh for Windows, Linux, and firewall activity.

• SNMP based monitoring and alerting using Zabbix for system performance and network visibility.

• IT asset inventory and ticket management using GLPI to replicate enterprise IT workflows.

• Cross platform identity management with LDAP and user mapping through FSSO for security visibility.

• Traffic inspection, log analysis, and session monitoring through FortiView and system logs.

• Simulated attack generation with Kali Linux and detection across SIEM, monitoring dashboards, and firewall logs.

• Enterprise level troubleshooting across networking, firewall, Windows, and Linux environments.

## TOOLS AND TECHNOLOGIES USED

• Windows Server 2019

• Windows 10

• Ubuntu Desktop

• Debian Server

• FortiGate Firewall, SD WAN, High Availability

• Wazuh SIEM

• Zabbix Monitoring

• GLPI IT asset and ticket management

• LDAP

• FSSO

• Kali Linux

• VMware Workstation

• Syslog and SNMP

• FortiView and log analysis tools

## PURPOSE OF THIS PROJECT

The purpose of this project is to design and operate a fully integrated enterprise style network where identity management, firewall security, monitoring, and threat detection work together as a unified system. 
This lab allows me to practice real world workflows by centralizing authentication through Active Directory, enforcing security controls with FortiGate firewalls, and using SIEM and monitoring tools to track system health and detect malicious activity. The project provides a hands on environment that simulates how modern organizations secure their networks, monitor critical assets, and respond to incidents across diverse platforms.

## For Resume
Enterprise Security and Monitoring Lab — Resume Bullet Points

• Designed and deployed a full enterprise grade environment with Active Directory, Windows and Linux endpoints, LDAP authentication, 
and identity based controls that provided end to end visibility across users, devices, and network activity.

• Implemented FortiGate firewalls in VMware with SD WAN and Active Passive HA, configured dual ISP paths, segmented internal networks, a
nd enforced identity based security policies while monitoring real time traffic and events through FortiView and system logs.

• Built a complete SOC style monitoring stack by deploying Wazuh SIEM on Debian for log analysis and alerting, installing Zabbix and GLPI on Ubuntu Server for infrastructure monitoring and asset management,
and generating controlled attacks from Kali Linux to validate detection and response capabilities.

## 1-FortiGate Virtual Machine Network Setup****
<img width="996" height="848" alt="MY-FORTIGATE interfaces" src="https://github.com/user-attachments/assets/78eff0c5-f420-40ef-85d6-c2aa80a4d4ad" />

I configured my FortiGate virtual machine inside VMware Workstation and assigned multiple network adapters in order to build a complete enterprise environment with three internal LANs and two external links for SD WAN testing.

Inside the VM settings, I added several virtual network adapters and mapped each one to a different VMware network. 
This allowed the FortiGate to see each adapter as a separate physical interface. From there, I assigned each interface to a specific purpose inside my lab.

Internal LAN Segments

I created three LAN environments, each with its own adapter and VLAN because I wanted clean segmentation that reflects a real enterprise network.

LAN 1: Employees
This segment is where all regular user systems stay. My Windows workstation is connected here.

LAN 2: Monitoring and SOC
This is the network where I placed Wazuh, Zabbix, GLPI, and other monitoring tools. Keeping them isolated helps protect the monitoring stack and gives me accurate data.

LAN 3: Administration
This network is dedicated to the domain controller and management access. It acts as the secure administrative plane of the environment.

Each LAN is mapped to a different VMware LAN Segment, and each of those segments is assigned to a different FortiGate port.

SD WAN Internet Interfaces

I also prepared two WAN connections so I could test SD WAN features.

Port 1
I assigned port 1 to VMnet0, which is bridged to my actual physical home network. This gives the FortiGate a real internet path from my local router.

Port 2
I assigned port 2 to the NAT network in VMware. This gives the firewall a second, independent internet connection that behaves differently from the bridged one.

Both connections act like two separate internet service providers, which lets me test SD WAN performance, failover, health checks, and traffic steering.

## 2-FortiGate Interface Configuration and WAN Setup

In this part of the lab I focused on configuring the network interfaces of my FortiGate firewall. 
My goal was to recreate a realistic enterprise layout with two independent WAN connections for SD WAN testing and three internal LAN networks that act as separate zones.
I also reviewed the system event logs to confirm that all changes were applied correctly.

 A-WAN Interface Configuration

I configured two different WAN links because I wanted the firewall to simulate a multi provider setup.
This allows me to test SD WAN performance, failover, and routing decisions.

WAN 1

WAN 1 is mapped to port1. It receives an address from my physical home network through DHCP because the interface is connected to the VMware bridged network. 
The firewall successfully obtained an IP address, a default gateway, and DNS information. The interface is up and reachable, which confirms that the link is active.
<img width="1912" height="921" alt="WAN 1 int config" src="https://github.com/user-attachments/assets/208327c5-c46a-42d1-b004-f728c19c5335" />

WAN 2

WAN 2 is mapped to port2. This interface is connected to the VMware NAT network. It also receives its configuration through DHCP. 
This gives the firewall a second independent internet path. Both WAN interfaces are fully operational and ready for SD WAN membership.

<img width="1919" height="923" alt="WAN 2 int configs" src="https://github.com/user-attachments/assets/94cd89d4-c7bc-45dc-8ca9-f87fb7feb785" />

  B-LAN Interface Configuration

I configured three LAN networks because I wanted clear separation between employees, SOC and monitoring systems, and administrative infrastructure.
Each LAN uses manual addressing and runs its own DHCP server inside the firewall.

LAN 1

LAN 1 is assigned to port3 with the subnet 192.168.10.0. I configured the interface as a DHCP server that provides addresses in the range 192.168.10.2 to 192.168.10.50. 
This network represents the employee workspace.
<img width="1910" height="924" alt="Port3 LAN1 config" src="https://github.com/user-attachments/assets/b229af14-5d2a-4696-995a-ef2c98e8349f" />

LAN 2

LAN 2 is assigned to port4 with the subnet 192.168.60.0. It also runs a DHCP server that distributes addresses between 192.168.60.2 and 192.168.60.50.
This network hosts my SOC and monitoring tools such as Wazuh, GLPI, and Zabbix.
<img width="1909" height="924" alt="Port4 LAN2 config" src="https://github.com/user-attachments/assets/1a1f83c7-a3dc-44b3-ab9a-08760e9c94ba" />

LAN 3

LAN 3 is assigned to port5 with the subnet 10.10.10.0. I set the DHCP server to provide addresses from 10.10.10.2 to 10.10.10.20.
This segment represents the administrative network for infrastructure and server management.
<img width="1888" height="930" alt="Port5 LAN3 config" src="https://github.com/user-attachments/assets/46422e88-848c-45a7-a81c-993085d9fbe5" />

All three LAN interfaces are up, they have their own address scopes, and they allow the lab machines to receive IP configurations automatically.

C-Reviewing System Events

After applying the configuration, I opened the system event logs to confirm that all changes were recorded successfully.
The logs show interface edits, DHCP server creation, global setting changes, and administrator login activity. 
This helped me verify that every configuration step was correctly applied and recognized by the firewall.
<img width="1907" height="921" alt="Systems Events (Logs)" src="https://github.com/user-attachments/assets/c671aba9-a112-4b09-874c-f4564a14e691" />

## 3-SD WAN Configuration and Performance Monitoring

After finishing the interface configuration for my WAN and LAN networks, I moved on to building the SD WAN setup. 
My goal was to combine my two internet connections into a single virtual link and apply performance monitoring so the firewall could make intelligent routing decisions.

A-Creating SD WAN Members

The first step was to add both WAN interfaces as SD WAN members. I added port1 as WAN1 and port2 as WAN2. 
Both interfaces had working internet connectivity because WAN1 was connected to my physical home network through the bridged mode and WAN2 was connected to the VMware NAT network.
By placing both interfaces inside the virtual SD WAN link, I created a logical path that the firewall would use to manage traffic based on performance.
<img width="1861" height="712" alt="SD-WAN members" src="https://github.com/user-attachments/assets/3727d147-6e0f-43d2-b771-8cba79ac98d2" />

B-Setting Up the Performance SLA

Once the members were created, I configured a performance SLA to measure latency, jitter, and packet loss.
I named it “Ping Google DNS” because I used two reliable public DNS servers as targets: 8.8.8.8 and 1.1.1.1.

I chose active probe mode and used the ping protocol because it gives consistent results for basic link quality.
I applied the SLA to both WAN connections so the firewall would check each link independently.

To create realistic thresholds, I configured values for latency, jitter, and packet loss.
I also set the failure and recovery counts because I wanted the link to be marked inactive only after several failed probes, not after a single bad response.
<img width="1556" height="894" alt="Performance SLAs configs" src="https://github.com/user-attachments/assets/c97ea49c-d094-41b6-aac1-80cd3223ba1e" />

C-Observing Performance Results

After enabling the SLA, I opened the performance dashboard to watch both WAN links in real time. 
The firewall displayed packet loss, latency, and jitter for each interface. Both connections remained stable with zero packet loss and very low jitter.
Latency averaged around fifteen milliseconds on both links because they both had direct access to the internet.

Seeing these metrics confirmed that both WAN paths were healthy and that the SD WAN logic had accurate data to use for routing decisions.
<img width="1911" height="700" alt="SD-WAN latency performance" src="https://github.com/user-attachments/assets/8d8cc322-de34-40f0-8f23-b61b5bf65563" />
<img width="1914" height="664" alt="SD-WAN jitter perfomance" src="https://github.com/user-attachments/assets/fbdf2b99-6fba-4f03-9634-def90bde74ed" />

D-DNS Configuration

After completing the SD WAN setup and before moving into firewall policies, I configured the DNS settings on the FortiGate. 
I wanted the firewall to use reliable public DNS servers for name resolution because this helps with faster lookups, stability, and accurate health checks for the SD WAN performance monitoring.

I specified Google DNS as both the primary and secondary DNS servers by using the address 8.8.8.8. The firewall displayed the lookup time beside each entry, which confirmed that the DNS queries were working correctly. 
I also reviewed the dynamically obtained DNS information coming from both WAN interfaces. WAN1 received its DNS address from the bridge connection on my home network, while WAN2 received its DNS address from the VMware NAT network.
This allowed me to compare the latency on each link. WAN2 responded much faster because it was directly connected to the VMware NAT resolver, while WAN1 had higher latency since it depended on the physical router.

By configuring static DNS servers and reviewing dynamic DNS information, I made sure the firewall always has consistent name resolution even if one WAN path becomes unstable. This helps improve SD WAN reliability, especially for SLA probes that depend on DNS.
<img width="1702" height="921" alt="DNS Server" src="https://github.com/user-attachments/assets/18049bc8-4b19-4e2c-8e3b-d4a82809b408" />


E-Creating the Static Route

With the SD WAN link operating correctly, I created the default route that sends all outbound traffic through the virtual WAN interface.
I configured a static route with the destination 0.0.0.0 and selected the SD WAN link as the outgoing interface. This allowed the firewall to use its performance monitoring to choose the best link at any moment.

By doing this, the firewall will automatically route traffic through the WAN link that meets the SLA requirements and fail over smoothly if one path experiences delays or drops.
<img width="1469" height="666" alt="Static Route config" src="https://github.com/user-attachments/assets/936dc79f-e4b7-431c-9342-e405cc0fdc25" />
<img width="1858" height="442" alt="Static Route (sdwan link)" src="https://github.com/user-attachments/assets/85e98f9f-540a-4a03-bba5-06093b6e0194" />

## 4-Firewall Policy Configuration

Once the SD WAN link was fully configured and the default route was in place, I created the firewall policies that allow my internal networks to reach the internet.
Each LAN segment needed its own policy because I built three separate networks for employees, SOC and monitoring systems, and administrative devices. I wanted clear traffic control for each zone while still pointing all outbound traffic toward the SD WAN virtual interface.

LAN 1 to Internet

The first policy connects the employee network on port3 to the virtual SD WAN link. The source and destination are set to all, and the schedule is always active. 
I enabled NAT because I want internal devices to use the outgoing interface address. This allows LAN 1 clients to access external resources through whichever WAN link the SD WAN decides is the best path.
<img width="1740" height="918" alt="Firewall Policies 1" src="https://github.com/user-attachments/assets/3617e96c-c44a-4a92-8e4c-b6f8aa5a1541" />

LAN 2 to Internet

The second policy connects the SOC and monitoring network on port4 to the virtual SD WAN link.
I used the same configuration settings because this network also needs open internet access for updates, package installation, and integrations such as Wazuh and Zabbix. NAT is enabled and the inspection mode uses the default flow based method.
<img width="1284" height="923" alt="FW Policies 2" src="https://github.com/user-attachments/assets/28e832e5-c34b-4e8d-bfc3-7bbaf9cab971" />

Administrative Considerations

I did not apply any security profiles yet because the focus at this stage was basic connectivity. Later in the project I will enable profiles such as web filtering, application control, and IPS when I start testing security and logging. For now, the policies ensure clean outbound communication from each LAN to the internet while maintaining control over which zones are allowed to exit the network.

Result

With these policies in place, all LAN networks can reach the internet through the SD WAN link. This creates a complete flow from interface configuration, SD WAN setup, DNS, static routing, and finally the firewall rules that allow the network to function.
<img width="1919" height="460" alt="Policies" src="https://github.com/user-attachments/assets/c46707ac-8c30-4947-ac04-e4bfc2847595" />

## 5-Testing Connectivity with the Windows Server

After finishing the routing and firewall policy configuration, I deployed a Windows Server 2022 virtual machine to test whether the environment was functioning correctly. 
I connected the server to the correct LAN segment in VMware so it would join the network through the Employees or SOC interface on the FortiGate, depending on the segment I selected.
<img width="1570" height="903" alt="Win-server interfaces 2" src="https://github.com/user-attachments/assets/b53ea09d-8598-4d4c-9ef2-f36b4d306586" />

When the system started, it automatically received its network configuration through DHCP. The server successfully obtained an IP address, its subnet mask, the default gateway, 
and the DNS server from the FortiGate. This confirmed that the internal DHCP service was working properly.
I then opened a command prompt and tested basic connectivity by pinging two important destinations. First, I pinged 8.8.8.8 to confirm that the server could reach the internet through the SD WAN link.
The replies came back with normal latency, which showed that outbound traffic was working. I also pinged the default gateway to verify internal communication between the server and the FortiGate.
Both tests succeeded without any packet loss.
<img width="1716" height="958" alt="Win-server got an address via dhcp and is connected to Internet" src="https://github.com/user-attachments/assets/f4322dda-e7f4-46be-97d4-b6c29ceeeff8" />

Once network connectivity was confirmed, I reviewed the activity of the Windows Server in FortiView on the firewall. The server appeared immediately under the active devices list because it was generating traffic. 
I checked the bandwidth usage, the number of sessions, and the destination IP addresses it was contacting.
<img width="1907" height="497" alt="FortiView win ser" src="https://github.com/user-attachments/assets/904ae65a-8ef2-4126-a59e-f3b721ad6d8d" />
<img width="1919" height="485" alt="FortiView sources for Win-server" src="https://github.com/user-attachments/assets/aaed9564-de03-4e78-b83e-643b8c0ecc96" />

Finally, I opened the forward traffic log to review the individual packets leaving the server. I could see each connection showing the source address, the service used, the outgoing interface,
the destination, and the policy that allowed the traffic. This confirmed that the firewall policies were applied correctly and that the SD WAN link was being used for internet access.
<img width="1916" height="921" alt="Traffic Logs for Win-server" src="https://github.com/user-attachments/assets/15ac341d-842a-406e-a9df-d724e1c89fcb" />

This test validated the entire setup. The LAN configuration, DHCP services, DNS settings, SD WAN routing, firewall rules, and monitoring tools all worked together exactly as intended.

## 6-Deploying Windows Server for Active Directory, LDAP, and FSSO

A-I deployed a Windows Server virtual machine because it plays a central role in any enterprise network.
Windows Server acts as the backbone of identity, authentication, and centralized management in a company. It provides services that allow employees to log in securely, access shared resources, and follow company wide policies.
I set up this Windows Server as a full Domain Controller and created my own domain named dervis.lab.
<img width="1714" height="956" alt="I created my AD Domain (dervis lab)" src="https://github.com/user-attachments/assets/82608e63-d475-4527-a2ff-2e8645107a7e" />

B-After promoting the server to a Domain Controller, I configured Active Directory Domain Services, which allowed me to introduce LDAP based authentication and prepare the environment for FSSO integration with my FortiGate. 
I also designed the organizational structure by creating several Organizational Units for IT, HR, Finance, and Managers. Each OU contains user accounts that match real company departments.
<img width="1715" height="927" alt="I created 4 differents OUs and their users  ( IT,HR,FINANCE and Managers)" src="https://github.com/user-attachments/assets/b924085e-4847-4a98-8214-c3bdb128fabe" />
I added user accounts inside their appropriate OUs, which allows each user to inherit the correct department based policies.
Creating multiple users helps simulate a real company network and prepares everything for LDAP authentication and future FSSO testing.

C-I configured another user account inside Active Directory by defining the username, domain logon format, and password requirements. 
This ensures that identity services are working correctly on the Domain Controller and confirms that my AD environment is ready for integration with other systems like FortiGate and GLPI.
<img width="983" height="687" alt="AD user account 2" src="https://github.com/user-attachments/assets/527e5987-682a-4cc6-a824-ca1283df61db" />
<img width="990" height="668" alt="AD (an user account)" src="https://github.com/user-attachments/assets/10682abe-f0d8-4bca-a491-40426d2f7f59" />

This layout creates a strong foundation for identity management across the entire lab.
It allows me to centralize authentication through LDAP and Kerberos.
It improves how users, departments, and permissions are organized.
It also supports identity driven firewall policies on the FortiGate.
This structure mirrors how real companies manage access and user security.
It prepares the environment for upcoming authentication labs, including full FSSO integration.


## 7-Joining the  Windows 10 Client to the Active Directory Domain (dervis.lab)

This how I deployed, configured, and validated a full Active Directory environment using Windows Server 2022 and a Windows 10 client. 
The goal was to create the domain dervis.lab, join a workstation to that domain, and verify that domain based authentication works as expected. This is part of my enterprise homelab where identity, security, 
and network management all connect.

A-Deploying and Preparing the Domain Controller

I began by deploying a Windows Server 2022 virtual machine inside my homelab. The server received its IP address from my FortiGate DHCP service. 
I verified the network configuration with the ipconfig command. The server had the IPv4 address 192.168.60.2 with the gateway 192.168.60.1.

Once connectivity was confirmed, I installed the Active Directory Domain Services role and promoted the server to a Domain Controller. During the promotion process, 
I created the new domain which is called dervis.lab. After a reboot, the server became the first Domain Controller in the environment.

To organize the domain in a way that reflects real enterprise structure, I used Active Directory Users and Computers to create OUs for IT, HR, Finance, Managers, and Users. 
This gives me a clean and organized space for authentication, access control, and future Group Policy deployment.
<img width="1648" height="959" alt="Windows Server configs" src="https://github.com/user-attachments/assets/f89228d1-018b-4c1e-98e1-e0a4e7f73966" />
<img width="845" height="569" alt="no computers joined the domain yet" src="https://github.com/user-attachments/assets/ec9a797f-8331-4613-b0f5-9008381ae12a" />


B-Preparing the Windows 10 Client

Next, I deployed my Windows 10 client that will serve as a domain joined workstation. The client obtained its IP address from my FortiGate DHCP service automatically.
Its configuration showed the IPv4 address 192.168.10.3 with the gateway 192.168.10.1.

Since Active Directory requires clients to use the Domain Controller as their DNS server, 
I modified the Windows 10 network settings. I changed the DNS server to 192.168.60.2 so the workstation could resolve domain records from the Domain Controller directly. 
This step is critical because domain join requests depend on DNS service from the Domain Controller.
<img width="1639" height="922" alt="I changed the dns settings of my  Win 10 client so I can join the domain" src="https://github.com/user-attachments/assets/7c924210-d155-449d-95e2-f05ed11115df" />
<img width="1649" height="952" alt="Windows 10 configs" src="https://github.com/user-attachments/assets/92bd1376-4ce8-4bff-8bfe-54236cc55889" />

C-Joining the Windows 10 Client to dervis.lab

I opened the Access Work or School settings on the Windows 10 machine and selected the option to join a domain. I entered dervis.lab and provided the domain Administrator credentials.
The client contacted the Domain Controller, authenticated successfully, and added the computer account to Active Directory.

The system confirmed a successful join and requested a reboot. After restarting, the login screen displayed the domain sign in option with the prefix DERVIS.
This confirmed that the system recognized the domain environment and was ready for domain based logins.

Inside Active Directory Users and Computers, I saw the workstation registered automatically under the Computers container as DERVIS PC1.
<img width="1645" height="954" alt="Windows 10 client is joining the domain(dervis lab)" src="https://github.com/user-attachments/assets/38db022b-c2b5-435e-97eb-9b247df5c2f7" />
<img width="1640" height="970" alt="Win 10 client successfully joined the domain" src="https://github.com/user-attachments/assets/1a93f4b0-bd89-4496-b2b9-95c12b672653" />
<img width="1644" height="954" alt="we can see our win 10 client has joined the domain" src="https://github.com/user-attachments/assets/e493ae46-1e5a-4665-bf9b-4be6feb68a4c" />

D-Testing Domain Authentication with a Domain User

To confirm that the domain join was fully functional, I created a domain user account named Man Dervis.
I assigned this user a password and placed the account inside my Users container.

On the Windows 10 machine, I attempted to sign in using the domain credentials for Man Dervis. 
The workstation authenticated the user against the Domain Controller successfully and completed the login process.
The session loaded with the identity DERVIS mandervis, which confirmed that the workstation trusts the Domain Controller and accepts domain user authentication.

This test proved that the domain join was successful and that the workstation and Domain Controller communicate correctly for authentication, authorization, and identity handling.
<img width="1646" height="920" alt="man dervis the user" src="https://github.com/user-attachments/assets/a1fad94a-a39f-4e47-977b-e96f0c466563" />
<img width="1642" height="955" alt="user ( Man Dervis) is connecting" src="https://github.com/user-attachments/assets/67beed17-2eb7-4032-926b-53f60fb0d3a7" />
<img width="1643" height="950" alt="Man Dervis ( an user) has successfully log in the desktop " src="https://github.com/user-attachments/assets/d092c80e-dad6-4aad-ac34-6ec94ece00ef" />

E-Summary

By completing these steps, I built a functional Active Directory environment and validated domain based authentication end to end.
I deployed a Domain Controller, created the domain dervis.lab, organized the directory with proper OUs, prepared a Windows 10 client, configured DNS for domain resolution, 
joined the client to the domain, and verified that a domain user could log in successfully. This workflow reflects real world enterprise identity and access management practices.

## 8-Deploying  High Availability Cluster (Active Passive)

In this part of my homelab build, I deployed a secondary FortiGate virtual appliance and configured a full high availability (HA) Active Passive cluster.
My goal was to simulate a real enterprise firewall environment where redundancy, failover, heartbeat links, and monitored interfaces are essential for maintaining uptime.
I configured VMware networking, prepared the management and heartbeat ports, verified communication, and then synchronized both units into a stable HA pair.

A-Deploying the Secondary FortiGate and Preparing VMware Networking

I began by deploying the second FortiGate VM in VMware Workstation. I assigned its hardware resources and then configured its network adapters to match the primary unit.

Management Interface (Port 10)

I set port10 to Bridged mode. This allowed me to reach the secondary FortiGate from my laptop using its assigned management IP address. 
Once the system booted, I configured port10 to allow http, https, ping, and ssh, which made remote access easier.

Heartbeat Interfaces (Port 7 and Port 8)

I set ports 7 and 8 to VMnet2, an isolated virtual network that exists only between the FortiGate appliances. These two interfaces would later serve as the heartbeat links for the cluster.
<img width="1269" height="842" alt="FGT secondary interfaces config" src="https://github.com/user-attachments/assets/5fb2b0b2-8f25-4e8b-b520-1534b4de9a17" />
<img width="913" height="871" alt="FGT 2 configs" src="https://github.com/user-attachments/assets/74cecdf4-6530-4de8-92d5-fa531036d40b" />

I configured the primary FortiGate the same way by placing its ports 7 and 8 in VMnet2. 
This ensured that both appliances shared the same isolated network for heartbeat communication and could exchange cluster health and synchronization traffic reliably.
<img width="878" height="799" alt="FGT-HQ interfaces ( Ports 7 and 8 are heartbeat)_" src="https://github.com/user-attachments/assets/2cd47ae9-4891-407d-b672-625bb04306db" />

B-Understanding Heartbeat Interfaces and Why They Matter

Heartbeat interfaces are dedicated links used exclusively for internal cluster communication.
They allow both firewalls to check each other’s health in real time. When heartbeats stop, the cluster triggers a failover to maintain service availability.

Heartbeat interfaces are important because they carry:

-Health status checks

-Cluster control traffic

-Configuration synchronization

-Session synchronization (if session pickup is enabled)

Without reliable heartbeat links, the HA cluster cannot function correctly. Ports 7 and 8 in VMnet2 created a private, stable communication channel for the two FortiGates.

C-Verifying Communication Between Both Firewalls

Before forming the cluster, I verified that both FortiGates could reach each other.
I used the CLI on each appliance and sent ping tests across the heartbeat network:

execute ping <peer-IP>

Both appliances responded successfully with zero packet loss. This confirmed that VMnet2 was working and that the heartbeat network was healthy.
<img width="1916" height="1036" alt="both FGT can communicate " src="https://github.com/user-attachments/assets/dc7436cb-b7bf-4065-b80e-3000a630051d" />

D-Configuring the HA Cluster

Once communication was confirmed, I configured the HA cluster on both appliances using matching settings.

Cluster Configuration Details

-Mode: Active Passive

-Group Name: HA CLUSTER

-Password: redundancy

-Primary Priority: 150

-Secondary Priority: 125

-Heartbeat Interfaces: port7 and port8

-Session Pickup: Enabled

After configuring these settings on the primary, I applied the same configuration to the secondary.
The two units immediately synchronized, exchanged heartbeat signals, and formed a stable HA cluster.

I also added the following interfaces as monitored interfaces:

WAN1 (port1)

WAN2 (port2)

Employees (port3)

SOC and NOC (port4)

Admins (port5)

What monitored interfaces are and why they matter

Monitored interfaces help the cluster detect link failures. If a monitored interface goes down, the cluster can trigger a failover to the secondary unit. 
This prevents outages and ensures that the firewall with the healthiest network path becomes the active device.

This mirrors exactly how production networks maintain high uptime.
<img width="1912" height="923" alt="HA cluster configurations on both FGTs" src="https://github.com/user-attachments/assets/7ce93b07-dc92-40e4-8a0d-dabd8cb6ab17" />
<img width="870" height="500" alt="synchronization" src="https://github.com/user-attachments/assets/7d541624-2a7e-4dad-b51b-7e081be231f0" />
<img width="1919" height="1033" alt="HA CLUSTER properly configured" src="https://github.com/user-attachments/assets/fe68e15d-6bc9-4e21-838d-5403cde8843a" />
<img width="1903" height="782" alt="HA Logs" src="https://github.com/user-attachments/assets/bbb91f5b-2a01-4992-afcd-52e7a365d8a8" />
<img width="1914" height="922" alt="systems HA status" src="https://github.com/user-attachments/assets/7ae4c61e-bc1f-4ad5-ba5c-986ced3f0484" />

E-Final State and Validation
I checked the interface configurations on both FortiGate appliances and confirmed that every port matches exactly.
The IP addresses, administrative access settings, and network mappings are identical on both units, which means the HA cluster synchronized the interface settings correctly.
This consistency shows that the secondary unit fully inherited the primary’s configuration and that both firewalls now operate as one unified system.
<img width="1910" height="923" alt="HQ Primry Interfaces" src="https://github.com/user-attachments/assets/b4bd57eb-4d29-49b2-860c-f502303a8193" />
<img width="1915" height="927" alt="HQ Secondary Interfaces   they are exactly the same " src="https://github.com/user-attachments/assets/88b83281-a926-4410-9b71-58d97574cf6d" />

Once both units synchronized, I checked the HA Monitor dashboard. The cluster showed:

Primary: FGT HQ

Secondary: FGT HQ

Status: Synchronized

Heartbeat: Healthy

Monitored Interfaces: All active

Both FortiGates now behave as a single unified firewall. 
Any configuration change on the primary automatically syncs to the secondary. The cluster will fail over smoothly if the primary becomes unavailable.
<img width="1915" height="661" alt="HA cluster ( Primary)" src="https://github.com/user-attachments/assets/b1b51e41-5a27-4205-8f92-48d9be132d89" />
<img width="1668" height="567" alt="secondary FGT" src="https://github.com/user-attachments/assets/7ba4d6b6-ff72-463b-bd7b-a86138cd5cea" />









































