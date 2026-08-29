# Project-13-PNETLab-Static-Routing
A PNETLab networking project demonstrating IP address configuration and static routing between two routers using R1 and R2.

# Project 13: Configure IP Addresses and Static Routes Using PNETLab

## 📌 Project Overview

This project is a networking lab implemented using **PNETLab**. The project focuses on configuring IPv4 addresses on router interfaces and implementing **static routing** between two routers.

The lab consists of two routers, **R1 and R2**. R1 is configured with multiple loopback interfaces representing different networks, while R1 and R2 are connected through the `192.168.12.0/24` network.

Static routes are configured on R2 to provide a path towards selected remote networks available through R1. The configuration is then verified using routing and connectivity testing commands.

---

## 🎯 Objectives

The main objectives of this project are:

- To understand basic IPv4 addressing and subnetting.
- To configure IP addresses on router interfaces.
- To configure and understand loopback interfaces.
- To create and configure a network topology in PNETLab.
- To establish connectivity between two routers.
- To understand directly connected and remote networks.
- To configure static routes on a router.
- To understand the role of a next-hop address.
- To verify routing information using the routing table.
- To test network connectivity using `ping`.
- To gain practical experience with router CLI configuration.

---

## 🛠️ Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| PNETLab | Network lab and topology environment |
| Router CLI | Router configuration and verification |
| IPv4 | Network addressing |
| Static Routing | Communication with remote networks |
| Ping | Connectivity testing |

---

## 🌐 Network Topology

The project uses two routers, **R1 and R2**, connected through the `192.168.12.0/24` network.

```text
                    R1
              ┌────────────┐
              │            │
              └──────┬─────┘
                     │
              192.168.12.0/24
                     │
              ┌──────┴─────┐
              │     R2     │
              └────────────┘


R1 Loopback Networks

R1 is configured with multiple loopback interfaces:

Loopback1 → 10.1.1.1/24
Loopback2 → 10.2.2.2/24
Loopback3 → 10.3.3.3/24
Loopback4 → 10.4.4.4/24
📋 IP Addressing Table
R1
Interface	IP Address	Subnet Mask
e0/0	192.168.12.1	255.255.255.0
Loopback1	10.1.1.1	255.255.255.0
Loopback2	10.2.2.2	255.255.255.0
Loopback3	10.3.3.3	255.255.255.0
Loopback4	10.4.4.4	255.255.255.0
R2
Interface	IP Address	Subnet Mask
e0/0	192.168.12.2	255.255.255.0
🧭 Static Routing

R2 is directly connected to the 192.168.12.0/24 network but the loopback networks are available through R1.

Therefore, static routes are configured on R2.

Static Routes
ip route 10.1.1.0 255.255.255.0 192.168.12.1

ip route 10.3.3.0 255.255.255.0 192.168.12.1

Here:

10.1.1.0/24 is the destination network.
10.3.3.0/24 is the destination network.
192.168.12.1 is the next-hop address of R1.
R2 forwards traffic for these remote networks towards R1.
⚙️ Project Workflow

The project is carried out in the following sequence:

Create PNETLab Project
        ↓
Add Router Nodes
        ↓
Connect R1 and R2
        ↓
Configure IP Addresses
        ↓
Configure R1 Loopback Interfaces
        ↓
Verify Interface Status
        ↓
Configure Static Routes on R2
        ↓
Verify Routing Table
        ↓
Test Connectivity
        ↓
Analyze Results
🔧 Configuration
R1 Configuration

The R1 router is configured with an IP address on its e0/0 interface and four loopback interfaces.

The main configuration includes:

interface e0/0
ip address 192.168.12.1 255.255.255.0
no shutdown

Loopback interfaces are configured using their respective IP addresses.

R2 Configuration

R2 is configured with:

interface e0/0
ip address 192.168.12.2 255.255.255.0
no shutdown
🧭 Static Route Configuration on R2

The required remote networks are added to R2's routing table using static routes:

ip route 10.1.1.0 255.255.255.0 192.168.12.1
ip route 10.3.3.0 255.255.255.0 192.168.12.1

This tells R2 to forward traffic for these networks to R1.

🔍 Verification

After completing the configuration, the setup is verified using the following commands.

Check Interface Status
show ip interface brief

This command displays the IP addresses and operational status of the router interfaces.

Check Routing Table
show ip route

This command is used to verify the routes known by the router, including the configured static routes.

Test Connectivity
ping 10.1.1.1

The ping command is used to check connectivity with the destination.

📦 Packet Flow

When R2 needs to communicate with a remote network such as 10.1.1.0/24, it checks its routing table.

The static route points R2 towards R1:

R2
 ↓
192.168.12.1
 ↓
R1
 ↓
10.1.1.0/24

This demonstrates how a static route provides a specific path towards a remote network.

🧪 Testing and Results

The configuration is tested after completing the router setup.

The following points are verified:

R1 and R2 interfaces are configured correctly.
The R1-R2 connection is operational.
R1 loopback interfaces are configured.
Static routes are present in the R2 routing table.
Required remote networks are reachable.
Connectivity is tested using ping.
🔧 Troubleshooting

If connectivity is not established, the following points can be checked:

Verify the IP address configured on each interface.
Check whether the interfaces are enabled using no shutdown.
Verify the connection between R1 and R2.
Check the routing table using show ip route.
Verify that the static routes have been entered correctly.
Test connectivity using ping.

Useful commands:

show ip interface brief
show ip route
ping <destination-ip>
