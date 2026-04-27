# Network Security Architecture Overview

## Overview

This document describes the logical and security architecture of a segmented network environment designed to support secure connectivity, traffic isolation, and security monitoring. The design follows a firewall-centric model with enforced segmentation between trust zones and controlled inter-zone communication.

The architecture is intended to simulate enterprise network segmentation patterns used in security operations environments, including defensive monitoring and controlled attack simulation zones.

---

## Architecture Design

The network is built around a centralized security enforcement model where all inter-network traffic is routed through a stateful firewall.

### Core Components

- **Edge Firewall (pfSense)** — Central routing and security enforcement point. Handles NAT, inter-VLAN routing, and policy enforcement. Default-deny posture between segmented networks.
- **Managed Layer 2 Switch (802.1Q VLAN capable)** — Provides VLAN segmentation and trunk distribution. Connects firewall, access points, and endpoint systems. Enforces logical separation of network segments at Layer 2.
- **Wireless Access Points** — Provide wireless connectivity mapped to VLAN-backed SSIDs. Support multi-segment wireless access (internal and guest).

---

## Network Segmentation Model

The environment is divided into logically isolated security zones:

| Zone | Purpose | Trust Level |
|------|---------|-------------|
| MGMT NET | Infrastructure administration (firewall, switch, APs) | Restricted |
| USER NET | General-purpose internal client devices | Trusted |
| GUEST NET | Internet-only access, fully isolated from internal infrastructure | Untrusted |
| BLUE NET | Defensive security monitoring, SIEM, detection engineering | Analytical |
| RED NET | Controlled offensive security testing and adversary emulation | Isolated |

---

## Traffic Flow and Security Policy Matrix

Inter-zone communication is explicitly controlled through pfSense firewall policies. All traffic between VLANs is denied by default unless explicitly permitted.

### Allowed / Denied Traffic Matrix

| Source Zone | Destination Zone | Allowed | Protocol/Port | Purpose |
|-------------|-----------------|---------|---------------|---------|
| MGMT NET | All Zones | Limited | HTTPS / SSH | Infrastructure administration |
| USER NET | Internet | Yes | HTTP/HTTPS | General user access |
| USER NET | MGMT NET | No | — | Prevent administrative access exposure |
| GUEST NET | Internet | Yes | HTTP/HTTPS | Isolated internet access only |
| GUEST NET | Any Internal Net | No | — | Prevent lateral movement |
| RED NET | USER NET | No | — | Controlled attack isolation |
| RED NET | MGMT NET | No | — | Prevent infrastructure compromise |
| BLUE NET | All Zones | Read-Only (Log Ingestion Only) | Syslog / Agent Forwarding | Security monitoring and analysis |

### Enforcement Notes

- Inter-VLAN routing is handled exclusively by pfSense
- No direct Layer 2 communication exists between VLANs
- All cross-zone communication is policy-validated at the firewall layer

### BLUE NET Enforcement Model

The BLUE NET does not initiate connections into other security zones. Instead, it operates on a **push-based telemetry model**:

- Endpoints and infrastructure components forward logs to the Wazuh SIEM via agent-based or syslog forwarding
- pfSense firewall logs are exported to the SIEM via internal logging configuration
- Switch and access point telemetry is collected via management-plane logging where supported

This ensures BLUE NET maintains analytical visibility without requiring inbound access to production or user networks. No cross-zone polling or active data collection is performed from the BLUE NET into other segments.

---

## Security Telemetry & Log Sources (Wazuh SIEM)

The detection layer is powered by centralized log aggregation into Wazuh SIEM. The following data sources feed into the monitoring pipeline:

### 1. Firewall Telemetry (pfSense)
- Firewall allow/deny logs
- NAT and port forwarding activity
- Inter-VLAN routing attempts
- Intrusion-related events (if IDS/IPS enabled)

### 2. Endpoint Telemetry (Wazuh Agents)
- Host-based authentication events
- File integrity monitoring (FIM)
- Process execution logs
- System security logs (Windows Event Logs / Linux auth logs)

### 3. Network Infrastructure Logs
- Switch port status and link changes
- VLAN assignment changes (where supported)
- Access point association and disassociation events

### 4. Authentication and Access Events
- Administrative login attempts to pfSense
- SSH / management interface access logs
- Failed authentication attempts across systems

---

## Detection Use Cases

The following use cases reflect active detection scenarios supported by the current architecture:

- **Failed authentication detection** — Alerting on repeated failed login attempts across zones, including administrative interfaces and endpoints
- **Inter-VLAN policy violations** — Detecting and alerting on traffic attempts that violate the defined segmentation policy at the firewall layer
- **File integrity alerts** — FIM-based detection on critical system files to identify unauthorized modification or tampering
- **Lateral movement indicators** — Monitoring for anomalous traffic patterns originating from or targeting the RED NET or GUEST NET segments
- **Privilege escalation signals** — Process execution and auth log correlation to surface suspicious privilege changes on monitored endpoints

---

## Design Principles

This architecture is built on the following security principles:

- Segmentation of trust zones based on operational risk
- Default-deny network posture between all zones
- Centralized enforcement of network policy via firewall
- Push-based telemetry model for passive monitoring without lateral exposure
- Separation of offensive and defensive security environments
- Centralized logging and detection for visibility and response

---

## Detection Engineering and Future Enhancements

The current environment already supports centralized log ingestion and detection via Wazuh SIEM, including rule-based alerting across firewall, endpoint, and infrastructure telemetry.

Planned enhancements focus on expanding detection depth and network visibility:

- **Suricata IDS/IPS** — Native pfSense integration for network-level intrusion detection and prevention
- **Traffic mirroring** — Packet-level inspection and analysis for deeper network visibility
- **MITRE ATT&CK mapping** — Expanded mapping of detection rules to observed and simulated adversary behaviors
- **Advanced correlation rules** — Enhanced alert tuning and multi-source event correlation within Wazuh
- **Vulnerability scanning integration** — Continuous exposure assessment across monitored segments

---

## Summary

This architecture provides a segmented and policy-driven network environment designed to support security monitoring, controlled attack simulation, and defensive analysis. The push-based telemetry model ensures analytical visibility without lateral exposure, and the detection pipeline is aligned with SOC operational workflows. It reflects common enterprise security design patterns used in modern SOC and security engineering environments.


## Running Environment

[Running Environment](/running-env)
Screenshots of pfSense firewall rules, VLAN interfaces, live dashboard, and VLAN definations are uploaded here as the env evolvers.

