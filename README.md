# Cisco-Enterprise-Homelab
My home configuration guide using Cisco enterprise devices and configurations

# Enterprise SMB Network Architecture & Monitoring Lab

## 🏢 Project Overview
This repository documents the design, configuration, and active monitoring of a multi-VLAN enterprise network modeled for a Small-to-Medium Business (SMB). Built with physical Cisco routing and switching hardware, this project demonstrates proficiency in standard network engineering practices, strict traffic segmentation, secure device management, and Linux-based Network Management System (NMS) deployment.

## 🗺️ Network Topology
> *(Note: to be done using Draw.io)*
> `![Network Topology](diagrams/network_topology.png)`renaskitamura/Cisco-Enterprise-Homelab/diagrams/renashomelab.drawio

## ⚙️ Hardware & Software Stack
* **Edge Router:** Cisco C1111 Integrated Services Router (IOS-XE)
* **Distribution/Access Switch:** Cisco Catalyst 3560CX (IOS 15.x)
* **Network Management System:** LibreNMS, MariaDB, and Redis 
* **NMS Infrastructure:** Docker Engine natively hosted on Windows Subsystem for Linux (WSL2 Ubuntu) - Will be moved later to native Linux hosting.
* **Credential Management:** KeePassXC (Offline encrypted database)

## 🔒 Architecture & Security Implementation
The network employs a strict security-first design, isolating untrusted traffic from management interfaces.

* **VLAN Segmentation:** 
  * **VLAN 20 (Management & Trusted):** Secure subnet hosting the primary admin workstation and LibreNMS container.
  * **VLAN 40 (IoT & Untrusted):** Isolated subnet for smart devices.
  * **VLAN 50 (Media/Streaming):** Dedicated subnet for high-bandwidth media devices.
* **Inter-VLAN Routing:** Configured Router-on-a-Stick (802.1Q trunking) on the C1111.
* **Device Hardening:** Legacy Telnet is globally disabled. Management access is strictly limited to SSHv2 using local databases with modern secret hashing.
* **SNMP Security:** SNMPv2c is locked down using Read-Only community strings and strict Access Control Lists (ACLs) that only permit polling from the Management VLAN.

## 📊 Network Monitoring (NMS)
To simulate a modern NOC (Network Operations Center), a LibreNMS stack was deployed using Docker Compose. The NMS actively polls the Cisco environment to provide:
* Real-time CPU, memory, and interface utilization telemetry.
* Automated network mapping via Cisco Discovery Protocol (CDP).
* Centralized syslog aggregation (Planned).

## 📂 Repository Structure
* **`/configs`**: Sanitized base configurations for all routing and switching hardware. Passwords, hashes, and public IPs have been scrubbed for security.
* **`/diagrams`**: Logical and physical network topology maps.
* **`/docs`**: IP addressing schemes and standard operating procedures (SOPs).