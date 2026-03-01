# 🔥 Firewall Configuration & Network Segmentation Lab

![Security](https://img.shields.io/badge/Security-Firewall_Configuration-red?style=for-the-badge&logo=cisco&logoColor=white)
![Tools](https://img.shields.io/badge/Tools-Packet_Tracer%20|%20VirtualBox%20|%20Windows_Firewall-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Course](https://img.shields.io/badge/Course-CSAI_5000-orange?style=for-the-badge)

A hands-on firewall configuration and network segmentation lab completed as part of **CSAI 5000: Fundamentals of Cybersecurity** at Humber College. This project covers protocol-based traffic filtering, port-based access control, and VM network isolation across three environments — Cisco Packet Tracer, VirtualBox NAT networking, and Windows Firewall.

---

## 📋 Lab Objectives

- Design and verify a LAN topology with end-to-end connectivity in Cisco Packet Tracer
- Configure firewall rules to allow and deny traffic based on protocol, port, and direction
- Understand NAT networking and VM isolation in VirtualBox
- Configure Windows Firewall inbound/outbound rules between two VMs
- Validate all firewall rules through systematic before/after testing

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Cisco Packet Tracer** | Network topology design and firewall simulation |
| **VirtualBox** | VM creation and NAT network configuration |
| **Windows Firewall** | Inbound/outbound rule configuration |
| **ICMP / TCP / UDP** | Protocols used for firewall rule testing |

---

## 📁 Repository Structure

```
firewall-network-segmentation-lab/
│
├── README.md                              # This file
├── reports/
│   └── Firewall-Network-Lab-Report.docx  # Full lab report with screenshots
├── packet-tracer/
│   └── Network-Topology.pkt              # Cisco Packet Tracer topology file

---

## 🔍 Lab Summary

### Part 1 — Cisco Packet Tracer Firewall Configuration

**Network Design:**
- 1 Router, 1 Switch, 2 PCs, 1 Server — all in the same subnet (192.168.1.0/24)
- Verified end-to-end connectivity via ping before applying any firewall rules

**Firewall Rules Tested:**

| Rule | Protocol | Port | Direction | Result |
|---|---|---|---|---|
| Deny ICMP to Server | ICMP | — | Inbound | PC1 → Server ping failed ✅ |
| Allow ICMP to PC2 | ICMP | — | Inbound | PC1 → PC2 ping worked ✅ |
| Deny HTTP | TCP | 80 | Inbound | Browser access blocked ✅ |
| Deny FTP | TCP | 21 | Inbound | FTP access blocked ✅ |
| Block UDP | UDP | — | Inbound | UDP traffic dropped ✅ |

**Key Finding:** Firewall rules filter traffic based on protocol, port, and direction independently — blocking port 80 prevents web access without affecting other services.

---

### Part 2 — VirtualBox Installation & NAT Networking

- Created two Windows VMs (VM1 and VM2) in VirtualBox
- Configured VM1 network adapter to **NAT mode**
- Confirmed internet access from inside VM1 via browser

**IP Address Comparison:**

| Device | IP Address | Network |
|---|---|---|
| VM1 (NAT) | 10.0.2.15 | 10.0.2.0/24 (VirtualBox internal) |
| Host Machine | 10.0.0.124 | 10.0.0.0/24 (Physical network) |

**Why Different Networks?**
NAT mode creates a private virtual network between the host and VM. VirtualBox acts as a virtual router translating VM traffic through the host's physical connection — the VM never directly joins the physical network.

---

### Part 3 — Windows Firewall Configuration Between VMs

**VM Network:**
- VM1: 192.168.100.10
- VM2: 192.168.100.20
- Network mode: Internal Network (isolated from host and internet)

**Test Results:**

| Test | Before Rule | After Rule |
|---|---|---|
| VM1 → VM2 ping | ❌ Request timed out | ✅ Reply received |

**Rule Created:**
- Name: Group4-Project1-Rule
- Protocol: ICMPv4
- Type: Custom inbound rule
- Applies to: All network types

**Why Ping Failed Initially:**
Windows Firewall blocks ICMP Echo Requests by default. The packets were silently dropped until an explicit inbound allow rule was created for ICMPv4.

---

## 💡 Key Takeaways

1. **Firewalls operate at multiple layers** — protocol (ICMP), transport (TCP/UDP), and application (port 80/21) rules all work independently
2. **Default deny is the right posture** — Windows blocks ICMP by default, demonstrating least privilege in action
3. **NAT isolates VMs** — VMs using NAT get a private IP range separate from the physical network, providing a layer of network segmentation
4. **Before/after testing is essential** — every firewall rule must be validated by testing both the blocked and allowed traffic paths
5. **Port-based filtering** — blocking a specific port (e.g. 80) removes service access without disrupting other connectivity

---

## 🚀 How to Reproduce

### Prerequisites
- Cisco Packet Tracer installed
- VirtualBox with two Windows VMs
- Windows Firewall access on both VMs

### Part 1 — Packet Tracer
```
1. Open Network-Topology.pkt in Cisco Packet Tracer
2. Verify ping connectivity between all devices
3. Apply firewall rules on the Server host
4. Re-test ping and browser access
```

### Part 3 — Windows Firewall
```
1. Set both VMs to Internal Network mode in VirtualBox
2. Assign static IPs: VM1=192.168.100.10, VM2=192.168.100.20
3. Test ping VM1 → VM2 (should fail)
4. On VM2: Windows Defender Firewall → Inbound Rules → New Rule
5. Select Custom → ICMPv4 → All Networks → Allow
6. Re-test ping (should succeed)
```

---

## 📚 Course Information

**Course:** CSAI 5000 — Fundamentals of Cybersecurity
**Institution:** Humber College, Toronto, ON
**Program:** Postgraduate Certificate — Cybersecurity & AI
**Project:** Project 1 — Installing VirtualBox and Configuring Firewall

---

## 👤 Author

**Waqas Salman, MSc**
Postgraduate Certificate — Cybersecurity & AI | Humber College
MSc Computer Science | Middlesex University

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/waqas-salman)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/waqassalman)

---

*Completed as part of the Postgraduate Certificate in Cybersecurity & AI — Humber College, Toronto, ON.*
