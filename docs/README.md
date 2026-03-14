# ENTERPRISE SECURITY AND MONITORING LAB

Enterprise Security and Monitoring Lab with Active Directory, LDAP, FortiGate, Wazuh, Zabbix, GLPI, and Kali Linux
---
My project is designed to mirror how a real company organizes its network, security tools, and authentication systems. Each virtual machine serves a clearly defined role that allows me to practice enterprise concepts such as identity management, monitoring, threat detection, and firewall security. Because of this structured design, the environment enables me to build and validate realistic SOC and IT operational workflows within a fully controlled setting.

<br>

# MODULES


| No | Name |
|----|------|
| Module 1 | [Lab Overview and Architecture](#module-1-lab-overview-and-architecture) |
| Module 2 | [FortiGate Network Setup](#module-2-fortigate-network-setup) |
| Module 3 | [SD WAN Configuration](#module-3-sd-wan-configuration) |
| Module 4 | [Firewall Policy Configuration](#module-4-firewall-policy-configuration) |
| Module 5 | [Active Directory and Domain Controller](#module-5-active-directory-and-domain-controller) |
| Module 6 | [LDAP Authentication and FSSO Integration](#module-6-ldap-authentication-and-fsso-integration) |
| Module 7 | [High Availability Cluster](#module-7-high-availability-cluster) |
| Module 8 | [Ubuntu Server with GLPI, Zabbix, and Wazuh](#module-8-ubuntu-server-with-glpi-zabbix-and-wazuh) |
| Module 9 | [Azure Hybrid Cloud Integration (Upcoming)](#module-9-azure-hybrid-cloud-integration) |
| Module 10 | [Threat Simulation and Detection](#module-10-threat-simulation-and-detection) |
| Module 11 | [Compliance Considerations](#module-11-compliance-considerations) |


---

# MODULE 1 
## LAB OVERVIEW

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
This project recreates a realistic enterprise network designed to integrate identity services, firewall security, SD WAN connectivity,
high availability, endpoint monitoring, and threat detection into one unified ecosystem.

The objective is to build and operate a multi platform environment where Windows and Linux clients authenticate through a centralized identity infrastructure,
security events are collected and analyzed through a SIEM and monitoring stack, and FortiGate firewalls enforce network segmentation and protect traffic across internal and external boundaries.

This lab mirrors how modern SOC teams and network engineering teams collaborate to manage authentication controls, system performance, monitoring workflows, and incident detection across a fully functional enterprise environment.
In addition, the architecture is designed to reflect major compliance frameworks such as ISO 27001, GDPR, and SOX, by enforcing role based access control, maintaining centralized audit logging, protecting data in transit through encryption, and supporting structured incident response procedures, all of which are essential for secure and compliant enterprise operations.
This project recreates a realistic enterprise network designed to integrate identity services, firewall security, SD WAN connectivity, high availability, endpoint monitoring, and threat detection into one unified ecosystem. 


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


[Back to Top](#top)
