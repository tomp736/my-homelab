# WiFi Mesh System

## Overview

- **Technology**: WiFi Access Point System (AP Mode)
- **Number of Nodes**: 2
- **Primary Use**: Wireless coverage extension
- **Network Mode**: Access Point Mode (connected to D-Link router)
- **Management**: Smart DHCP enabled

## Hardware Specifications

### Node 1 (Primary/Main)

- **Make/Manufacturer**: (To be documented)
- **Model**: BE85
- **Hardware Version**: (To be documented)
- **Serial Number**: (To be documented)
- **Firmware Version**: 1.2.1 Build 20250731 Rel.15505
- **Last Firmware Update**: 2025-07-31
- **Location/Placement**: (To be documented)

### Node 2 (Satellite)

- **Make/Manufacturer**: (To be documented)
- **Model**: BE85
- **Hardware Version**: (To be documented)
- **Serial Number**: (To be documented)
- **Firmware Version**: (To be documented - likely same as Node 1)
- **Last Firmware Update**: (To be documented)
- **Location/Placement**: (To be documented)

## Network Configuration

### IP Addressing

| Node | IP Address | Subnet Mask | Gateway | DHCP/Static | MAC Address |
|------|------------|-------------|---------|-------------|-------------|
| Node 1 (Primary) | | | | | |
| Node 2 (Satellite) | | | | | |

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
- **Channel (2.4 GHz)**: (To be documented)
- **Channel (5 GHz)**: (To be documented)
- **Channel Width**: (To be documented)
- **Transmit Power**: (To be documented)
- **Security**: (To be documented)
- **Password**: (Reference to secure storage)
- **Max Speed**: (To be documented)

### 6 GHz Network - D3K0_6GHz

- **Status**: Enabled
- **SSID**: D3K0_6GHz
- **Band**: 6 GHz
- **Channel**: (To be documented)
- **Channel Width**: (To be documented)
- **Transmit Power**: (To be documented)
- **Security**: (To be documented)
- **Password**: (Reference to secure storage)
- **Max Speed**: (To be documented)

### MLO Network - D3K0_MLO

- **Status**: Enabled
- **SSID**: D3K0_MLO
- **Technology**: Multi-Link Operation (MLO)
- **Bands**: Multi-band aggregation
- **Description**: WiFi 7 MLO network for compatible devices
- **Channel**: (To be documented)
- **Security**: (To be documented)
- **Password**: (Reference to secure storage)

### Guest Networks

- **Enabled**: Yes
- **2.4 GHz Guest**: Enabled
- **5 GHz Guest**: Enabled
- **6 GHz Guest**: Enabled
- **Guest SSID(s)**: (To be documented)
- **Isolation**: (To be documented)
- **Access Restrictions**: (To be documented)

## Mesh Configuration

### Mesh Topology

```
[Diagram showing mesh node placement and connections]

Router (192.168.0.1)
         |
         | (wired/wireless)
         |
    [Node 1 - Primary]
         |
         | Mesh Backhaul
         |
    [Node 2 - Satellite]
```

### Backhaul Configuration

- **Backhaul Type**: Wireless
- **Backhaul Band**: (To be documented - likely 5 GHz or 6 GHz)
- **Backhaul Channel**: (To be documented)
- **Backhaul Speed**: (To be documented)
- **Dedicated Backhaul**: (To be documented)
- **Connection**: Node 1 → Router (wireless), Node 2 → Node 1 or Router (wireless)

### Mesh Settings

- **Mesh Network Name**:
- **Seamless Roaming**: Enabled / Disabled
- **Band Steering**: Enabled / Disabled
- **Fast Roaming (802.11r)**: Enabled / Disabled
- **Load Balancing**: Enabled / Disabled

## Connected Devices

### Overall Statistics

- **Total Connected Devices**:
- **2.4 GHz Clients**:
- **5 GHz Clients**:
- **6 GHz Clients**:

### Per-Node Distribution

| Node | Connected Devices | 2.4 GHz | 5 GHz | 6 GHz |
|------|-------------------|---------|-------|-------|
| Node 1 | | | | |
| Node 2 | | | | |

## Coverage & Performance

### Coverage Areas

- **Node 1 Coverage**:
- **Node 2 Coverage**:
- **Total Coverage Area**:
- **Overlap Zones**:

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
- **WiFi 7 Support**: BE85 devices support WiFi 7 (802.11be) with Multi-Link Operation (MLO)
- **Multiple SSIDs**: Three main networks (D3K0, D3K0_6GHz, D3K0_MLO) plus guest networks
- **Access Point Mode**: Devices operate as APs, routing handled by D-Link router
- **Smart DHCP**: Automatic IP management for seamless roaming
- **Wireless Backhaul**: Inter-node communication via wireless (no Ethernet backhaul)
- **Full Band Support**: 2.4 GHz, 5 GHz, and 6 GHz bands all enabled
- **Guest Network**: Separate guest access on all three bands

### Key Features
- **MLO Network**: Allows compatible WiFi 7 devices to use multiple bands simultaneously for improved throughput and reliability
- **6 GHz Dedicated Network**: Separate SSID for 6 GHz band for devices that support it
- **Unified 2.4/5 GHz**: Single SSID for seamless roaming between 2.4 and 5 GHz

### Data Collection
- Initial configuration gathered from management interface
- Firmware version: 1.2.1 Build 20250731 Rel.15505 (July 2025)
- Additional details to be documented: IP addresses, serial numbers, channels, connected devices

### Outstanding Items
- IP addresses for both nodes
- Serial numbers and hardware versions
- Manufacturer/brand confirmation (likely TP-Link based on BE85 model)
- Detailed channel assignments for each band
- Guest network SSIDs and configuration
- Connected device counts and distribution
- Physical placement/locations of nodes
- Specific mesh/roaming settings enabled

---
*Last Updated: 2025-11-01*
