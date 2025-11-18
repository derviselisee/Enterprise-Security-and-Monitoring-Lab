## Enterprise-Security-and-Monitoring-Lab

#Enterprise Security and Monitoring Lab with AD, LDAP, Wazuh, Zabbix, GLPI, and Kali Linux

## Lab Setup Overview

My homelab is built to mirror how a real company structures its network, security, and authentication systems. 
Each virtual machine plays a dedicated role that helps me test enterprise concepts such as identity management, threat detection, monitoring, and firewall security.**
<img width="826" height="394" alt="Screenshot 2025-11-17 224826" src="https://github.com/user-attachments/assets/81c0de4e-002e-4c4b-83dd-2729a3991582" />

Ubuntu Server

I use Ubuntu as the main platform for GLPI and Zabbix. Ubuntu provides a reliable foundation for IT asset management, helpdesk operations, and infrastructure monitoring. 
This allows me to simulate how organizations track devices, manage tickets, and monitor system health.

Debian Server

My Debian server runs Wazuh, which acts as the central SIEM and endpoint security platform. It collects logs, analyzes activity, and detects threats across the network. 
This system helps me practice real SOC workflows such as threat hunting, alert review, and incident response.

Windows Server 2022

This server is configured as my domain controller for Active Directory. It manages user accounts, groups, authentication, and directory services for my entire environment.
I rely on it for LDAP, Kerberos, Group Policy, and future FSSO integration. Because of this, it becomes the foundation for identity based security and centralized administration.

Windows 10

My Windows 10 machine simulates a standard employee workstation. It helps me test domain logins, GPOs, endpoint monitoring, application behavior, and normal user activity inside a company network.

Windows 7

This system acts as a vulnerable workstation for security testing. I use it to simulate attacks, exploit attempts, and malware behavior. 
It allows me to validate how Wazuh, Zabbix, and the firewall respond to risky or suspicious activity.

Kali Linux

Kali is my penetration testing machine. It allows me to generate controlled attacks such as brute force attempts, scans, exploits, and lateral movement. 
This creates realistic security events that I can analyze in my SOC tools.

FGT-HQ

FGT-HQ is the primary FortiGate firewall that secures the entire lab. It handles routing, NAT, SD-WAN, identity based policies, IPS, and monitoring.
It represents the main corporate firewall in an enterprise environment.

MY-FORTIGATE

This second FortiGate appliance is dedicated to High Availability testing. 
I use it to configure and validate HA behavior such as redundancy, synchronization, failover, and heartbeat monitoring.


## MISSION CONTEXT

This project recreates a full enterprise network environment that combines identity services, firewall security, SD WAN, high availability, endpoint monitoring, and threat detection. 
The goal is to design and operate a multi platform ecosystem where Windows and Linux clients authenticate through centralized identity systems, security logs are collected and analyzed,
and FortiGate firewalls protect and monitor traffic. The lab simulates how real SOC and network engineering teams work together to manage authentication, system health, m
monitoring, and incident detection across a modern enterprise network.

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

TOOLS AND TECHNOLOGIES USED

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

PURPOSE OF THIS PROJECT

The purpose of this project is to build a complete enterprise style security and monitoring environment that mirrors how real SOC and network engineering teams operate. 
The lab integrates identity management, firewall security, SIEM, SNMP monitoring, and IT operations systems to provide end to end visibility and control. 
It supports centralized authentication, log analytics, performance monitoring, and incident detection while using simulated attacks to validate security coverage.
This environment strengthens practical skills across Windows, Linux, and FortiGate platforms and provides hands on experience with the technologies commonly used in modern cybersecurity and IT operations.

## For Resume
Enterprise Security and Monitoring Lab

• Built a complete multi system enterprise environment that included a Windows Server domain, 
Windows and Linux clients, LDAP authentication, and identity based visibility through Active Directory and FSSO.

• Deployed FortiGate firewalls in VMware with SD WAN and high availability, configured dual WAN paths, created segmented networks, 
and applied identity based policies while monitoring traffic and sessions through FortiView and security logs.

• Installed and managed Wazuh SIEM on Debian for centralized log collection and alerting, deployed Zabbix and GLPI on Ubuntu Server
for SNMP monitoring and IT asset management, and used Kali Linux to generate simulated attacks that were detected across SIEM and monitoring platforms.

1-FortiGate Virtual Machine Network Setup****
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

2-FortiGate Interface Configuration and WAN Setup

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

3-SD WAN Configuration and Performance Monitoring

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

4-Firewall Policy Configuration

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

5-Testing Connectivity with the Windows Server

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

6-Deploying Windows Server for Active Directory, LDAP, and FSSO

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


















