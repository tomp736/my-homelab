# desk001 - Main Desktop Workstation

## Overview

**Purpose:** Primary development and workstation computer
**Location:** Office
**Network Connection:** WiFi (wlp8s0) via TP-Link BE85 mesh
**Primary Functions:**
- Software development
- AI/ML workloads
- Container orchestration (Docker)
- General-purpose computing

**Connection Details:**
- Connected to: TP-Link BE85 WiFi mesh network
- Network: 192.168.0.0/24
- Upstream Gateway: 192.168.0.1

---

## Hardware Specifications

### Motherboard
- **Manufacturer:** ASRock
- **Model:** X570 Taichi
- **Firmware Version:** P1.80
- **Firmware Date:** August 8, 2019
- **Chassis Type:** Desktop

### Processor
- **Model:** AMD Ryzen 9 3900X 12-Core Processor
- **Architecture:** x86-64
- **Cores:** 12 physical cores
- **Threads:** 24 (2 threads per core)
- **Base Frequency:** 2200 MHz
- **Max Frequency:** 4672 MHz
- **NUMA Configuration:** Single node (node0: CPUs 0-23)

### Memory
- **Total RAM:** 30 GiB
- **Used:** ~12 GiB
- **Available:** ~17 GiB
- **Buffer/Cache:** ~17 GiB
- **Swap:** 8.0 GiB (356 KiB used)

### Graphics
- **GPU:** AMD Radeon RX 470/480/570/570X/580/580X/590
- **Manufacturer:** Advanced Micro Devices, Inc. [AMD/ATI]
- **Model:** Ellesmere (rev e7)
- **Bus:** PCIe 10:00.0

### Storage Configuration

#### Primary System Drive
- **Device:** /dev/nvme0n1 (465.8 GB NVMe)
  - **Partition 1:** 1 GB EFI boot partition (vfat, mounted at /boot/efi, 1% used)
  - **Partition 2:** 464.7 GB root partition (ext4, mounted at /, 48% used - 205GB/457GB)

#### Secondary NVMe Drives
- **Device:** /dev/nvme1n1 (931.5 GB)
  - **Partition 1:** 931.5 GB (ZFS member - not currently mounted)

- **Device:** /dev/nvme2n1 (465.8 GB)
  - **Partition 1:** 600 MB
  - **Partition 2:** 1 GB (XFS)
  - **Partition 3:** 464.2 GB (crypto_LUKS encrypted)

#### HDD Array (ZFS Members)
Seven 3.6 TB hard drives configured as ZFS members (currently not mounted):
- /dev/sda - 3.6 TB (ZFS member)
- /dev/sdb - 3.6 TB (ZFS member)
- /dev/sdc - 3.6 TB (ZFS member)
- /dev/sdd - 3.6 TB (ZFS member)
- /dev/sde - 3.6 TB (ZFS member)
- /dev/sdf - 3.6 TB (ZFS member)
- /dev/sdg - 3.6 TB (ZFS member)

**Total Raw Storage Capacity:** ~27 TB (HDD array) + 1.86 TB (NVMe)

**Note:** ZFS pools are not currently active. Drives are members of ZFS pools but pools may need to be imported.

---

## Operating System

- **Distribution:** Ubuntu 25.10
- **Kernel:** Linux 6.17.0-6-generic
- **Architecture:** x86-64
- **Machine ID:** 3a03cdbbed7d476081e12a100dad3342
- **Boot ID:** 68f63fb6626648b6bf082b7f37ccedc8
- **Hostname:** desk001

---

## System Status

**Last Checked:** 2025-11-13

- **Uptime:** 16 hours, 5 minutes
- **Load Average:** 12.06 (1 min), 11.49 (5 min), 7.21 (15 min)
- **Active Users:** 1
- **System Load:** High (consistent load above core count - likely running ML/AI workloads)

---

## Network Configuration

### Network Interfaces

#### Primary Interface (WiFi)
- **Interface:** wlp8s0
- **Status:** UP
- **Type:** WiFi 6E
- **MAC Address:** 3c:f0:11:db:ac:95
- **IPv4 Address:** 192.168.0.163/24
- **IPv6 Address:** fe80::6a3c:b4bb:82a3:b855/64
- **Connection:** TP-Link BE85 WiFi mesh network

#### Ethernet Interfaces (Unused)
- **Interface:** enp10s0
  - **Status:** DOWN
  - **MAC Address:** 70:85:c2:d8:87:e3

- **Interface:** enp15s0
  - **Status:** DOWN
  - **MAC Address:** 24:8a:07:e3:e9:40

- **Interface:** enx90cc248b23fa
  - **Status:** DOWN
  - **Type:** USB Ethernet adapter

#### Virtual/Container Interfaces
- **Interface:** lo (Loopback)
  - **Status:** UNKNOWN (active)
  - **IPv4:** 127.0.0.1/8
  - **IPv6:** ::1/128

- **Interface:** docker0
  - **Status:** DOWN
  - **Network:** 172.17.0.0/16
  - **Bridge IP:** 172.17.0.1/16
  - **IPv6:** fe80::6cb7:45ff:fec6:e2c4/64

- **Interface:** br-d9c2dd8c0587 (Docker bridge)
  - **Status:** UP
  - **Network:** 172.18.0.0/16
  - **Bridge IP:** 172.18.0.1/16
  - **IPv6:** fe80::5c1a:34ff:fe6a:698b/64

- **Interface:** veth18941b5@if2 (Container veth pair)
  - **Status:** UP
  - **IPv6:** fe80::c4d5:daff:fec8:1099/64

---

## IP Addressing & Routing

### IP Configuration
- **Primary IP:** 192.168.0.163/24 (DHCP assigned)
- **Gateway:** 192.168.0.1
- **DNS Server:** 127.0.0.53 (systemd-resolved local stub)
- **Network:** 192.168.0.0/24

### Routing Table
```
default via 192.168.0.1 dev wlp8s0 proto dhcp src 192.168.0.163 metric 600
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
172.18.0.0/16 dev br-d9c2dd8c0587 proto kernel scope link src 172.18.0.1
192.168.0.0/24 dev wlp8s0 proto kernel scope link src 192.168.0.163 metric 600
```

### DNS Configuration
- **Primary DNS:** 127.0.0.53 (systemd-resolved)
- **Upstream DNS:** Configured via DHCP from 192.168.0.1

---

## Software & Services

### Container Platform
- **Docker:** Active
  - **Default Bridge:** docker0 (172.17.0.0/16)
  - **Custom Bridge:** br-d9c2dd8c0587 (172.18.0.0/16)
  - **Active Containers:** At least 1 (veth pair detected)

### Development Tools
- **Python:** Installed (evidence: /home/u0/code/my-diet/ml-api/ project)
- **Git:** Active (homelab repository)
- **Claude Code:** Active (AI coding assistant)

### File Systems
- **ext4:** Primary system filesystem
- **vfat:** EFI boot partition
- **ZFS:** Configured but pools not currently imported
- **LUKS:** Encrypted partition on nvme2n1p3

---

## Network Topology

```
Internet
    |
    v
[192.168.0.1 - Gateway/Router]
    |
    | WiFi Connection
    v
[TP-Link BE85 WiFi Mesh]
    |
    | WiFi 6E (wlp8s0)
    v
[desk001 - 192.168.0.163]
    |
    +-- Docker Network (172.17.0.0/16)
    |   |
    |   +-- docker0 (172.17.0.1)
    |
    +-- Docker Network (172.18.0.0/16)
        |
        +-- br-d9c2dd8c0587 (172.18.0.1)
        |
        +-- Container(s) (veth pairs)
```

---

## Performance Notes

- **High CPU Load:** System consistently shows load averages above 12, indicating heavy computational workload
  - Likely running ML/AI training or inference
  - 24-thread CPU handling significant parallel workloads

- **Memory Usage:** Moderate usage at ~40% (12GB/30GB)
  - Healthy buffer/cache utilization
  - Minimal swap usage

- **Storage:** Primary drive at 48% capacity (205GB/457GB used)
  - Large ZFS array (~27TB raw) available but not currently mounted

---

## Security Configuration

### Network Security
- **Firewall:** Default Ubuntu firewall (ufw/iptables)
- **SSH:** Status unknown (not documented)
- **Connection Type:** WiFi (encrypted with WPA3/WPA2)

### Disk Encryption
- LUKS encrypted partition detected on nvme2n1p3 (464GB)

---

## Network Access & Connectivity

### Current Network Placement
- **Network:** 192.168.0.0/24 (likely Management or General Access network)
- **Connection Method:** WiFi via TP-Link BE85 mesh
- **Gateway:** 192.168.0.1

### Available Wired Connections
- **2x Ethernet Ports:** Currently unused (enp10s0, enp15s0)
  - Could be used for:
    - 10G connection to MikroTik CRS317 (if available)
    - Dedicated VLAN connection
    - Link aggregation for higher bandwidth

### Potential VLAN Assignment
Based on the homelab MikroTik configuration, desk001 could be assigned to:
- **VLAN 10 (Management):** 10.0.10.0/24 - For administrative access
- **VLAN 40 (Development):** 10.0.40.0/24 - For development workstation (like pc1008)
- **VLAN 90 (Sandbox):** 10.0.90.0/24 - For testing/experimental work

**Current Status:** Not yet integrated into VLAN segmentation, using flat 192.168.0.0/24 network

---

## Maintenance & Administration

### Access Methods
- **Physical Access:** Local keyboard/monitor
- **SSH:** Likely enabled (standard Ubuntu installation)
- **Remote Desktop:** Not documented

### Configuration Management
- Git repositories active:
  - `/home/u0/code/my-homelab` - Infrastructure documentation
  - `/home/u0/code/my-diet` - Application project

### Monitoring
- **System Monitoring:** Standard Linux tools (top, htop, systemd)
- **Container Monitoring:** Docker stats available

---

## Future Improvements

1. **Network Integration**
   - Connect via wired Ethernet to MikroTik CRS317
   - Assign to appropriate VLAN (Development or Management)
   - Enable 10G connection if available

2. **Storage Management**
   - Import and configure ZFS pools
   - Document ZFS pool layout and redundancy
   - Set up automated backups

3. **Performance Optimization**
   - Investigate high load average (>12)
   - Document running services and workloads
   - Consider CPU/RAM upgrades if needed

4. **Security Hardening**
   - Document and configure firewall rules
   - Set up fail2ban for SSH protection
   - Enable automatic security updates

5. **Documentation**
   - Document installed software and services
   - Create backup and disaster recovery procedures
   - Document ZFS pool configuration when activated

---

## Notes

- **Data Collection Date:** 2025-11-13
- **Data Collection Method:** Direct system commands via Claude Code
- **Primary Use Case:** Development workstation with AI/ML capabilities
- **Unique Features:**
  - Large ZFS storage array (~27TB)
  - High-performance 12-core CPU
  - AMD GPU for compute workloads
  - Active Docker containerization platform

**Hardware Highlights:**
- AMD Ryzen 9 3900X is a powerful workstation-class CPU
- X570 Taichi motherboard supports PCIe 4.0 and high-speed storage
- Extensive storage capacity suitable for data hoarding or media server
- Radeon GPU suitable for compute tasks and light gaming

**Network Considerations:**
- Currently using WiFi which may limit throughput for large file transfers
- Would benefit from wired 10G connection to core switch
- Has multiple unused Ethernet ports available for wired connectivity