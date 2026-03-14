# ENTERPRISE SECURITY AND MONITORING LAB

Enterprise Security and Monitoring Lab with Active Directory, LDAP, FortiGate, Wazuh, Zabbix, GLPI, and Kali Linux
---
My project is designed to mirror how a real company organizes its network, security tools, and authentication systems. Each virtual machine serves a clearly defined role that allows me to practice enterprise concepts such as identity management, monitoring, threat detection, and firewall security. Because of this structured design, the environment enables me to build and validate realistic SOC and IT operational workflows within a fully controlled setting.


# MODULES

| No | Name |
|----|------|
| Module 1 | [Lab Overview & Architecture](#module-1-lab-architecture-and-infrastructure) |
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

## Module 1 - Lab Overview & Architecture

Mission Context
This project recreates a realistic enterprise network designed to integrate identity services, firewall security, SD-WAN connectivity, high availability, endpoint monitoring, and threat detection into one unified ecosystem.
The objective is to build and operate a multi-platform environment where:

Windows and Linux clients authenticate through a centralized identity infrastructure
Security events are collected and analyzed through a SIEM and monitoring stack
FortiGate firewalls enforce network segmentation and protect traffic across internal and external boundaries

This lab mirrors how modern SOC teams and network engineering teams collaborate to manage authentication controls, system performance, monitoring workflows, and incident detection across a fully functional enterprise environment.
Virtual Machines & Roles
VMRoleWindows Server 2022Domain Controller — Active Directory, DNS, DHCP, LDAP, FSSOWindows 10Employee workstation — domain logins, Group Policy, endpoint monitoringWindows 7Legacy/vulnerable workstation — exploit simulation, SIEM testingUbuntu ServerHosts GLPI (helpdesk), Zabbix (monitoring), and Wazuh (SIEM)Ubuntu DesktopLinux client — cross-platform auth, log collection, agent deploymentKali LinuxAttacker machine — scans, brute force, exploit simulationFGT HQ (Primary FortiGate)Main firewall — routing, NAT, security profiles, identity-based policiesFGT HQ2 (Secondary FortiGate)HA pair — Active-Passive cluster, failover, config sync
Skills Demonstrated

Windows Server administration: AD design, OU structuring, DNS/DHCP, domain workstation management
FortiGate engineering: SD-WAN, HA, routing, segmentation, NAT, LDAP/FSSO identity enforcement
Linux system administration: Ubuntu Server and Desktop, SSH management, service integration
SIEM operations with Wazuh: agent deployment, log ingestion, rule-based alerting, event correlation
Performance monitoring with Zabbix: SNMP and Zabbix Agents, device and network health
IT operations with GLPI: inventory tracking, helpdesk ticketing, documentation workflows
Identity integration: LDAP + FSSO for real-time user mapping and policy enforcement
Threat simulation: Kali Linux scanning, enumeration, and intrusion attempts validated through SIEM and firewall logs
Enterprise troubleshooting: multi-layer debugging across networking, firewalls, Windows, Linux, and hybrid cloud

Tools & Technologies
Operating Systems: Windows Server 2022, Windows 10, Ubuntu Desktop, Ubuntu Server, Kali Linux
Security & Monitoring: Wazuh SIEM, Zabbix, GLPI, FortiView & Log Analysis Tools
Networking & Protocols: FortiGate Firewall (VM), LDAP, FSSO, SNMP, Syslog, OSPF, IPsec VPN
Cloud & Virtualization: Microsoft Azure, Azure Bastion, VMware Workstation
Administration: SecureCRT, SSH


[Back to Top](#top)
