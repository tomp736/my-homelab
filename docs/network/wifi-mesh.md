# WiFi Mesh System

## Overview

- **Technology**: WiFi Access Point System (AP Mode)
- **Number of Nodes**: 2
- **Primary Use**: Wireless coverage extension
- **Network Mode**: Access Point Mode (connected to D-Link router)
- **Management**: Smart DHCP enabled

## Hardware Specifications

### Node 1 (Primary/Main) - Living Room

- **Make/Manufacturer**: TP-Link
- **Model**: BE85
- **Hardware Version**: (To be documented)
- **Serial Number**: (To be documented)
- **MAC Address**: 20:23:51:62:DC:E0
- **Firmware Version**: 1.2.1 Build 20250731 Rel.15505
- **Last Firmware Update**: 2025-07-31
- **Location/Placement**: Living Room
- **Role**: Main node, connected to edge router (D-Link DIR-X1530)
- **IP Address**: 192.168.0.124

### Node 2 (Satellite) - Office

- **Make/Manufacturer**: TP-Link
- **Model**: BE85
- **Hardware Version**: (To be documented)
- **Serial Number**: (To be documented)
- **MAC Address**: 20:23:51:62:DF:4A
- **Firmware Version**: (To be documented - likely same as Node 1)
- **Last Firmware Update**: (To be documented)
- **Location/Placement**: Office
- **Role**: Satellite node
- **IP Address**: 192.168.0.171

## Network Configuration

### IP Addressing

| Node | IP Address | Subnet Mask | Gateway | DHCP/Static | MAC Address |
|------|------------|-------------|---------|-------------|-------------|
| Node 1 (Living Room) | 192.168.0.124 | 255.255.255.0 | 192.168.0.1 | DHCP (Smart) | 20:23:51:62:DC:E0 |
| Node 2 (Office) | 192.168.0.171 | 255.255.255.0 | 192.168.0.1 | DHCP (Smart) | 20:23:51:62:DF:4A |

### Connection to Router

- **Router IP**: 192.168.0.1 (D-Link DIR-X1530)
- **Connection Method**: Wireless (AP Mode)
- **Uplink Port/Interface**: Wireless backhaul to router
- **DHCP**: Smart DHCP enabled (IPs assigned by router)

## Wireless Configuration

### Main Network - D3K0 (2.4 GHz & 5 GHz)

- **Status**: Enabled
- **SSID**: D3K0
- **Bands**: 2.4 GHz and 5 GHz (unified)
- **Channel (2.4 GHz)**: Auto (not accessible via interface)
- **Channel (5 GHz)**: Auto (not accessible via interface)
- **Channel Width**: Auto
- **Transmit Power**: Auto
- **Security**: WPA3/WPA2 (assumed)
- **Password**: (Reference to secure storage)
- **Max Speed**: WiFi 6/6E speeds

### 6 GHz Network - D3K0_6GHz

- **Status**: Enabled
- **SSID**: D3K0_6GHz
- **Band**: 6 GHz
- **Channel**: Auto (not accessible via interface)
- **Channel Width**: Auto
- **Transmit Power**: Auto
- **Security**: WPA3 (required for 6 GHz)
- **Password**: (Reference to secure storage)
- **Max Speed**: WiFi 6E speeds

### MLO Network - D3K0_MLO

- **Status**: Enabled
- **SSID**: D3K0_MLO
- **Technology**: Multi-Link Operation (MLO)
- **Bands**: Multi-band aggregation (2.4/5/6 GHz)
- **Description**: WiFi 7 MLO network for compatible devices
- **Channel**: Auto (managed by MLO)
- **Security**: WPA3 (required for MLO)
- **Password**: (Reference to secure storage)

### Guest Networks

- **Enabled**: Yes
- **Guest SSID**: D3KO_Guest (unified across all bands)
- **2.4 GHz Guest**: Enabled (SSID: D3KO_Guest)
- **5 GHz Guest**: Enabled (SSID: D3KO_Guest)
- **6 GHz Guest**: Enabled (SSID: D3KO_Guest)
- **Isolation**: (To be documented)
- **Access Restrictions**: (To be documented)

## Mesh Configuration

### Mesh Topology

```
D-Link Router - DIR-X1530
IP: 192.168.0.1
         |
         | Wireless Backhaul
         |
    [Living Room Node]
    BE85 - Primary/Main
    IP: 192.168.0.124
    SSIDs: D3K0, D3K0_6GHz, D3K0_MLO
         |
         | Wireless Mesh Backhaul
         |
    [Office Node]
    BE85 - Satellite
    IP: 192.168.0.171
    SSIDs: D3K0, D3K0_6GHz, D3K0_MLO
```

### Backhaul Configuration

- **Backhaul Type**: Wireless
- **Backhaul Band**: (To be documented - likely 5 GHz or 6 GHz)
- **Backhaul Channel**: (To be documented)
- **Backhaul Speed**: (To be documented)
- **Dedicated Backhaul**: (To be documented)
- **Connection Path**:
  - Living Room Node (192.168.0.124) → D-Link Router (192.168.0.1) via wireless
  - Office Node (192.168.0.171) → Living Room Node (192.168.0.124) via wireless mesh backhaul

### Mesh Settings

- **Mesh Network Name**: D3K0 (main SSID)
- **Wireless Network Mode**: High Capacity
- **Fast Roaming (802.11r)**: Disabled
- **Beamforming**: Enabled
- **Seamless Roaming**: (To be documented)
- **Band Steering**: (To be documented)
- **Load Balancing**: (To be documented)

## Connected Devices

### Overall Statistics

- **Total Connected Devices**:
- **2.4 GHz Clients**:
- **5 GHz Clients**:
- **6 GHz Clients**:

### Per-Node Distribution

| Node | Location | Connected Devices | 2.4 GHz | 5 GHz | 6 GHz |
|------|----------|-------------------|---------|-------|-------|
| Node 1 (192.168.0.124) | Living Room | (To be documented) | | | |
| Node 2 (192.168.0.171) | Office | (To be documented) | | | |

## Coverage & Performance

### Coverage Areas

- **Node 1 (Living Room) Coverage**: Primary coverage for living room and adjacent areas
- **Node 2 (Office) Coverage**: Primary coverage for office and adjacent areas
- **Total Coverage Area**: (To be documented)
- **Overlap Zones**: (To be documented - likely between living room and office)

### Performance Metrics

- **Average Signal Strength**:
- **Roaming Performance**:
- **Backhaul Stability**:

## Advanced Features

### WiFi Standards Supported

- **WiFi 7 (802.11be)**: Supported (MLO network enabled)
- **WiFi 6E (802.11ax)**: Supported (6 GHz band)
- **WiFi 6 (802.11ax)**: Supported
- **WiFi 5 (802.11ac)**: Supported (backward compatibility)
- **WiFi 4 (802.11n)**: Supported (backward compatibility)

### Wireless Features

- **Beamforming**: Enabled
- **Network Mode**: High Capacity
- **Fast Roaming (802.11r)**: Disabled
- **MU-MIMO**: (To be documented)
- **OFDMA**: (To be documented)

### Quality of Service (QoS)

- **QoS Enabled**:
- **Priority Rules**:

### Access Control

- **MAC Filtering**:
- **Access Schedule**:

### Parental Controls

- **Enabled**:
- **Profiles**:

## Management & Monitoring

### Management Interface

- **Access Method**: Web / Mobile App / Both
- **Management URL/App**:
- **Admin Access**:

### Monitoring Features

- **Real-time Client Monitoring**:
- **Traffic Statistics**:
- **Health Monitoring**:
- **Alerts/Notifications**:

## Integration with Network

### DHCP

- **DHCP Server**: Disabled (handled by router 192.168.0.1)
- **IP Assignment**: From router DHCP pool

### VLANs

- **VLAN Support**:
- **VLANs Configured**:

### Network Services

- **DNS**: Forwarded to router
- **NTP**:

## Maintenance History

| Date | Node | Action | Version/Details | Notes |
|------|------|--------|-----------------|-------|
|      |      |        |                 |       |

## Notes

### Configuration Highlights
- **Manufacturer**: TP-Link BE85 WiFi 7 access points
- **WiFi 7 Support**: BE85 devices support WiFi 7 (802.11be) with Multi-Link Operation (MLO)
- **Multiple SSIDs**: Three main networks (D3K0, D3K0_6GHz, D3K0_MLO) plus guest networks
- **Access Point Mode**: Devices operate as APs, routing handled by D-Link router
- **Smart DHCP**: Automatic IP management for seamless roaming
- **Wireless Backhaul**: Inter-node communication via wireless (no Ethernet backhaul)
- **Full Band Support**: 2.4 GHz, 5 GHz, and 6 GHz bands all enabled
- **Guest Network**: Separate guest access on all three bands
- **Beamforming**: Enabled for improved signal directionality
- **High Capacity Mode**: Optimized for many simultaneous connections
- **Fast Roaming**: Disabled (802.11r not in use)

### Key Features
- **MLO Network**: Allows compatible WiFi 7 devices to use multiple bands simultaneously for improved throughput and reliability
- **6 GHz Dedicated Network**: Separate SSID for 6 GHz band for devices that support it
- **Unified 2.4/5 GHz**: Single SSID for seamless roaming between 2.4 and 5 GHz

### Data Collection
- Initial configuration gathered from management interface
- Firmware version: 1.2.1 Build 20250731 Rel.15505 (July 2025)
- Additional details to be documented: IP addresses, serial numbers, channels, connected devices

### Outstanding Items
- ✅ ~~IP addresses for both nodes~~ (Living Room 192.168.0.124, Office 192.168.0.171)
- ✅ ~~Physical placement/locations of nodes~~ (Living Room and Office)
- ✅ ~~MAC addresses for both nodes~~ (20:23:51:62:DC:E0 and 20:23:51:62:DF:4A)
- ✅ ~~Manufacturer/brand confirmation~~ (TP-Link BE85)
- ✅ ~~Wireless features~~ (Beamforming enabled, Fast roaming disabled, High Capacity mode)
- ✅ ~~Guest network SSIDs~~ (D3KO_Guest for all bands)
- Serial numbers and hardware versions (not critical)
- Detailed channel assignments (not accessible via management interface - auto-managed)
- Connected device counts and distribution (not available at this time)
- Additional mesh settings details (seamless roaming, band steering, load balancing status)

---
*Last Updated: 2025-11-01*
