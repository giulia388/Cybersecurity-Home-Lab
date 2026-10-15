# Cybersecurity Home Lab

**Building, securing, monitoring, and analyzing a virtual enterprise network.**

## Overview

Cybersecurity Home Lab is an ongoing personal project focused on designing, deploying, and securing a simulated enterprise IT infrastructure using virtualization technologies.

The purpose of this project is to develop practical skills in system administration, network security, identity and access management, threat detection, and incident response.

Rather than focusing exclusively on theoretical concepts, the lab provides a controlled environment to configure enterprise services, investigate security events, experiment with defensive techniques, and understand how different security technologies interact.

All experiments are performed in an isolated, authorized testing environment.

## Project Objectives

- Design and deploy a virtual enterprise network.
- Implement centralized identity and access management using Active Directory.
- Explore Kerberos authentication and Windows security mechanisms.
- Configure DNS, Group Policy, users, groups, and access permissions.
- Collect, monitor, and analyze security events using SIEM technologies.
- Investigate Indicators of Compromise (IoCs).
- Map suspicious activities to the MITRE ATT&CK framework.
- Explore web application vulnerabilities based on the OWASP Top 10.
- Implement and evaluate defensive security controls.
- Experiment with incident detection, correlation, and automated response.

## Lab Architecture

The infrastructure is hosted on a Windows 11 computer using Oracle VirtualBox.

### Current Infrastructure

| Component | Technology | Purpose |
|---|---|---|
| Host Machine | Windows 11 | Virtualization host |
| Hypervisor | Oracle VirtualBox | Virtual machine management |
| Domain Controller | Windows Server 2025 | Active Directory infrastructure |
| Virtual Network | CYBER-LAB | Isolated communication between VMs |
| Administration | PowerShell | System configuration and management |

### Planned Infrastructure

| Component | Technology | Purpose |
|---|---|---|
| Windows Client | Windows 11 | Domain authentication and Group Policy testing |
| Security Monitoring | Wazuh | SIEM and endpoint monitoring |
| Security Testing | Kali Linux | Authorized security assessments |
| Web Security Lab | OWASP Juice Shop | Web vulnerability analysis |
| Web Application Firewall | ModSecurity / OWASP CRS | Application-layer protection |

## Active Directory Environment

The initial deployment focuses on building a centralized Windows domain infrastructure.

**Target configuration:**

| Parameter | Value |
|---|---|
| Domain | lab.test |
| NetBIOS Name | LAB |
| Domain Controller | DC01 |
| Server Operating System | Windows Server 2025 |
| Planned Server IP | 192.168.50.10 |
| Network | 192.168.50.0/24 |
| Virtual Network | CYBER-LAB |

The environment is designed to support experiments involving authentication, authorization, centralized administration, DNS service discovery, and security policy enforcement.

## Project Roadmap

### Phase 1 — Infrastructure Setup
- [x] Install and configure Oracle VirtualBox
- [x] Deploy Windows Server 2025
- [x] Configure the DC01 hostname
- [x] Set up the CYBER-LAB internal network
- [ ] Complete and verify the Active Directory deployment
- [ ] Validate DNS service discovery and domain controller health

### Phase 2 — Identity and Access Management
- [ ] Create Organizational Units (OUs)
- [ ] Configure domain users and security groups
- [ ] Deploy a Windows domain client
- [ ] Configure and test Group Policy Objects (GPOs)
- [ ] Analyze Kerberos authentication tickets
- [ ] Implement role-based access controls

### Phase 3 — Security Monitoring and Detection
- [ ] Deploy Wazuh SIEM
- [ ] Collect Windows security event logs
- [ ] Simulate suspicious authentication activity
- [ ] Investigate security alerts and IoCs
- [ ] Map detection events to MITRE ATT&CK techniques

### Phase 4 — Web and Network Security
- [ ] Deploy a vulnerable web application
- [ ] Perform controlled OWASP Top 10 exercises
- [ ] Configure web application firewall protections
- [ ] Explore Network Access Control (NAC)

### Phase 5 — Incident Response and Automation
- [ ] Investigate simulated security incidents
- [ ] Correlate endpoint, identity, and network events
- [ ] Experiment with XDR concepts
- [ ] Design and test SOAR workflows
- [ ] Document incident response procedures

## Documentation

Each laboratory is documented with:

- Technical objectives and prerequisites
- Infrastructure configuration
- Commands and implementation steps
- Screenshots and collected evidence
- Expected and observed results
- Troubleshooting procedures
- Security observations and lessons learned

Documentation is maintained using Obsidian and Markdown.

## Skills and Technologies

**Infrastructure:** Windows Server, Active Directory, DNS, VirtualBox, PowerShell

**Networking:** TCP/IP, Network Segmentation, Virtual Networking

**Security:** IAM, Kerberos, Network Security, Security Monitoring

**Planned:** Wazuh, SIEM, MITRE ATT&CK, OWASP, WAF, Incident Response, SOAR

## Project Status

**In Progress — October 2026**

The initial virtual infrastructure has been deployed. Windows Server configuration and Active Directory domain deployment are underway.

Additional security monitoring, attack simulation, and incident response capabilities will be introduced progressively.

## Disclaimer

This project is intended strictly for educational purposes and authorized security testing.

All security experiments are designed to operate within controlled lab environments. No testing of third-party infrastructure is performed without explicit authorization.
