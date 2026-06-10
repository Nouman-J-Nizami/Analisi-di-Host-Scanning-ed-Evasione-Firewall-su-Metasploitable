# Advanced Host Scanning and Firewall Evasion Analysis with Nmap & Wireshark

## Overview

This project documents a comprehensive network reconnaissance and packet analysis laboratory performed against a Metasploitable 2 target system using Kali Linux.

The objective was to identify exposed services, enumerate system information, analyze TCP/IP communications, and evaluate multiple firewall and IDS evasion techniques through practical experimentation and packet-level verification using Wireshark.

The assessment combines active reconnaissance, service enumeration, protocol analysis, and advanced Nmap scanning techniques within an isolated cybersecurity laboratory environment.

---

## Laboratory Environment

### Attacker

- Kali Linux
- IP: 192.168.50.100

### Target

- Metasploitable 2
- IP: 192.168.50.101

### Network

- Isolated Lab Network
- 192.168.50.0/24

### Tools

- Nmap
- Wireshark
- Kali Linux
- Metasploitable 2

---

# Phase 1 – Host Discovery

Network discovery was performed to identify active systems within the laboratory subnet.

### Command

```bash
nmap -sn 192.168.50.0/24
```

### Results

Identified active hosts:

- Kali Linux
- Metasploitable 2

---

# Phase 2 – Port Scanning

Common TCP ports were scanned to identify exposed network services.

### Objectives

- Discover open ports
- Identify attack surface
- Establish baseline visibility

### Examples of Open Services

- FTP
- SSH
- Telnet
- SMTP
- HTTP
- SMB

---

# Phase 3 – Service Version Detection

### Command

```bash
nmap -sV 192.168.50.101
```

### Identified Services

- vsFTPd 2.3.4
- ProFTPD 1.3.1
- OpenSSH 4.7p1
- Samba 3.x – 4.x
- MySQL 5.0.51a
- PostgreSQL 8.3.x
- VNC
- Apache HTTP Server

### Security Assessment

Multiple legacy and outdated services were identified, significantly increasing the attack surface and potential exposure to publicly documented vulnerabilities.

---

# Phase 4 – Full TCP Port Enumeration

### Command

```bash
nmap -p- -sV 192.168.50.101
```

### Purpose

Perform complete TCP enumeration to identify services running on non-standard ports.

### Findings

The scan revealed numerous additional services and expanded visibility of the target's exposed infrastructure.

---

# Phase 5 – Operating System Fingerprinting

### Command

```bash
nmap -O 192.168.50.101
```

### Results

Nmap identified:

- Linux Kernel 2.6.x
- Estimated versions between 2.6.9 and 2.6.33

### Importance

Operating system identification helps correlate discovered services with known vulnerabilities and exploitation paths.

---

# Phase 6 – Nmap Scripting Engine Enumeration

### Command

```bash
nmap -sC 192.168.50.101
```

### Key Findings

#### FTP

- Anonymous login enabled

#### SMB

- Guest authentication enabled
- Message signing disabled

#### SMTP

- PIPELINING
- VRFY
- ETRN
- STARTTLS

#### HTTP

- Metasploitable2 web application identified

#### Additional Services

- RPCBind
- NFS
- UnrealIRCd
- Apache Tomcat

### Security Impact

The presence of anonymous FTP access and guest SMB authentication would represent severe security risks in a production environment.

---

# Phase 7 – Aggressive Enumeration

### Command

```bash
nmap -A 192.168.50.101
```

### Components Included

- Version Detection
- OS Detection
- NSE Scripts
- Traceroute

This scan provided a consolidated overview of all reconnaissance findings.

---

# Wireshark Traffic Analysis

Throughout the project, Wireshark was used to validate and inspect packet-level communications.

### Protocol Layers Analyzed

- Ethernet II (Layer 2)
- IPv4 (Layer 3)
- TCP (Layer 4)
- FTP (Layer 7)

### Investigated Elements

- TCP Three-Way Handshake
- TCP Flags
- Sequence Numbers
- Acknowledgment Numbers
- Window Size
- FTP Banner Responses

This analysis demonstrated how reconnaissance activities translate into actual network traffic.

---

# Advanced Firewall and IDS Evasion Techniques

## TCP SYN Scan

### Command

```bash
nmap -sS 192.168.50.101
```

### Analysis

The SYN scan performs a half-open connection:

```text
SYN → SYN/ACK → RST
```

This approach identifies open ports without completing the TCP handshake.

---

## IP Fragmentation

### Command

```bash
nmap -sS -f 192.168.50.101
```

### Objective

Evaluate how fragmented IP packets appear at the network level and how fragmentation may affect packet inspection mechanisms.

### Wireshark Validation

Verified:

- Fragment Offset
- More Fragments Flag
- IPv4 Fragmentation Behavior

---

## Source Port Spoofing

### Command

```bash
nmap -sS -g 53 192.168.50.101
```

### Objective

Simulate DNS-originated traffic by using source port 53.

### Analysis

Wireshark confirmed:

- Source Port = 53
- SYN packets transmitted successfully
- Proper interaction with target services

---

## TTL Manipulation

### Command

```bash
nmap -sS --ttl 10 192.168.50.101
```

### Objective

Modify the Time To Live value to alter traffic characteristics.

### Validation

Wireshark inspection confirmed:

- Modified TTL field
- Accurate IPv4 header manipulation
- Correlation between Nmap configuration and packet structure

---

## MAC Address Spoofing

### Command

```bash
nmap -sS --spoof-mac 00:11:22:33:44:55 192.168.50.101
```

### Objective

Modify the Ethernet source address at Layer 2.

### Verification

Wireshark confirmed:

- Spoofed source MAC address
- Successful communication with the target
- Correct Layer 2 packet modification

---

# Skills Demonstrated

- Network Reconnaissance
- Information Gathering
- Host Discovery
- Port Scanning
- Service Enumeration
- OS Fingerprinting
- NSE Enumeration
- TCP/IP Analysis
- Packet Inspection
- Wireshark Analysis
- Firewall Evasion Concepts
- IDS Evasion Concepts
- IP Fragmentation Analysis
- Source Port Spoofing
- TTL Manipulation
- MAC Address Spoofing
- Layer 2 / Layer 3 / Layer 4 Protocol Analysis

---

# Key Learning Outcomes

This laboratory demonstrates how network reconnaissance techniques can be combined with packet-level analysis to understand service exposure, protocol behavior, and advanced scanning methodologies.

The project highlights the relationship between Nmap scan configurations and their direct impact on Ethernet, IPv4, and TCP packet structures, providing practical insight into reconnaissance operations, network security assessments, and firewall evasion concepts.

---

## Author

Nouman Javed Nizami

Cybersecurity Analyst | Network Security | Threat Analysis | Penetration Testing
