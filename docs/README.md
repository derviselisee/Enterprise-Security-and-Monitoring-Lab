# ENTERPRISE SECURITY AND MONITORING LAB

Enterprise Security and Monitoring Lab with **Active Directory, LDAP, FortiGate, Wazuh, Zabbix, GLPI, and Kali Linux**

This project recreates a realistic enterprise infrastructure where identity services, firewall security, monitoring platforms, and threat detection systems operate together in a SOC style environment.

---

# MODULES

| No | Name |
|----|------|
| Module 1 | [Lab Architecture and Infrastructure](#module-1-lab-architecture-and-infrastructure) |
| Module 2 | [FortiGate Network Deployment](#module-2-fortigate-network-deployment) |
| Module 3 | [SD WAN Configuration](#module-3-sd-wan-configuration) |
| Module 4 | [Firewall Policy Configuration](#module-4-firewall-policy-configuration) |
| Module 5 | [Network Connectivity Validation](#module-5-network-connectivity-validation) |
| Module 6 | [Active Directory Deployment](#module-6-active-directory-deployment) |
| Module 7 | [Domain Client Integration](#module-7-domain-client-integration) |
| Module 8 | [LDAP Authentication Integration](#module-8-ldap-authentication-integration) |
| Module 9 | [Fortinet FSSO Deployment](#module-9-fortinet-fsso-deployment) |
| Module 10 | [FortiGate High Availability Cluster](#module-10-fortigate-high-availability-cluster) |
| Module 11 | [Monitoring Platform Deployment](#module-11-monitoring-platform-deployment) |
| Module 12 | [Threat Simulation and Detection](#module-12-threat-simulation-and-detection) |
| Module 13 | [Hybrid Cloud Expansion](#module-13-hybrid-cloud-expansion) |


### Lab Overview

This environment mirrors how enterprises design secure infrastructures by integrating identity services, monitoring tools, and firewall security into a structured network.

### Infrastructure Components

**Windows Server 2022**

Domain controller responsible for:

- Active Directory  
- DNS  
- User authentication  
- LDAP integration  

**Windows 10**

Represents a standard employee workstation used for:

- Domain authentication  
- Endpoint monitoring  
- User activity simulation  

**Windows 7**

Legacy vulnerable system used for security testing.

**Ubuntu Server**

Hosts enterprise monitoring platforms:

- GLPI
- Zabbix
- Wazuh

**Ubuntu Desktop**

Linux client used for monitoring and authentication testing.

**Kali Linux**

Attacker machine used to simulate security threats.


[Back to Top](#top)
