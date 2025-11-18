# Enterprise-Security-and-Monitoring-Lab

Enterprise Security and Monitoring Lab with AD, LDAP, Wazuh, Zabbix, GLPI, and Kali Linux

Mission Context

This project recreates a full enterprise network environment that combines identity services, firewall security, SD WAN, high availability, endpoint monitoring, and threat detection. 
The goal is to design and operate a multi platform ecosystem where Windows and Linux clients authenticate through centralized identity systems, security logs are collected and analyzed,
and FortiGate firewalls protect and monitor traffic. The lab simulates how real SOC and network engineering teams work together to manage authentication, system health, m
monitoring, and incident detection across a modern enterprise network.

Implementation Summary

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

Skills Demonstrated

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

Tools and Technologies Used

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

Purpose of the Project

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









