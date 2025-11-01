# Internal Office Router

## Overview

- **Purpose**:
- **Location**: Office
- **Connection**: Connected to Office BE85 WiFi node (192.168.0.171)
- **Function**: Internal network segmentation / routing

## Hardware Specifications

- **Make/Manufacturer**:
- **Model**:
- **Hardware Version**:
- **Serial Number**:
- **Firmware Version**:
- **Last Firmware Update**:

## Device Status

- **Uptime**:
- **Load Average**:

## Network Interfaces

| Interface | IP Address | Subnet Mask | Purpose | VLAN | Status |
|-----------|------------|-------------|---------|------|--------|
| WAN       |            |             | Connection to main network |      |        |
| LAN       |            |             | Office internal network |      |        |

### Connection to Main Network

- **Upstream Device**: Office BE85 WiFi node (192.168.0.171)
- **Connection Method**: Wired / Wireless
- **Physical Port/Interface**:
- **WAN MAC Address**:
- **LAN MAC Address**:

## IP Addressing Scheme

### WAN Configuration (Uplink to Main Network)

- **WAN IP**:
- **Subnet Mask**:
- **Gateway**: (likely 192.168.0.1 or 192.168.0.171)
- **Connection Type**: Static / DHCP
- **DNS Servers**:

### LAN Configuration (Office Internal Network)

- **Network**:
- **Gateway/Router IP**:
- **Subnet Mask**:
- **Broadcast**:
- **Available Addresses**:

### Network Segmentation

- **Main Network**: 192.168.0.0/24 (D-Link router)
- **Office Network**: (This router's internal network)
- **Isolation**: Are networks isolated or can they communicate?

## Routing Configuration

### Default Route

- **Default Gateway**:
- **Interface**:

### Static Routes

| Destination | Gateway | Interface | Metric | Purpose |
|-------------|---------|-----------|--------|---------|
|             |         |           |        |         |

### Routing Table
```
# Output from routing table command

```

### Inter-Network Routing

- **Can office devices reach main network?**:
- **Can main network devices reach office network?**:
- **Routing method**:

## NAT/PAT Configuration

### NAT Status

- **NAT Enabled**: Yes / No
- **NAT Type**: Source NAT / Double NAT
- **Impact**: (e.g., double NAT scenario)

### Port Forwarding Rules

| External Port | Internal IP | Internal Port | Protocol | Service |
|---------------|-------------|---------------|----------|---------|
|               |             |               |          |         |

### NAT Rules
```
# NAT configuration details

```

## DHCP Configuration

- **DHCP Server Enabled**:
- **DHCP Range**:
- **Lease Time**:
- **DNS Servers Provided**:

### DHCP Reservations

| MAC Address | IP Address | Hostname | Description |
|-------------|------------|----------|-------------|
|             |            |          |             |

## DNS Configuration

- **Primary DNS**:
- **Secondary DNS**:
- **DNS Forwarder Enabled**:
- **Local Domain**:

## Wireless Configuration

### WiFi Status

- **WiFi Enabled**:
- **SSID(s)**:
- **Bands**:
- **Purpose**: (if different from main WiFi network)

## Firewall Configuration

### Firewall Rules

- **Default Policy**:
- **Custom Rules**:

### Security Features

- **Firewall Type**:
- **Stateful Inspection**:
- **DoS Protection**:

## VPN Configuration

- **VPN Server Enabled**:
- **VPN Type**:
- **VPN Purpose**:

## Advanced Features

### QoS/Traffic Shaping

- **QoS Enabled**:
- **Configuration**:

### VLANs

- **VLAN Support**:
- **VLANs Configured**:

## Connected Devices

### Device Statistics

- **Total Connected Devices**:
- **Wired Connections**:
- **Wireless Connections**:

### Notable Devices

| Device Type | IP Address | MAC Address | Hostname | Purpose |
|-------------|------------|-------------|----------|---------|
|             |            |             |          |         |

## Network Topology

```
Main Network (192.168.0.0/24)
         |
    D-Link Router (192.168.0.1)
         |
         |
    Office WiFi Node (192.168.0.171)
    TP-Link BE85 Satellite
         |
         | [Wired/Wireless Connection]
         |
    [Office Router - WAN Side]
         |
         | [Office Internal Network]
         |
    Office Devices (LAN Side)
```

## Use Case & Purpose

### Primary Purpose

- **Network Segmentation**:
- **Additional Ports**:
- **Specific Routing**:
- **Security Isolation**:

### Benefits

-
-

### Considerations

- **Double NAT**: (if applicable)
- **Performance Impact**:
- **Management Complexity**:

## Integration with Main Network

### Access Between Networks

- **Office → Main Network**:
- **Main Network → Office**:
- **Port Forwarding Through Both Routers**:

### DNS Resolution

- **Office devices resolve via**:
- **Cross-network name resolution**:

## Maintenance History

| Date | Action | Version/Details | Notes |
|------|--------|-----------------|-------|
|      |        |                 |       |

## Notes

### Configuration Summary
-
-

### Known Issues
-
-

### Future Improvements
-
-

---
*Last Updated: 2025-11-01*
