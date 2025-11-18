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
<img width="1919" height="923" alt="WAN 2 int configs" src="https://github.com/user-attachments/assets/94cd89d4-c7bc-45dc-8ca9-f87fb7feb785" />
<img width="1912" height="921" alt="WAN 1 int config" src="https://github.com/user-attachments/assets/208327c5-c46a-42d1-b004-f728c19c5335" />

