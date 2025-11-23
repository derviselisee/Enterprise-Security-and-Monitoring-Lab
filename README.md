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

-Ubuntu Server (GLPI, Zabbix and Wazuh )

This Ubuntu Server hosts GLPI for asset management and helpdesk operations, and it also runs Zabbix to monitor system performance.
Because of that, I can simulate how real organizations track devices, manage tickets, and keep visibility over their infrastructure.

The server also runs Wazuh as my SIEM platform. It collects logs from all machines, analyzes activity, and alerts me about suspicious events.
This helps me practice core SOC skills such as threat detection and incident response.

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
The objective is to build and operate a multi platform environment where Windows and Linux clients authenticate through centralized identity infrastructure, security events are collected and analyzed through SIEM and monitoring tools, and FortiGate firewalls enforce segmentation and protect network traffic. 
This lab mirrors how modern SOC and network engineering teams collaborate to manage authentication, system performance, monitoring workflows, and incident detection across a fully functional enterprise environment.

## IMPLEMENTATION SUMMARY

   ## Core Infrastructure

• Deployed Windows Server 2022 as the Active Directory domain controller for DNS, DHCP, and centralized identity services.
• Joined a Windows 10 workstation to the domain and added an Ubuntu Desktop as a Linux client for cross platform testing.
• Configured LDAP and FSSO so the FortiGate can authenticate users and enforce identity based firewall policies.

  ## FortiGate Security, SD WAN, and HA

• Deployed two FortiGate firewalls in VMware to create a high availability pair.
• Configured SD WAN with one bridged WAN link and one NAT based WAN link for path selection and link quality monitoring.
• Integrated the FortiGate cluster with Active Directory using LDAP and FSSO for real time identity based control.
• Built internal segmentation and monitored all user activity through FortiView and firewall logs.

   ## Security Monitoring and IT Management

• Installed a Wazuh server on Ubuntu for centralized SIEM, log analysis, and security event correlation.
• Deployed Zabbix to monitor servers, network devices, and performance metrics using SNMP and Zabbix Agents.
• Installed GLPI to manage inventory, documentation, and helpdesk workflows within the environment.

   ## Azure Hybrid Cloud Integration

• Deployed a FortiGate VM in Microsoft Azure alongside a Windows client in the same virtual network.
• Configured a custom route table so the Azure Windows VM routes all outbound traffic through the Azure FortiGate for inspection.
• Built a site to site IPsec VPN between the on premises FortiGate and the Azure FortiGate to unify both environments.
• Enabled OSPF across the tunnel to automatically exchange subnets and maintain synchronized routing.
• Used Azure Bastion for secure, clientless remote access to the cloud VM without exposing RDP to the internet.

   ## Threat Simulation and Detection

• Used Kali Linux to simulate port scans, brute force attempts, enumeration, and other adversarial techniques.
• Verified detections through Wazuh alerts, FortiGate security logs, Windows event logs, and Zabbix performance spikes.
• Confirmed full event correlation, identity mapping, and incident triage across the entire hybrid environment.


## SKILLS DEMONSTRATED

• Windows Server administration, including Active Directory design, OU structuring, DNS and DHCP configuration, and domain joined workstation management.

• FortiGate engineering, covering SD WAN setup, high availability deployment, routing, segmentation, NAT, and identity based firewall enforcement using LDAP and FSSO.

• Linux system administration on Ubuntu Server and Ubuntu Desktop, including service installation, SSH based management, and integration with authentication and monitoring systems.

• SIEM operations with Wazuh, including agent deployment, log ingestion, rule based alerting, and correlation of Windows, Linux, and firewall events.

• Performance and availability monitoring with Zabbix, using SNMP and Zabbix Agents to track devices, servers, and network health.

• IT asset and operations management with GLPI, including inventory tracking, helpdesk ticketing, and documentation workflows.

• Identity integration across platforms, combining LDAP authentication with FSSO real time user mapping for visibility and policy enforcement.

• Network traffic inspection and log analysis through FortiView, event logs, Syslog forwarding, and security monitoring dashboards.

• Threat simulation and detection, using Kali Linux to conduct scanning, enumeration, and intrusion attempts validated through SIEM and firewall logs.

• Enterprise troubleshooting, including multi layered debugging across networking, firewalls, Windows, Linux, hybrid cloud, and security monitoring components.


## TOOLS AND TECHNOLOGIES USED

  ## -Operating Systems 💻

• Windows Server 2022 (Primary Domain Controller/Identity)

• Windows 10 (Domain Client)

• Ubuntu Desktop (Linux Client)

• Ubuntu Server (Monitoring/SIEM Host)

  ## -Security and Monitoring 🛡️

• Wazuh SIEM: Security monitoring, log collection, and threat detection.

• Zabbix: Performance monitoring, resource usage tracking, and alerting.

• GLPI: IT asset management, documentation, and helpdesk ticketing.

• Kali Linux: Attack simulation and security validation testing.

• FortiView & Log Analysis Tools: Real-time visualization and interpretation of security logs.

  ## -Networking and Security Protocols 🌐

• FortiGate Firewall (VM): Central security enforcement, routing, segmentation, and inspection.

• LDAP: Integration for user authentication against Active Directory.

• FSSO (Fortinet Single Sign On): Automatic identity mapping for user-based policies.

• SNMP & Syslog: Protocols for forwarding performance metrics and security logs, respectively.

• OSPF: Routing protocol enabling automatic subnet exchange between firewalls.

• IPsec VPN: Used for the site-to-site tunnel connecting the hybrid environment.

  ## -Cloud and Virtualization ☁️

• Microsoft Azure: Hosts the cloud portion of the lab (FortiGate VM and client).

• Azure Bastion: Provides secure remote access to cloud resources without exposing RDP.

• VMware Workstation: The core virtualization platform used to host the entire on-premises lab.

  ## -Administration Tools ⚙️

• SecureCRT: Client used for remote command-line management.

• SSH (Secure Shell): Protocol used for secure remote administration of Linux hosts.

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

## FortiGate Network Setup

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

-LAN 1 to Internet

The first policy connects the employee network on port3 to the virtual SD WAN link. The source and destination are set to all, and the schedule is always active. 
I enabled NAT because I want internal devices to use the outgoing interface address. This allows LAN 1 clients to access external resources through whichever WAN link the SD WAN decides is the best path.
<img width="1740" height="918" alt="Firewall Policies 1" src="https://github.com/user-attachments/assets/3617e96c-c44a-4a92-8e4c-b6f8aa5a1541" />

-LAN 2 to Internet

The second policy connects the SOC and monitoring network on port4 to the virtual SD WAN link.
I used the same configuration settings because this network also needs open internet access for updates, package installation, and integrations such as Wazuh and Zabbix. NAT is enabled and the inspection mode uses the default flow based method.
<img width="1284" height="923" alt="FW Policies 2" src="https://github.com/user-attachments/assets/28e832e5-c34b-4e8d-bfc3-7bbaf9cab971" />

Administrative Considerations

I did not apply any security profiles yet because the focus at this stage was basic connectivity. 
Later in the project I will enable profiles such as web filtering, application control, and IPS when I start testing security and logging. For now, 
the policies ensure clean outbound communication from each LAN to the internet while maintaining control over which zones are allowed to exit the network.

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

## 6-Deploying Windows Server for Active Directory

A-I deployed a Windows Server virtual machine because it plays a central role in any enterprise network.

Windows Server acts as the backbone of identity, authentication, and centralized management in a company. 
It provides services that allow employees to log in securely, access shared resources, and follow company wide policies.
I set up this Windows Server as a full Domain Controller and created my own domain named ## dervis.lab.

<img width="1714" height="956" alt="I created my AD Domain (dervis lab)" src="https://github.com/user-attachments/assets/82608e63-d475-4527-a2ff-2e8645107a7e" />

B-After promoting the server to a Domain Controller, I configured Active Directory Domain Services, 
which allowed me to introduce LDAP based authentication and prepare the environment for FSSO integration with my FortiGate. 
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

## Deploying LDAP Authentication with Windows Server and FortiGate

In this part of my homelab project, I connected my FortiGate firewall to my Windows Server Active Directory so it could authenticate users through their domain accounts.
This approach matches real enterprise environments because it allows the firewall to identify who is on the network and apply access control based on identity rather than only on IP addresses.
My goal was to create a foundation for user based security, monitoring, and future FSSO testing.

A-Creating and Configuring the LDAP Server

I prepared the Windows Server Domain Controller by confirming that Active Directory was fully operational under the domain name dervis.lab.
I created several users inside my organized OU structure and also created a dedicated LDAP bind account. 
This account allows FortiGate to query the directory securely whenever authentication is required.
<img width="1715" height="927" alt="I created 4 differents OUs and their users  ( IT,HR,FINANCE and Managers)" src="https://github.com/user-attachments/assets/cca92b93-8991-4d7f-ad46-2ee2b7702777" />
<img width="1645" height="953" alt="creation of an special user for LDAP server" src="https://github.com/user-attachments/assets/1fe92dfb-a3c1-4d81-aad9-21b99198ee0a" />

On the FortiGate, I created an LDAP server entry and configured the following key settings:

• Windows Server address and proper service port
• sAMAccountName as the username format
• Distinguished Name set to DC=dervis, DC=lab
• Regular bind using the account DERVIS ldapbind

I tested the connection and received a successful result, which confirmed that the firewall and Domain Controller were communicating correctly.
<img width="1919" height="709" alt="LDAP Server created successfully" src="https://github.com/user-attachments/assets/a218ec09-6d66-48ad-804f-1a95ddee9e0b" />

B-Importing Domain Identities into the Firewall

Once the LDAP connection was verified, I opened the User Definition section on the FortiGate. The firewall displayed all my Active Directory accounts, which proved that the directory lookup was functioning the way it should. 
I selected several users and imported them so the firewall could recognize them by name and enforce identity based rules.
<img width="1914" height="515" alt="FGT Users Groups" src="https://github.com/user-attachments/assets/059ede8d-fc21-4e88-a151-7ea11dc690f2" />

C-Creating the Remote Users Group

To organize access control, I created a user group called Remote Users. I added the imported Active Directory accounts into this group. 
This step is important because it gives the firewall a simple way to reference domain users inside security policies. It also mirrors how companies structure role based access across their networks.

<img width="1913" height="824" alt="I created a group named (Remote Users)  FortiGate will verify their credentials , apply policies based on the user not just ip" src="https://github.com/user-attachments/assets/ad6b99c6-9048-48a5-8a4e-ad390fb0bbe3" />

D-Testing LDAP Authentication with a Domain User

To validate everything, I joined my Windows 10 client to the dervis.lab domain and logged in using one of the domain accounts.
The authentication succeeded on the workstation, and the FortiGate immediately recognized the user identity in FortiView. I was able to see traffic, sessions, and activity tied directly to the correct username.
I then added the Remote Users group to my LAN to Internet firewall policy. This allowed the FortiGate to permit or restrict traffic based on the authenticated user rather than only the workstation IP address.
<img width="1917" height="925" alt="now I edited my firewall policy to add the remote user group" src="https://github.com/user-attachments/assets/ca27975c-d6df-4625-9281-42c6b23ef202" />

I also expanded my testing by using the user Sara. I simulated her logging into the domain computer and browsing the internet. 
The FortiGate displayed her identity in real time, which confirmed that LDAP was working correctly and that the firewall could monitor user level activity.

<img width="1647" height="954" alt="lets test the ldap server with the user (Sara )" src="https://github.com/user-attachments/assets/80b72645-a71b-44bd-aa4e-2bf9bcb649b2" />
<img width="1653" height="957" alt="TEST USER" src="https://github.com/user-attachments/assets/0c6d7059-4242-4112-b755-eaffdb9c1a66" />
<img width="1642" height="955" alt="the user Sara has successfully logged into " src="https://github.com/user-attachments/assets/b067414c-5a8f-4723-a062-56cb170de649" />
<img width="1917" height="692" alt="Thank to LDAP , I can see my user&#39;s activities now " src="https://github.com/user-attachments/assets/eda87897-87be-4df3-a08d-2bf2ccf163ca" />

 At the same time, I tested my Ubuntu machine. Since Ubuntu is not joined to the domain, the FortiGate redirected it to the authentication page. 
 This behavior showed that the firewall enforces identity based controls even for non domain devices.
 <img width="1548" height="957" alt="ldap is working properly on ubuntu" src="https://github.com/user-attachments/assets/85f075cc-6dbb-4164-a586-08f90b02b176" />

 E-Summary of the Implementation

Through this setup, I successfully integrated FortiGate with my Active Directory using LDAP.
I configured the bind account, connected the firewall to the domain, imported users, created a Remote Users group, and tested user authentication from a domain joined workstation. 
This gives my enterprise lab a realistic identity driven security structure because the firewall can now enforce access, monitor activity, and log sessions using authenticated domain identities.

## Implementing Fortinet FSSO for Identity Based Firewall Policies

In this part of my homelab project, I deployed FortiGate Single Sign On to connect my firewall with my Windows Server Active Directory. 
My goal was to let the firewall identify users automatically based on their Windows logins so that I could apply security policies according to usernames and groups instead of relying only on IP addresses. 
This approach reflects how enterprises enforce identity based access control.
<img width="1557" height="958" alt="FFSO components " src="https://github.com/user-attachments/assets/b7d6c272-792c-48fd-b926-f3e2df236628" />

A-Installing the FSSO Components on Windows Server

I began on my domain controller, which hosts the dervis.lab Active Directory domain. 
The FSSO system requires two components, and I installed both of them on the same server because this keeps the setup simple in a homelab environment.

What I installed

-DC Agent
The DC Agent monitors the Windows Security log and detects domain logon events. It captures information such as usernames, the IP addresses of devices, and login timestamps.
This allows the FortiGate to know which user is active on each workstation.

<img width="1560" height="957" alt="dc agent installation" src="https://github.com/user-attachments/assets/e237bc79-553b-4e86-b685-f12e6aadb514" />


-FSSO Collector Agent
The Collector Agent receives logon information from the DC Agent and forwards the user to IP mappings to the FortiGate. 
It also sends group membership information so that the firewall can apply identity based policies.
This component is essential because it acts as the link between the domain controller and the FortiGate.

<img width="1560" height="957" alt="dc agent installation" src="https://github.com/user-attachments/assets/7862dcbe-0c4e-447e-b632-3e66ff285c14" />
<img width="1551" height="954" alt="FSSO setup installation" src="https://github.com/user-attachments/assets/b61e11e1-da68-4162-87aa-377baf56d59a" />
<img width="1555" height="953" alt="fsso SETUP" src="https://github.com/user-attachments/assets/25f1578a-7755-44dc-9eac-ec9be0c1c096" />


B-Configuring the FSSO Collector Agent

After installing the agents, I opened the Collector Agent configuration. I added my domain controller to the monitored list and confirmed that the agent was reading Windows Security logs correctly.
I configured a password for the FortiGate connection and verified that the service was running.

Because I am using the polling method in this lab, the Collector Agent pulls logon information directly from the Windows Server event logs. 
As soon as a domain user logs in, the agent detects the authentication event and records the username and IP address.
<img width="1547" height="952" alt="FSSO setup part2" src="https://github.com/user-attachments/assets/66ecf22e-515d-44fe-bd92-48e3e662fc00" />

To make sure the communication worked, I created a firewall rule on my Windows Server to allow traffic on TCP port 8000. 
This is the port used by the Collector Agent, and opening it ensured that the FortiGate could reach the service without any issues.
<img width="1554" height="958" alt="I created a polciy to allow traffic from tcp 8000 on windows server" src="https://github.com/user-attachments/assets/2698e5d6-17ac-41f7-bae6-cb7592be6e80" />

C-Integrating Active Directory with FortiGate

On the FortiGate, I added a new FSSO server entry under the User and Authentication menu. 
I entered the IP address of my Windows Server, applied the same password I set earlier, and tested the connection.
The firewall immediately connected to the Collector Agent, which confirmed that the setup was working.

After the connection was established, FortiGate pulled my Active Directory structure automatically. I created a user group named Remote Users and added my domain accounts to it. 
Because FSSO provides group membership details directly from Active Directory, FortiGate was able to identify each domain user by name whenever they logged in to a Windows machine.

This integration now allows my firewall to build policies based on real user identities. The system can apply rules according to the person who is logged in rather than relying only on IP addresses or network segments.
This mirrors how modern enterprise networks enforce access control.

<img width="1915" height="658" alt="FFSO is deployed properly" src="https://github.com/user-attachments/assets/d7ac862d-3e86-4e7d-b8b2-49fa2c1e7b13" />
<img width="1915" height="658" alt="FFSO is deployed properly" src="https://github.com/user-attachments/assets/65165fd2-412b-4d8f-9616-f0e9df3cadcc" />

E-Summary

I successfully deployed Fortinet FSSO in my homelab by installing both the DC Agent and the Collector Agent on my Windows Server domain controller. 
I configured the Collector Agent to monitor login events and allowed FortiGate to communicate with it by opening TCP port 8000 on the server firewall.
After linking FortiGate to the Collector Agent, the firewall immediately detected my Active Directory users and groups. 
This setup now allows me to apply identity based firewall rules and monitor user activity in real time, which accurately reflects how enterprises control access and enforce security policies.


## 8-Deploying  High Availability Cluster (Active Passive)

In this part of my homelab build, I deployed a secondary FortiGate virtual appliance and configured a full high availability (HA) Active Passive cluster.
My goal was to simulate a real enterprise firewall environment where redundancy, failover, heartbeat links, and monitored interfaces are essential for maintaining uptime.
I configured VMware networking, prepared the management and heartbeat ports, verified communication, and then synchronized both units into a stable HA pair.

A-Deploying the Secondary FortiGate and Preparing VMware Networking

I began by deploying the second FortiGate VM in VMware Workstation. I assigned its hardware resources and then configured its network adapters to match the primary unit.

-Management Interface (Port 10)

I set port10 to Bridged mode. This allowed me to reach the secondary FortiGate from my laptop using its assigned management IP address. 
Once the system booted, I configured port10 to allow http, https, ping, and ssh, which made remote access easier.

-Heartbeat Interfaces (Port 7 and Port 8)

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


## Deploying Ubuntu Server for GLPI, Zabbix and Wazuh

In this stage of my homelab, I deployed an Ubuntu Server virtual machine and transformed it into a central platform for three major enterprise tools that support IT operations, monitoring, and security.
My goal was to recreate what real companies use for asset management, helpdesk services, network monitoring, and security visibility. I installed GLPI, Zabbix, and Wazuh on the same server, 
and I followed the same structured installation approach for each tool.

1. Deploying the Ubuntu Server

I began by installing Ubuntu Server and checking its network configuration using the ip a command. 
The machine received the address 192.168.72.54, which allowed me to access it through SSH from my workstation.

To work more comfortably, I connected to the server through SecureCRT. 
This gave me a stable terminal where I could edit configuration files, follow installation guides, and manage packages with ease.

<img width="1480" height="836" alt="I deploy my Ubuntu server ( Zabbix and GLPI)" src="https://github.com/user-attachments/assets/40ae7bbd-595a-435c-8f66-195d613feb23" />
<img width="1152" height="1015" alt="I use SecureCRT to ssh my ubuntu server  I am installed GLPI" src="https://github.com/user-attachments/assets/80c5f570-ec30-46f0-afc7-5ca1d8734038" />

2. Installing GLPI

What GLPI is and why it matters

GLPI is an IT asset management and helpdesk system. It helps organizations track their devices, software, users, and infrastructure.
At the same time, it provides a full ticketing platform that allows support teams to manage incidents and service requests.
It is an important tool because it centralizes both inventory and helpdesk operations in one place.

How I installed GLPI ?

I prepared the server by configuring MariaDB, creating the glpidb database, and adding a dedicated user with the correct privileges.
I downloaded the GLPI package from GitHub and extracted it into the Apache web directory, then created the necessary Apache configuration file so the service would load correctly.

After restarting Apache, I accessed the GLPI installer through my browser at http://192.168.72.54/glpi
The installation page opened without issues. After completing the setup, I logged into the GLPI dashboard and confirmed that everything was working properly.

<img width="1919" height="1032" alt="I access GLPI DASHBOARD" src="https://github.com/user-attachments/assets/e9017ee9-8ed7-4dc9-a9e6-19cf01ca393f" />
<img width="1917" height="925" alt="GLPI dashboard" src="https://github.com/user-attachments/assets/8f9b8686-d7ce-43c8-9359-3d775394e572" />

3. Installing Zabbix

What Zabbix is and why it matters

Zabbix is an open source monitoring system used to observe servers, network devices, applications, and services in real time.
It helps detect problems early, prevents downtime, and improves visibility across an environment. 
It is a core tool in both SOC and NOC operations because it provides live monitoring, alerts, and performance data.

How I installed Zabbix ?

I installed the Zabbix server, the frontend, and the agent packages. I created a dedicated zabbix database in MariaDB, granted the correct permissions, and imported the initial schema.
After editing the Zabbix configuration file with the right database credentials, I enabled and started all the services.

Once everything was ready, I opened http://192.168.72.54/zabbix
 in my browser and logged into the dashboard. The interface showed that the Zabbix server was running and ready for monitoring.
 
 <img width="1918" height="1030" alt="I am installing Zabbix " src="https://github.com/user-attachments/assets/0e2fdc77-901b-46e1-b095-224860e1c3c2" />
 <img width="1919" height="1034" alt="Accessing Zabbix" src="https://github.com/user-attachments/assets/284af41e-79ac-4380-b901-67e2640ba126" />
 <img width="1914" height="924" alt="Zabbix dashboard" src="https://github.com/user-attachments/assets/4d365e89-5b18-4e3b-8de2-d9ef4aefc7c3" />

 4. Installing Wazuh

I installed Wazuh on the same server using the same SecureCRT workflow. Wazuh is an open source security platform that focuses on detection, monitoring, and response. 
It includes intrusion detection, log analysis, file integrity monitoring, vulnerability detection, and compliance checks.
It is an essential tool in modern SOC environments because it gives deep visibility into security events and endpoint activity.
The installation script handled most of the configuration. When it finished, I accessed the Wazuh dashboard through the web interface and verified that the service was running correctly.

<img width="960" height="1032" alt="Wazuh is installed" src="https://github.com/user-attachments/assets/51c07a3a-dfbf-4ee9-a8a9-c08854688d38" />
<img width="958" height="920" alt="access Wazuh dashboard" src="https://github.com/user-attachments/assets/1696190c-8266-425b-9de8-622f9d5d644a" />
<img width="1919" height="921" alt="Wazuh Dashboard" src="https://github.com/user-attachments/assets/2887351b-928b-4cb3-902d-c60d79080584" />

5. Summary 

I deployed an Ubuntu Server and installed three major enterprise level tools: GLPI for asset management and helpdesk operations, Zabbix for real time monitoring, 
and Wazuh for security visibility and threat detection. I used SecureCRT throughout the process to manage the server through SSH, which made the installation smooth and efficient.

Each tool installed successfully, and I confirmed this by accessing the GLPI dashboard, the Zabbix dashboard, and the Wazuh dashboard.
Together, these systems now form a strong IT and security operations environment inside my homelab.
They replicate the same tools used in real organizations and allow me to practice managing, monitoring, and securing a complete enterprise style infrastructure.
















































