# home-soc-lab (pfSense + VLAN Segmentation + Wazuh SIEM + Red/Blue Simulation)

## Overview

This project documents the design, implementation, and operation of a home-based Security Operations Center (SOC) lab. The environment is built to simulate enterprise network segmentation, security monitoring, and adversarial activity in a controlled setting.

The lab integrates firewalling, VLAN segmentation, wireless isolation, log collection, and security monitoring to replicate real-world security operations workflows.

---

## Objectives

The primary goals of this environment are:

- Design and implement segmented network architecture using VLANs
- Configure and manage firewall policies using pfSense
- Deploy and operate a centralized logging and detection platform (Wazuh SIEM)
- Simulate adversary techniques in a controlled lab environment
- Develop detection and response workflows for security events
- Improve practical understanding of defensive and offensive security concepts

---

## Architecture Summary

The environment is composed of the following core components:

- Edge Firewall: pfSense (Protectli V1410 hardware)
- Switching Infrastructure: Netgate-managed switch
- Wireless Infrastructure: TP-Link Omada Access Points
- Security Monitoring: Wazuh SIEM
- Network Segmentation: VLAN-based isolation model

---

## Network Segmentation Model

The network is divided into multiple security zones:

- VLAN 10: Trusted internal network (user devices and management systems)
- VLAN 20: Guest network with internet-only access
- VLAN 30: Security testing and attack simulation environment
- VLAN 40: Security monitoring and logging infrastructure (Wazuh)
- VLAN 99: Network management and administrative access

Each VLAN is isolated using firewall policies defined in pfSense.

---

## Security Controls Implemented

The following security controls are implemented within the environment:

- Stateful firewall rules for inter-VLAN traffic control
- Network segmentation based on trust boundaries
- Wireless network isolation for guest access
- Centralized log collection and analysis using Wazuh
- Detection rules for simulated attack patterns
- Traffic monitoring and alert correlation

---

## Red Team Simulation Scope

The red team component is limited to controlled lab activity and includes:

- Network reconnaissance and enumeration
- Port scanning and service discovery
- Simulated lateral movement techniques
- Basic credential-based attack simulation

All activities are restricted to the lab environment.

---

## Blue Team Operations

The blue team component focuses on detection and response:

- Log ingestion from network and endpoint sources
- Alert monitoring and tuning within Wazuh
- Analysis of security events and anomalies
- Incident response documentation and workflows
- Firewall log correlation and traffic analysis

---

## Tools and Technologies

- pfSense firewall
- Netgate switching infrastructure
- TP-Link Omada wireless system
- Wazuh SIEM platform
- Kali Linux (attack simulation)
- Windows and Linux endpoints

---

## Repository Structure

The repository is organized as follows:

- architecture/              Network diagrams and design documentation
- pfsense/                   Firewall configuration and policy documentation
- switches/                  VLAN and switching configuration
- wireless/                  Access point and SSID configuration
- detection/                 SIEM configuration and alert rules
- attack-simulations/       Documented adversary techniques
- red-team/                 Offensive security notes and procedures
- blue-team/                Defensive security workflows and playbooks
- logs-samples/            Sample logs and alert outputs

---

## Security Considerations

This environment is strictly isolated and used for educational and research purposes only. It does not interact with production systems or external networks beyond standard internet access through controlled firewall rules.

Sensitive configuration data, credentials, and real-world identifiers are excluded from this repository.

---

## Future Improvements

Planned enhancements include:

- Deployment of intrusion detection/prevention systems (IDS/IPS)
- Integration of threat intelligence feeds
- Advanced alert correlation and rule tuning in Wazuh
- Expanded attack simulation scenarios
- Automated incident response scripting

---

## Purpose

This repository serves as a technical record of a security-focused lab environment used to develop practical skills in network security, threat detection, and incident response.
