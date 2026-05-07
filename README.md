# home-soc-lab

*(pfSense + VLAN Segmentation + Wazuh SIEM + Red/Blue Simulation)*


This repository documents the build process, architecture, troubleshooting, and ongoing evolution of my first self-hosted SOC and segmented home lab environment.

The goal of this project is not only to show *how* the environment was built, but also to explain *why* certain technologies, configurations, and security controls were implemented.

Rather than presenting a finished environment, this repository is intended to function as a living technical journal that grows alongside the lab itself.

As the environment evolves, additional documentation, detections, attack simulations, and infrastructure changes will continue to be added.

---

# Current State

## Infrastructure

* pfSense deployed as primary router/firewall
* Managed switch configured with 802.1Q VLANs
* Omada controller deployed locally
* Multi-AP wireless mesh configured and centrally managed
* Centralized wireless SSID management operational

---

## SIEM & Monitoring

* Wazuh SIEM deployed as a standalone monitoring platform
* Management laptop onboarded as monitored endpoint
* Multiple personal endpoints integrated using Wazuh agents
* Centralized endpoint telemetry and log collection operational

---

## VLANs (Current)

| VLAN    | Purpose            |
| ------- | ------------------ |
| VLAN 20 | Management Network |
| VLAN 30 | Guest Network      |

---

## Wireless

* Controller-managed SSIDs
* Multi-AP mesh deployment operational
* Guest wireless segmentation currently being tested
* VLAN-aware wireless infrastructure in progress

---

# Planned Implementations

The environment is still actively expanding. Planned additions include:

* RED / BLUE segmented lab networks
* Dedicated attack simulation environment
* pfSense log ingestion into Wazuh
* Detection engineering and custom alert creation
* Endpoint telemetry correlation
* Adversary emulation scenarios
* Threat hunting workflows
* IDS/IPS tuning and validation
* Infrastructure hardening and management isolation
* Log parsing and alert enrichment
* Network traffic analysis workflows

---

# Project Focus

This lab is being built to strengthen practical experience in:

* Network segmentation
* Security monitoring
* Threat detection
* Incident investigation
* Infrastructure troubleshooting
* SIEM operations
* Detection engineering
* Defensive security architecture
* Firewall policy design
* Wireless infrastructure management

The emphasis of this project is understanding systems at both the operational and security level — not simply deploying tools, but understanding how they communicate, fail, recover, and interact with one another under real conditions.

---

# Network Segmentation Model

## Current Segmentation

| VLAN    | Purpose                              |
| ------- | ------------------------------------ |
| VLAN 20 | Management / Infrastructure          |
| VLAN 30 | Guest Network (internet-only access) |

Current segmentation is enforced using pfSense firewall policies and VLAN-aware switching.

---

## Planned Segmentation Expansion

| Planned VLAN | Purpose                               |
| ------------ | ------------------------------------- |
| RED          | Attack simulation / offensive testing |
| BLUE         | Trusted internal systems              |
| LOGGING      | SIEM and monitoring infrastructure    |
| MGMT         | Dedicated administrative access       |

The long-term goal is to simulate a small enterprise-style segmented environment capable of supporting both defensive monitoring and controlled attack simulation.

---

# Security Controls Implemented

Current security controls include:

* Stateful inter-VLAN firewall policies
* Wireless network isolation
* Guest network internet-only restrictions
* Centralized endpoint monitoring through Wazuh
* VLAN-based network segmentation
* Controller-managed wireless infrastructure
* DHCP-based infrastructure management with reserved addressing

Additional controls and detections will continue to be implemented as the lab evolves.

---

# Red Team Simulation Scope

The red team component of this lab is intended for controlled attack simulation and adversary emulation within isolated lab segments.

Planned activities include:

* Network reconnaissance and enumeration
* Port scanning and service discovery
* Basic credential attack simulation
* Simulated lateral movement techniques
* Detection validation against known attack behavior

All testing is restricted to the isolated lab environment.

---

# Blue Team Operations

The blue team side of the environment focuses on monitoring, detection, and investigation workflows.

Current and planned blue team activities include:

* Wazuh alert monitoring and tuning
* Endpoint telemetry analysis
* Firewall log analysis
* Detection validation
* Incident documentation
* Threat hunting exercises
* Security event correlation
* Detection rule refinement

---

# Tools & Technologies

* pfSense
* Wazuh SIEM
* TP-Link Omada ecosystem
* Managed VLAN-capable switching
* Ubuntu Linux
* Kali Linux
* Windows endpoints
* UFW firewall
* MongoDB
* Wireless mesh infrastructure

---

# Repository Structure

```text
architecture/         Network diagrams and design documentation
pfsense/              Firewall policies and VLAN configuration
switches/             VLAN and switching configuration notes
wireless/             AP deployment and wireless infrastructure
detection/            SIEM rules, detections, and alert tuning
attack-simulations/   Attack simulation documentation
red-team/             Offensive testing notes
blue-team/            Defensive workflows and investigations
log-samples/          Sample logs and alert outputs
```

---

# Security Considerations

This environment is isolated and intended strictly for educational and research purposes.

The lab does not intentionally target external systems, and all offensive testing is restricted to controlled internal environments.

Sensitive configuration data, credentials, public IP addresses, and personal identifiers are excluded from this repository.

---

# Recent Progress

## Recently Completed

* Local Omada controller deployment
* Multi-AP wireless mesh setup
* VLAN-aware wireless infrastructure
* Guest network segmentation testing
* Infrastructure IP cleanup and DHCP reservation planning
* AP adoption troubleshooting and controller onboarding

---

## Current Work

* Guest VLAN validation
* RED / BLUE VLAN deployment planning
* Wazuh integration expansion
* pfSense log forwarding
* Detection simulation and validation
* Additional infrastructure hardening

---

# Philosophy

One of the goals of this repository is to document not only successful deployments, but also troubleshooting, failures, and recovery processes encountered during the build.

This repository aims to document that process honestly as the environment continues to evolve.
