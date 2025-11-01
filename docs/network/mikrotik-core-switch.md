# MikroTik Core Network Switch

## Overview

- **Purpose**: Core network infrastructure switch with VLAN segmentation
- **Role**: Layer 3 switch providing routing between VLANs and network segmentation
- **Location**: Office
- **Connection**: Connected to main network via D-Link router (192.168.0.1)
- **Function**: Network segmentation, inter-VLAN routing, firewall, DHCP, DNS, VPN

## Hardware Specifications

- **Make/Manufacturer**: MikroTik
- **Model**: CRS317-1G-16S+
- **Ports**: 16x SFP/SFP+ ports + 1x Gigabit Ethernet
- **Serial Number**: HED08K8390B
- **Firmware Version**: RouterOS 7.18
- **Software ID**: 67DD-IEY2
- **System Identity**: mikrotik
- **MAC Address**: 48:A9:8A:B6:5D:5C

## Network Interfaces

### WAN Interface (ether1)

- **IP Address**: 192.168.0.2/24
- **Network**: 192.168.0.0/24
- **Gateway**: 192.168.0.1 (D-Link DIR-X1530)
- **Purpose**: Uplink to main network
- **DHCP Client**: Disabled (static IP)
- **Connection**: To main D-Link router

### Bridge Interface (bridge0)

- **IP Address**: 192.168.1.1/24
- **Network**: 192.168.1.0/24
- **VLAN Filtering**: Enabled
- **Purpose**: Internal home network bridge
- **Admin MAC**: 48:A9:8A:B6:5D:5C
- **Domain**: home.bor.labrats.work

## VLAN Configuration

This switch implements a comprehensive VLAN strategy for network segmentation across different environments and purposes.

### VLAN Summary Table

| VLAN ID | Network | Gateway | Domain | Purpose | Environment |
|---------|---------|---------|--------|---------|-------------|
| 10 | 10.0.10.0/24 | 10.0.10.1 | mgmt.bor.labrats.work | Management | Management |
| 11 | 10.0.11.0/24 | 10.0.11.1 | mgmt-vms.bor.labrats.work | Management VMs | Management |
| 20 | 10.0.20.0/24 | 10.0.20.1 | root.prod.bor.labrats.work | Production Root | Production |
| 21 | 10.0.21.0/24 | 10.0.21.1 | infra.cluster.prod.bor.labrats.work | Production K8s Infrastructure | Production |
| 22 | 10.0.22.0/24 | 10.0.22.1 | app.cluster.prod.bor.labrats.work | Production K8s Applications | Production |
| 29 | 10.0.29.0/24 | 10.0.29.1 | ingress.cluster.prod.bor.labrats.work | Production Ingress/DMZ | Production |
| 30 | 10.0.30.0/24 | 10.0.30.1 | staging.bor.labrats.work | Staging | Staging |
| 31 | 10.0.31.0/24 | 10.0.31.1 | staging-vms.bor.labrats.work | Staging VMs | Staging |
| 40 | 10.0.40.0/24 | 10.0.40.1 | dev.bor.labrats.work | Development | Development |
| 41 | 10.0.41.0/24 | 10.0.41.1 | dev-vms.bor.labrats.work | Development VMs | Development |
| 50 | 10.0.50.0/24 | 10.0.50.1 | sandbox.bor.labrats.work | Sandbox | Sandbox |
| 51 | 10.0.51.0/24 | 10.0.51.1 | sandbox-vms.bor.labrats.work | Sandbox VMs | Sandbox |

### Management VLANs (10-11)

**VLAN 10 - Management Network**
- Network: 10.0.10.0/24
- Purpose: Physical infrastructure management (servers, switches, iLO/IPMI)
- DHCP Pool: 10.0.10.10-254
- Lease Time: 8 hours
- Isolation: Isolated from other VLANs
- Access: SSH/WinBox from trusted networks only

**VLAN 11 - Management VM Network**
- Network: 10.0.11.0/24
- Purpose: Management virtual machines
- DHCP Pool: 10.0.11.10-254
- Lease Time: 8 hours
- Isolation: Isolated from other VLANs

### Production VLANs (20-29)

**VLAN 20 - Production Root**
- Network: 10.0.20.0/24
- Purpose: Core production services
- DHCP Pool: 10.0.20.10-254
- Isolation: Isolated from other VLANs

**VLAN 21 - Production K8s Infrastructure**
- Network: 10.0.21.0/24
- Purpose: Kubernetes cluster infrastructure nodes
- DHCP Pool: 10.0.21.10-254
- Isolation: Isolated from other VLANs

**VLAN 22 - Production K8s Applications**
- Network: 10.0.22.0/24
- Purpose: Kubernetes cluster application workloads
- DHCP Pool: 10.0.22.10-254
- Isolation: Isolated from other VLANs
- Special: Accessible from VLAN 29 (ingress) on ports 80/443

**VLAN 29 - Production Ingress (DMZ)**
- Network: 10.0.29.0/24
- Purpose: Public-facing ingress/load balancers
- DHCP Pool: 10.0.29.10-254
- Isolation: DMZ zone, restricted access
- Inbound: Allows HTTP/HTTPS from internet
- Outbound: Limited to VLAN 22 on ports 80/443

### Staging VLANs (30-31)

**VLAN 30 - Staging Network**
- Network: 10.0.30.0/24
- Purpose: Staging environment for testing
- DHCP Pool: 10.0.30.10-254
- Access: Can reach management VLANs on ports 22, 3389, 80, 443

**VLAN 31 - Staging VM Network**
- Network: 10.0.31.0/24
- Purpose: Staging virtual machines
- DHCP Pool: 10.0.31.10-254
- Access: Can reach management VLANs on ports 22, 3389, 80, 443

### Development VLANs (40-41)

**VLAN 40 - Development Network**
- Network: 10.0.40.0/24
- Purpose: Developer workstations and services
- DHCP Pool: 10.0.40.10-254
- Access: Can reach management VLANs, limited internet access (HTTP/HTTPS only)
- Special: Port sfp-sfpplus2-pc1008 (PVID 40)

**VLAN 41 - Development VM Network**
- Network: 10.0.41.0/24
- Purpose: Development virtual machines
- DHCP Pool: 10.0.41.10-254
- Access: Can reach management VLANs

### Sandbox VLANs (50-51)

**VLAN 50 - Sandbox Network**
- Network: 10.0.50.0/24
- Purpose: Experimental/testing environment
- DHCP Pool: 10.0.50.10-254
- Access: Limited access, isolated from production

**VLAN 51 - Sandbox VM Network**
- Network: 10.0.51.0/24
- Purpose: Sandbox virtual machines
- DHCP Pool: 10.0.51.10-254
- Access: Limited access, isolated from production

## Physical Port Configuration

### SFP/SFP+ Ports

| Port | Name | Speed | PVID | Tagged VLANs | Description |
|------|------|-------|------|--------------|-------------|
| sfp-sfpplus1 | sfp-sfpplus1-kvm002 | 10G | 10 | 10,11,20,21,22,30,31,40,41,50,51 | KVM server connection |
| sfp-sfpplus2 | sfp-sfpplus2-pc1008 | Auto | 40 | 10,11,20,21,22,30,31,40,41,50,51 | PC1008 workstation |
| sfp-sfpplus3-13 | (default names) | Auto | - | - | Available ports |
| sfp-sfpplus14 | (default name) | 1G | 10 | - | Management |
| sfp-sfpplus15 | (default name) | 1G | 10 | - | Management |
| sfp-sfpplus16 | (default name) | 1G | 10 | - | Management |

### Bridge Port Assignments

All SFP/SFP+ ports are members of bridge0 with VLAN filtering enabled.

## DHCP Configuration

### DHCP Servers

Each VLAN has its own DHCP server providing automatic IP assignment:

| Server Name | Interface | Pool | Lease Time | Domain |
|-------------|-----------|------|------------|--------|
| dhcp1 | bridge0 | 192.168.1.100-250 | 10 minutes | home.bor.labrats.work |
| vlan10 | vlan10 | 10.0.10.10-254 | 8 hours | mgmt.bor.labrats.work |
| vlan11 | vlan11 | 10.0.11.10-254 | 8 hours | mgmt-vms.bor.labrats.work |
| vlan20 | vlan20 | 10.0.20.10-254 | 8 hours | root.prod.bor.labrats.work |
| vlan21 | vlan21 | 10.0.21.10-254 | 8 hours | infra.cluster.prod.bor.labrats.work |
| vlan22 | vlan22 | 10.0.22.10-254 | 8 hours | app.cluster.prod.bor.labrats.work |
| vlan29 | vlan29 | 10.0.29.10-254 | 8 hours | ingress.cluster.prod.bor.labrats.work |
| vlan30 | vlan30 | 10.0.30.10-254 | 8 hours | staging.bor.labrats.work |
| vlan31 | vlan31 | 10.0.31.10-254 | 8 hours | staging-vms.bor.labrats.work |
| vlan40 | vlan40 | 10.0.40.10-254 | 8 hours | dev.bor.labrats.work |
| vlan41 | vlan41 | 10.0.41.10-254 | 8 hours | dev-vms.bor.labrats.work |
| vlan50 | vlan50 | 10.0.50.10-254 | 8 hours | sandbox.bor.labrats.work |
| vlan51 | vlan51 | 10.0.51.10-254 | 8 hours | sandbox-vms.bor.labrats.work |

### Dynamic DNS from DHCP

DHCP lease script automatically creates DNS entries for all DHCP leases:
- Script: `DHCP2DNS_FULLUPDATE`
- Creates DNS A records with #DHCP comment
- Updates TTL based on lease expiration
- Cleanup script removes stale entries

## DNS Configuration

- **DNS Server**: Enabled
- **Allow Remote Requests**: Yes
- **Upstream DNS**: 192.168.0.1 (D-Link router)
- **Dynamic DNS**: Automatic from DHCP leases
- **Static Entries**: Example: ILOCZ3442F22R.mgmt.bor.labrats.work → 10.0.10.10

## Routing Configuration

### Default Route

- **Default Gateway**: 192.168.0.1 via ether1
- **Routing**: Inter-VLAN routing enabled
- **Masquerade**: NAT to WAN interface

### Inter-VLAN Routing

The switch performs Layer 3 routing between VLANs with firewall rules controlling traffic flow.

## Firewall Configuration

### Input Chain Rules (to router itself)

1. **Allow established/related connections**
2. **Allow ICMP for diagnostics**
3. **Allow SSH (port 22) from trusted networks**
4. **Allow WinBox (port 8291) from trusted networks**
5. **Allow DNS (TCP/UDP 53) from each VLAN to respective gateway**
6. **Allow NTP (UDP 123) from each VLAN to respective gateway**
7. **Allow DHCP (UDP 67-68) from each VLAN to respective gateway**

### Forward Chain Rules (between VLANs)

**Priority 10: Base Rules**
- Allow established/related connections

**Priority 30: Internal Network Services**
- Allow internal networks to DNS servers
- Allow internal networks to NTP servers
- Allow ICMP from internal networks

**Priority 50: Staging/Dev to Management Access**
- VLAN 30 → VLAN 10: ports 22, 3389, 80, 443
- VLAN 31 → VLAN 11: ports 22, 3389, 80, 443
- VLAN 40 → VLAN 10: ports 22, 2222, 80, 443
- VLAN 40 → VLAN 41: ports 22, 2222, 80, 443
- VLAN 40 → 10.0.10.100: port 8006 (Proxmox)
- VLAN 40 → Internet: ports 80, 443
- VLAN 50 → VLAN 10: ports 22, 3389, 80, 443
- VLAN 50 → Internet: ports 80, 443
- VLAN 51 → VLAN 11: ports 22, 3389, 80, 443

**Priority 60-65: Production Ingress (DMZ)**
- VLAN 29 → VLAN 22: ports 80, 443
- Internet → VLAN 29: ports 80, 443
- Block non-HTTP/HTTPS to VLAN 29
- Block VLAN 29 to internal networks

**Priority 70-90: VLAN Isolation**
- Drop all inter-VLAN traffic not explicitly allowed above
- Each VLAN is isolated from other VLANs by default

### Address Lists

**Network Zones:**
- `internal_networks`: 10.0.10/11/20/21/22/30/31/40/41/50/51, 192.168.216.0/24
- `management_networks`: 10.0.10.0/24, 10.0.11.0/24
- `dmz_networks`: 10.0.29.0/24
- `vlan_networks`: All VLAN subnets
- `trusted_networks`: 10.0.10.0/24, 10.0.11.0/24

**External Services:**
- `dns_servers`: 1.1.1.1, 1.0.0.1, 8.8.8.8, 8.8.4.4, 9.9.9.9, 149.112.112.112
- `ntp_servers`: time.cloudflare.com, time.google.com, pool.ntp.org

**Network Lists:**
- `private_networks`: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
- `bogon_networks`: Reserved/invalid IP ranges

## NAT Configuration

### Masquerade Rules

1. **VPN Traffic NAT**: Source NAT for 192.168.89.0/24 (VPN clients)
2. **WAN NAT**: Masquerade all traffic going to WAN interface list
3. **Global NAT**: Masquerade for outbound traffic on ether1

### Dynamic NAT Rules

Script `NATUPDATE` creates dynamic port forwarding:
- Resolves hostname from DHCP
- Creates HTTP (80) and HTTPS (443) NAT rules
- Target: `websrv0001` hostname

## WireGuard VPN

### VPN Configuration

- **Interface**: back-to-home-vpn
- **Listen Port**: 55515
- **MTU**: 1420
- **Cloud Integration**: Enabled with DDNS

### VPN Users

| User | Public Key | LAN Access |
|------|------------|------------|
| thopi | 5KIPtapQNBEyz2RwKc49JsNMm+ApjGdQTTWYB1jt0H0= | Yes |
| glinet | Knm6V3V0EdUde53VdyDL+M5O58nJ5OMRACi2E0aiqEQ= | Yes |
| LAPTOP-MUJJBT1D | HHYywI7w/1aDmbQiFQL18S0KNhCT1Ixso5ay4iRl/A4= | Yes |
| Pixel4 | Z31h2Sfse8Q0T3GLDxOszS7GmvyWGl18T39rax/o7Ss= | Yes |
| gh_action_01 | oFWwct8eXlQPDMPT/13U0akrDLbLGtFHBSUiOFU4TmE= | Yes |

All users have LAN access enabled.

## System Configuration

### Time Zone

- **Time Zone**: Europe/Warsaw
- **NTP Client**: Enabled
- **NTP Servers**: time.google.com, pool.ntp.org

### Cloud Features

- **Cloud Service**: Enabled
- **DDNS**: Enabled
- **Update Interval**: 5 minutes
- **Back-to-Home VPN**: Enabled

### Scripts

**DHCP2DNS_FULLUPDATE**: Automatically creates DNS entries from DHCP leases
**DHCP2DNS_CLEANUP**: Removes stale DNS entries
**NATUPDATE**: Updates dynamic NAT rules for specific hostnames

## Network Security Strategy

### Network Segmentation

The network implements a defense-in-depth strategy with multiple isolated zones:

1. **Management Zone** (VLANs 10-11): Infrastructure management only
2. **Production Zone** (VLANs 20-22, 29): Production workloads with DMZ
3. **Staging Zone** (VLANs 30-31): Pre-production testing
4. **Development Zone** (VLANs 40-41): Development work
5. **Sandbox Zone** (VLANs 50-51): Experimental/testing

### Access Control Model

- **Default Deny**: All inter-VLAN traffic blocked by default
- **Explicit Allow**: Only specific ports/services allowed between zones
- **Management Access**: Restricted to trusted networks
- **DMZ Isolation**: Production ingress (VLAN 29) heavily restricted
- **Internet Access**: Limited to specific VLANs and ports

### Production Security

- Production K8s application network (VLAN 22) only accessible via ingress (VLAN 29)
- Ingress VLAN only allows HTTP/HTTPS
- Production networks isolated from dev/staging/sandbox

## Network Topology

```
Internet
    |
192.168.0.1 (D-Link Router)
    |
    |--- 192.168.0.124 (Living Room WiFi - BE85)
    |--- 192.168.0.171 (Office WiFi - BE85)
    |
    |--- 192.168.0.2 (ether1)
         |
    [MikroTik CRS317]
    192.168.1.1 (bridge0)
         |
         |--- Home Network: 192.168.1.0/24
         |
         |--- Management VLANs:
         |    |--- VLAN 10: 10.0.10.0/24 (mgmt)
         |    |--- VLAN 11: 10.0.11.0/24 (mgmt-vms)
         |
         |--- Production VLANs:
         |    |--- VLAN 20: 10.0.20.0/24 (root.prod)
         |    |--- VLAN 21: 10.0.21.0/24 (k8s-infra.prod)
         |    |--- VLAN 22: 10.0.22.0/24 (k8s-app.prod)
         |    |--- VLAN 29: 10.0.29.0/24 (ingress.prod/DMZ)
         |
         |--- Staging VLANs:
         |    |--- VLAN 30: 10.0.30.0/24 (staging)
         |    |--- VLAN 31: 10.0.31.0/24 (staging-vms)
         |
         |--- Development VLANs:
         |    |--- VLAN 40: 10.0.40.0/24 (dev)
         |    |--- VLAN 41: 10.0.41.0/24 (dev-vms)
         |
         |--- Sandbox VLANs:
              |--- VLAN 50: 10.0.50.0/24 (sandbox)
              |--- VLAN 51: 10.0.51.0/24 (sandbox-vms)

Physical Connections:
    - sfp-sfpplus1-kvm002 (10G): KVM server (PVID 10, tagged all VLANs)
    - sfp-sfpplus2-pc1008: PC workstation (PVID 40, tagged all VLANs)
    - sfp-sfpplus14-16 (1G): Management ports (PVID 10)

VPN Access:
    - WireGuard VPN on port 55515
    - 5 configured VPN users with LAN access
```

## Use Cases & Benefits

### Network Segmentation Benefits

1. **Security Isolation**: Production separated from dev/staging/sandbox
2. **Environment Separation**: Each environment (prod/staging/dev/sandbox) isolated
3. **Blast Radius Containment**: Security incidents contained to single VLAN
4. **Compliance**: Network segmentation for regulatory requirements
5. **Performance**: Separate broadcast domains reduce network noise

### Kubernetes Integration

- Dedicated VLANs for Kubernetes infrastructure and applications
- DMZ/ingress VLAN (29) for public-facing services
- Infrastructure VLAN (21) for control plane
- Application VLAN (22) for workloads

### Development Workflow

- Developers on VLAN 40 can access management infrastructure
- Limited internet access (HTTP/HTTPS only) for security
- Isolated from production to prevent accidental changes
- Access to dev VMs on VLAN 41

## Maintenance & Administration

### Management Access

- **SSH**: Port 22 from trusted networks (10.0.10.0/24, 10.0.11.0/24)
- **WinBox**: Port 8291 from trusted networks
- **Web UI**: Available from trusted networks

### Monitoring & Logging

- Extensive firewall logging enabled
- Log prefixes indicate traffic type and VLAN
- Connection tracking for all rules

### Backup & Configuration

- Configuration exported: 2025-11-01 17:49:44
- Configuration file: `mikrotik-export.rsc`
- Software ID: 67DD-IEY2

## Notes

### Configuration Highlights

- **Comprehensive VLAN Strategy**: 12 VLANs for complete environment separation
- **Zero Trust Network**: Default deny with explicit allow rules
- **Dynamic DNS**: Automatic DNS from DHCP leases
- **WireGuard VPN**: Secure remote access with 5 users
- **Layer 3 Switch**: Full routing capabilities between VLANs
- **Production DMZ**: Dedicated ingress VLAN for public services
- **Kubernetes Ready**: Dedicated VLANs for K8s infrastructure and apps

### Network Design Philosophy

This network implements a **defense-in-depth** security model with:
- Multiple isolated security zones
- Principle of least privilege for inter-VLAN access
- DMZ for public-facing services
- Separate networks for different lifecycle stages (prod/staging/dev/sandbox)

### Scalability

- 16x SFP/SFP+ ports provide room for expansion
- VLAN design allows adding new networks easily
- Firewall rules organized by priority for maintainability
- Dynamic DNS and NAT scripts for automation

---
*Last Updated: 2025-11-01*
*Configuration Exported: 2025-11-01 17:49:44*
*RouterOS Version: 7.18*
