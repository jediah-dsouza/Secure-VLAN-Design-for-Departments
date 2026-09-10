# 🔐 Secure VLAN Design for Departments

> A Cisco Packet Tracer-based enterprise network design demonstrating departmental VLAN segmentation, Layer 3 Inter-VLAN Routing, VLSM addressing, and Extended ACLs for role-based communication control.

---

## 📌 Overview

**Secure VLAN Design for Departments** is a networking project developed in **Cisco Packet Tracer** to model a secure, segmented organizational network.

The organization is divided into six departments:

- Computer Science (CS)
- Artificial Intelligence (AI)
- Software Engineering (SE)
- Cyber Security
- Administration
- Examination

Each department is placed in a separate VLAN and IP subnet. A central Layer 3 switch performs inter-VLAN routing and enforces communication policies using Extended ACLs.

The core security requirement is:

> **Staff devices should communicate only within their own department, while Heads of Department (HODs) are allowed to communicate across departments for coordination.**

This project demonstrates how VLANs, trunking, Layer 3 switching, VLSM, and ACLs can be combined to create a structured and secure network.

---

## 🎯 Objectives

The project was designed to achieve the following objectives:

- Segment six departments using dedicated VLANs.
- Provide each department with a dedicated IP subnet.
- Connect departmental devices through dedicated access switches.
- Use 802.1Q trunk links between access switches and the Layer 3 core.
- Implement Inter-VLAN Routing on the core switch.
- Provide a Layer 3 default gateway for each VLAN using SVIs.
- Apply Extended ACLs to enforce role-based communication.
- Allow HOD-to-HOD communication across departments.
- Prevent unauthorized staff-to-staff communication between departments.
- Verify the design using IOS show commands, ping, and traceroute.

---

# 🏗️ Network Topology

The project uses a centralized core-and-access architecture.

![Network Design Topology](<Screenshot 2026-09-11 022408.png>)

### Device Count

| Device | Quantity | Role |
|---|---:|---|
| Layer 3 Switch | 1 | Core routing, SVIs and ACLs |
| Access Switches | 6 | Department connectivity |
| PCs | 30 | End-user devices |
| **Total** | **37** | |

Each department contains:

```text
1 × HOD PC
4 × Staff PCs
```

---

# 🏢 Department & VLAN Plan

| VLAN | Department | Planned Users | Network | Subnet Mask | Default Gateway |
|---:|---|---:|---|---|---|
| 10 | Computer Science | 70 | `192.168.10.0/25` | `255.255.255.128` | `192.168.10.26` |
| 20 | Artificial Intelligence | 60 | `192.168.10.128/26` | `255.255.255.192` | `192.168.10.130` |
| 30 | Software Engineering | 50 | `192.168.10.192/26` | `255.255.255.192` | `192.168.10.200` |
| 40 | Cyber Security | 30 | `192.168.11.0/27` | `255.255.255.224` | `192.168.11.30` |
| 50 | Administration | 20 | `192.168.11.32/27` | `255.255.255.224` | `192.168.11.35` |
| 60 | Examination | 20 | `192.168.11.64/27` | `255.255.255.224` | `192.168.11.65` |

> **Note:** The addressing plan uses the departmental subnets defined for the project. The original academic report labels the overall network as `192.168.10.0/24`, while VLANs 40–60 use `192.168.11.x`; therefore, the implementation treats the combined addressing space as spanning the required `192.168.10.x` and `192.168.11.x` ranges.

---

# 👥 End-Device Addressing

## VLAN 10 — Computer Science

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| CS-HOD | `192.168.10.1` | `/25` | `192.168.10.26` |
| CS-PC1 | `192.168.10.2` | `/25` | `192.168.10.26` |
| CS-PC2 | `192.168.10.3` | `/25` | `192.168.10.26` |
| CS-PC3 | `192.168.10.4` | `/25` | `192.168.10.26` |
| CS-PC4 | `192.168.10.5` | `/25` | `192.168.10.26` |

## VLAN 20 — Artificial Intelligence

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| AI-HOD | `192.168.10.131` | `/26` | `192.168.10.130` |
| AI-PC1 | `192.168.10.132` | `/26` | `192.168.10.130` |
| AI-PC2 | `192.168.10.133` | `/26` | `192.168.10.130` |
| AI-PC3 | `192.168.10.134` | `/26` | `192.168.10.130` |
| AI-PC4 | `192.168.10.135` | `/26` | `192.168.10.130` |

## VLAN 30 — Software Engineering

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| SE-HOD | `192.168.10.201` | `/26` | `192.168.10.200` |
| SE-PC1 | `192.168.10.202` | `/26` | `192.168.10.200` |
| SE-PC2 | `192.168.10.203` | `/26` | `192.168.10.200` |
| SE-PC3 | `192.168.10.204` | `/26` | `192.168.10.200` |
| SE-PC4 | `192.168.10.205` | `/26` | `192.168.10.200` |

## VLAN 40 — Cyber Security

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| CYBER-HOD | `192.168.11.1` | `/27` | `192.168.11.30` |
| CYBER-PC1 | `192.168.11.2` | `/27` | `192.168.11.30` |
| CYBER-PC2 | `192.168.11.3` | `/27` | `192.168.11.30` |
| CYBER-PC3 | `192.168.11.4` | `/27` | `192.168.11.30` |
| CYBER-PC4 | `192.168.11.5` | `/27` | `192.168.11.30` |

## VLAN 50 — Administration

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| ADMIN-HOD | `192.168.11.36` | `/27` | `192.168.11.35` |
| ADMIN-PC1 | `192.168.11.37` | `/27` | `192.168.11.35` |
| ADMIN-PC2 | `192.168.11.38` | `/27` | `192.168.11.35` |
| ADMIN-PC3 | `192.168.11.39` | `/27` | `192.168.11.35` |
| ADMIN-PC4 | `192.168.11.40` | `/27` | `192.168.11.35` |

## VLAN 60 — Examination

| Device | IP Address | Mask | Gateway |
|---|---|---|---|
| EXAM-HOD | `192.168.11.66` | `/27` | `192.168.11.65` |
| EXAM-PC1 | `192.168.11.67` | `/27` | `192.168.11.65` |
| EXAM-PC2 | `192.168.11.68` | `/27` | `192.168.11.65` |
| EXAM-PC3 | `192.168.11.69` | `/27` | `192.168.11.65` |
| EXAM-PC4 | `192.168.11.70` | `/27` | `192.168.11.65` |

---

# 🔀 Switching Design

Each department has a dedicated access switch:

```text
SW-CS      → VLAN 10
SW-AI      → VLAN 20
SW-SE      → VLAN 30
SW-CYBER   → VLAN 40
SW-ADMIN   → VLAN 50
SW-EXAM    → VLAN 60
```

End devices are connected through access ports.

The uplinks from access switches to the core are configured as 802.1Q trunks.

Example access-port configuration:

```cisco
interface range fa0/1-5
switchport mode access
switchport access vlan 10
spanning-tree portfast
```

Example trunk configuration:

```cisco
interface gi0/1
switchport mode trunk
```

Depending on the Packet Tracer switch model, 802.1Q encapsulation may need to be explicitly selected with:

```cisco
switchport trunk encapsulation dot1q
```

---

# 🌐 Inter-VLAN Routing

The central Layer 3 switch performs routing between VLANs using **Switch Virtual Interfaces (SVIs)**.

Example:

```cisco
interface vlan 10
ip address 192.168.10.26 255.255.255.128
no shutdown
```

Routing is enabled with:

```cisco
ip routing
```

SVI gateways used in the project:

```text
VLAN 10 → 192.168.10.26
VLAN 20 → 192.168.10.130
VLAN 30 → 192.168.10.200
VLAN 40 → 192.168.11.30
VLAN 50 → 192.168.11.35
VLAN 60 → 192.168.11.65
```

---

# 🔐 Security Architecture

## Communication Policy

The ACL design implements a role-based communication model.

### HODs

HOD devices are permitted to communicate across departments:

```text
HOD → HOD = ✅ ALLOWED
```

Examples:

```text
CS-HOD     → AI-HOD       ✅
CS-HOD     → SE-HOD       ✅
AI-HOD     → CYBER-HOD    ✅
ADMIN-HOD  → EXAM-HOD     ✅
```

### Staff

Staff devices remain restricted to their own department:

```text
Staff → Same VLAN       = ✅ ALLOWED
Staff → Other VLAN      = ❌ DENIED
```

Examples:

```text
CS-PC1 → CS-PC2         ✅
CS-PC1 → AI-PC1         ❌
CS-PC1 → SE-PC1         ❌
ADMIN-PC1 → EXAM-PC1    ❌
```

---

# 🛡️ Extended ACL Implementation

Extended ACLs are applied to the VLAN SVIs on the Layer 3 switch.

Example for CS staff:

```cisco
ip access-list extended CS-STAFF-FILTER
deny ip 192.168.10.2 0.0.0.3 192.168.10.128 0.0.0.63
deny ip 192.168.10.2 0.0.0.3 192.168.10.192 0.0.0.63
deny ip 192.168.10.2 0.0.0.3 192.168.11.0 0.0.0.31
deny ip 192.168.10.2 0.0.0.3 192.168.11.32 0.0.0.31
deny ip 192.168.10.2 0.0.0.3 192.168.11.64 0.0.0.31
permit ip any any
```

Applied inbound:

```cisco
interface vlan 10
ip access-group CS-STAFF-FILTER in
```

Equivalent policies are implemented for the remaining departmental VLANs.

---

# 🧪 Verification & Testing

The following IOS commands are useful for validating the implementation.

### VLAN Verification

```cisco
show vlan brief
```

### Trunk Verification

```cisco
show interfaces trunk
```

### SVI Status

```cisco
show ip interface brief
```

### Routing Table

```cisco
show ip route
```

### ACL Counters

```cisco
show access-lists
```

### Full Configuration

```cisco
show running-config
```

---

# 📡 Connectivity Test Matrix

| Test | Expected |
|---|---|
| CS-PC1 → CS-PC2 | ✅ Success |
| CS-PC1 → AI-PC1 | ❌ Blocked |
| CS-PC1 → SE-PC1 | ❌ Blocked |
| CS-HOD → AI-HOD | ✅ Success |
| CS-HOD → SE-HOD | ✅ Success |
| AI-HOD → CYBER-HOD | ✅ Success |
| ADMIN-HOD → EXAM-HOD | ✅ Success |
| ADMIN-PC1 → EXAM-PC1 | ❌ Blocked |

These tests verify both normal connectivity and the intended security restrictions.

---

# 🧠 Concepts Demonstrated

This project provides practical experience with:

- VLAN configuration
- VLAN-based network segmentation
- Access ports
- 802.1Q trunking
- VLSM subnetting
- IPv4 addressing
- Layer 3 switching
- Switch Virtual Interfaces (SVIs)
- Inter-VLAN Routing
- Extended Access Control Lists
- Role-based network access
- Network troubleshooting
- Ping and traceroute testing
- Cisco IOS verification commands


# 🛠️ Tools & Technologies

| Technology | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation |
| Cisco IOS CLI | Device configuration |
| VLAN | Departmental segmentation |
| 802.1Q | VLAN trunking |
| VLSM | Efficient IP addressing |
| Layer 3 Switching | Routing between VLANs |
| SVI | VLAN default gateways |
| Extended ACL | Traffic filtering |
| ICMP / Ping | Connectivity testing |
| Traceroute | Path verification |


# ✅ Final Outcome

The completed topology provides:

- ✅ Six separate departmental VLANs
- ✅ Thirty end-user PCs
- ✅ Six departmental access switches
- ✅ One central Layer 3 core switch
- ✅ VLSM-based IP addressing
- ✅ 802.1Q trunking
- ✅ Inter-VLAN routing
- ✅ Dedicated VLAN gateways
- ✅ HOD-to-HOD communication
- ✅ Staff isolation between departments
- ✅ Extended ACL-based traffic control
- ✅ Verified connectivity and security behavior

The result is a scalable academic model of a secure organizational network where segmentation and access control are enforced at the network layer.

# 🎓 Academic Context

**Project:** Complex Computing Problem (CCP)  
**Course:** Routing & Switching  
**Project Title:** Secure VLAN Design for Departments  
**Simulation Platform:** Cisco Packet Tracer


# 📜 License

This project was developed for academic and educational purposes.

The topology and configurations may be used as a learning reference and extended for experimentation with Cisco networking concepts.

---

## ⭐ Project Status

**Completed and tested in Cisco Packet Tracer.**
