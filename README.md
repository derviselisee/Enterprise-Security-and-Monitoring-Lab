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
