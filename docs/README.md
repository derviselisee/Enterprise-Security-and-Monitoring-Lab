# ENTERPRISE SECURITY AND MONITORING LAB

Enterprise Security and Monitoring Lab with Active Directory, LDAP, FortiGate, Wazuh, Zabbix, GLPI, and Kali Linux
---
My project is designed to mirror how a real company organizes its network, security tools, and authentication systems. Each virtual machine serves a clearly defined role that allows me to practice enterprise concepts such as identity management, monitoring, threat detection, and firewall security. Because of this structured design, the environment enables me to build and validate realistic SOC and IT operational workflows within a fully controlled setting.


# MODULES

| No | Name |
|----|------|
| Module 1 | [Lab Architecture and Infrastructure](#module-1-lab-architecture-and-infrastructure) |
| Module 2 | [FortiGate Network Setup ](#module-2-fortigate-network-deployment) |
| Module 3 | [SD WAN Configuration](#module-3-sd-wan-configuration) |
| Module 4 | [Firewall Policy Configuration](#module-4-firewall-policy-configuration) |
| Module 5 | [Active Directory & Domain Controller](#module-5-network-connectivity-validation) |
| Module 6 | [LDAP Authentication & FSSO Integration](#module-6-active-directory-deployment) |
| Module 7 | [High Availability Cluster](#module-7-domain-client-integration) |
| Module 8 | [Ubuntu Server-GLPI,Zabbix & Wazuh](#module-8-ldap-authentication-integration) |
| Module 9 | [Azure Hybrid Cloud Integration (Upcoming](#module-9-fortinet-fsso-deployment) |
| Module 10 | [Threat Simulation and Detection](#module-10-fortigate-high-availability-cluster) |
| Module 11 | [Compliance Considerations](#module-11-monitoring-platform-deployment) |



### MODULE 1
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


[Back to Top](#top)
