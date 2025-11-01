# Homelab Network Diagram

## Overall Network Topology

```mermaid
graph TB
    Internet((Internet))
    ISP[ISP Gateway<br/>109.206.198.129]

    Internet --> ISP
    ISP --> |WAN: 109.206.198.193/25| EdgeRouter

    EdgeRouter[D-Link DIR-X1530<br/>Edge Router<br/>192.168.0.1]

    EdgeRouter --> |192.168.0.2| MikroTik
    EdgeRouter -.Wireless.-> WiFiLR

    MikroTik[MikroTik CRS317<br/>Core Switch<br/>192.168.0.2<br/>bridge0: 192.168.1.1]

    WiFiLR[TP-Link BE85<br/>Living Room<br/>192.168.0.124]
    WiFiOffice[TP-Link BE85<br/>Office<br/>192.168.0.171]

    WiFiLR -.Wireless Mesh.-> WiFiOffice

    MikroTik --> |sfp-sfpplus1<br/>10G| KVM[KVM Server<br/>kvm002]
    MikroTik --> |sfp-sfpplus2| PC[PC Workstation<br/>pc1008<br/>VLAN 40]
    MikroTik --> |sfp-sfpplus14-16<br/>1G| MgmtPorts[Management Ports<br/>VLAN 10]

    style Internet fill:#e1f5ff
    style ISP fill:#fff4e1
    style EdgeRouter fill:#ffe1e1
    style MikroTik fill:#e1ffe1
    style WiFiLR fill:#f0e1ff
    style WiFiOffice fill:#f0e1ff
```

## Detailed Network Architecture

```mermaid
graph TB
    subgraph External
        Internet((Internet))
        ISP[ISP Gateway<br/>109.206.198.129]
    end

    subgraph Edge["Edge Network - 192.168.0.0/24"]
        Router[D-Link DIR-X1530<br/>192.168.0.1<br/>WAN: 109.206.198.193]
        WiFi1[BE85 Living Room<br/>192.168.0.124]
        WiFi2[BE85 Office<br/>192.168.0.171]
        Core[MikroTik CRS317<br/>192.168.0.2]
    end

    subgraph Management["Management VLANs"]
        VLAN10[VLAN 10<br/>10.0.10.0/24<br/>mgmt.bor.labrats.work<br/>Physical Infrastructure]
        VLAN11[VLAN 11<br/>10.0.11.0/24<br/>mgmt-vms.bor.labrats.work<br/>Management VMs]
    end

    subgraph Production["Production VLANs"]
        VLAN20[VLAN 20<br/>10.0.20.0/24<br/>root.prod.bor.labrats.work<br/>Core Services]
        VLAN21[VLAN 21<br/>10.0.21.0/24<br/>infra.cluster.prod<br/>K8s Infrastructure]
        VLAN22[VLAN 22<br/>10.0.22.0/24<br/>app.cluster.prod<br/>K8s Applications]
        VLAN29[VLAN 29<br/>10.0.29.0/24<br/>ingress.cluster.prod<br/>DMZ/Ingress]
    end

    subgraph Staging["Staging VLANs"]
        VLAN30[VLAN 30<br/>10.0.30.0/24<br/>staging.bor.labrats.work]
        VLAN31[VLAN 31<br/>10.0.31.0/24<br/>staging-vms.bor.labrats.work]
    end

    subgraph Development["Development VLANs"]
        VLAN40[VLAN 40<br/>10.0.40.0/24<br/>dev.bor.labrats.work]
        VLAN41[VLAN 41<br/>10.0.41.0/24<br/>dev-vms.bor.labrats.work]
    end

    subgraph Sandbox["Sandbox VLANs"]
        VLAN50[VLAN 50<br/>10.0.50.0/24<br/>sandbox.bor.labrats.work]
        VLAN51[VLAN 51<br/>10.0.51.0/24<br/>sandbox-vms.bor.labrats.work]
    end

    Internet --> ISP
    ISP --> Router
    Router --> Core
    Router -.Wireless.-> WiFi1
    WiFi1 -.Mesh.-> WiFi2

    Core --> Management
    Core --> Production
    Core --> Staging
    Core --> Development
    Core --> Sandbox

    style Internet fill:#e1f5ff
    style ISP fill:#fff4e1
    style Router fill:#ffe1e1
    style Core fill:#90EE90
    style WiFi1 fill:#DDA0DD
    style WiFi2 fill:#DDA0DD
```

## VLAN Security Zones

```mermaid
graph LR
    subgraph Internet_Zone["Internet"]
        WAN[WAN<br/>109.206.198.193]
    end

    subgraph DMZ["DMZ Zone"]
        VLAN29[VLAN 29<br/>Ingress/DMZ<br/>10.0.29.0/24]
    end

    subgraph Prod["Production Zone"]
        VLAN20[VLAN 20<br/>Root]
        VLAN21[VLAN 21<br/>K8s Infra]
        VLAN22[VLAN 22<br/>K8s Apps]
    end

    subgraph Mgmt["Management Zone"]
        VLAN10[VLAN 10<br/>Physical]
        VLAN11[VLAN 11<br/>VMs]
    end

    subgraph NonProd["Non-Production Zones"]
        subgraph Stg["Staging"]
            VLAN30[VLAN 30]
            VLAN31[VLAN 31]
        end
        subgraph Dev["Development"]
            VLAN40[VLAN 40]
            VLAN41[VLAN 41]
        end
        subgraph Sbx["Sandbox"]
            VLAN50[VLAN 50]
            VLAN51[VLAN 51]
        end
    end

    WAN -->|HTTP/HTTPS| VLAN29
    VLAN29 -->|HTTP/HTTPS| VLAN22
    NonProd -.->|Limited| Mgmt
    NonProd -->|Limited| WAN

    style WAN fill:#ffe1e1
    style VLAN29 fill:#fff4e1
    style Prod fill:#e1ffe1
    style Mgmt fill:#e1f5ff
    style NonProd fill:#f0e1ff
```

## WiFi Network Architecture

```mermaid
graph TB
    Router[D-Link Router<br/>192.168.0.1]

    Router -.Wireless Backhaul.-> Living[TP-Link BE85<br/>Living Room<br/>192.168.0.124<br/>MAC: 20:23:51:62:DC:E0]

    Living -.Wireless Mesh.-> Office[TP-Link BE85<br/>Office<br/>192.168.0.171<br/>MAC: 20:23:51:62:DF:4A]

    Living --> SSID1[D3K0<br/>2.4GHz + 5GHz<br/>WPA2/WPA3]
    Living --> SSID2[D3K0_6GHz<br/>6GHz<br/>WPA3]
    Living --> SSID3[D3K0_MLO<br/>WiFi 7 MLO<br/>WPA3]
    Living --> Guest1[D3KO_Guest<br/>All Bands]

    Office --> SSID4[D3K0<br/>2.4GHz + 5GHz<br/>WPA2/WPA3]
    Office --> SSID5[D3K0_6GHz<br/>6GHz<br/>WPA3]
    Office --> SSID6[D3K0_MLO<br/>WiFi 7 MLO<br/>WPA3]
    Office --> Guest2[D3KO_Guest<br/>All Bands]

    style Router fill:#ffe1e1
    style Living fill:#DDA0DD
    style Office fill:#DDA0DD
    style SSID1 fill:#e1f5ff
    style SSID2 fill:#e1f5ff
    style SSID3 fill:#90EE90
    style SSID4 fill:#e1f5ff
    style SSID5 fill:#e1f5ff
    style SSID6 fill:#90EE90
    style Guest1 fill:#fff4e1
    style Guest2 fill:#fff4e1
```

## Network Address Summary

### Edge Network (192.168.0.0/24)
- **192.168.0.1** - D-Link DIR-X1530 (Edge Router)
- **192.168.0.2** - MikroTik CRS317 (Core Switch) - DHCP reservation
- **192.168.0.100-199** - DHCP pool
- **192.168.0.124** - TP-Link BE85 Living Room
- **192.168.0.171** - TP-Link BE85 Office

### MikroTik Internal Networks

#### Management VLANs
- **10.0.10.0/24** - VLAN 10 (Physical infrastructure management)
- **10.0.11.0/24** - VLAN 11 (Management VMs)

#### Production VLANs
- **10.0.20.0/24** - VLAN 20 (Production root services)
- **10.0.21.0/24** - VLAN 21 (Kubernetes infrastructure)
- **10.0.22.0/24** - VLAN 22 (Kubernetes applications)
- **10.0.29.0/24** - VLAN 29 (DMZ/Ingress)

#### Staging VLANs
- **10.0.30.0/24** - VLAN 30 (Staging environment)
- **10.0.31.0/24** - VLAN 31 (Staging VMs)

#### Development VLANs
- **10.0.40.0/24** - VLAN 40 (Development workstations)
- **10.0.41.0/24** - VLAN 41 (Development VMs)

#### Sandbox VLANs
- **10.0.50.0/24** - VLAN 50 (Sandbox environment)
- **10.0.51.0/24** - VLAN 51 (Sandbox VMs)

## Traffic Flow Rules

### Internet Access
- **VLAN 29 (DMZ)**: Inbound HTTP/HTTPS allowed
- **VLAN 40 (Dev)**: Outbound HTTP/HTTPS only
- **VLAN 50 (Sandbox)**: Outbound HTTP/HTTPS only
- **Other VLANs**: No direct internet access (isolated)

### Inter-VLAN Communication
- **Default Policy**: DENY (all VLANs isolated)
- **VLAN 29 → VLAN 22**: HTTP/HTTPS (ingress to K8s apps)
- **VLAN 30/31 → VLAN 10/11**: SSH, RDP, HTTP, HTTPS (staging to management)
- **VLAN 40 → VLAN 10**: SSH, HTTP, HTTPS, Proxmox (dev to management)
- **VLAN 40 → VLAN 41**: SSH, HTTP, HTTPS (dev to dev VMs)
- **VLAN 50/51 → VLAN 10/11**: Limited management access

### Services Allowed to All VLANs
- DNS (to gateway)
- NTP (to gateway)
- DHCP (to gateway)
- ICMP (ping)

## Physical Connections

### MikroTik CRS317 Port Assignments
- **ether1**: Uplink to D-Link router (192.168.0.2/24)
- **sfp-sfpplus1**: KVM server (10G, PVID 10, tagged all VLANs)
- **sfp-sfpplus2**: PC workstation pc1008 (PVID 40, tagged all VLANs)
- **sfp-sfpplus14-16**: Management ports (1G, PVID 10)
- **sfp-sfpplus3-13**: Available

## VPN Access

### WireGuard VPN
- **Interface**: back-to-home-vpn
- **Port**: 55515
- **Users**: 5 (thopi, glinet, LAPTOP-MUJJBT1D, Pixel4, gh_action_01)
- **Access**: Full LAN access for all users

## Infrastructure as Code

### MikroTik Core Switch Management

The MikroTik CRS317 core switch is managed using **Terraform** with configuration stored in version control:

- **Repository**: [labrats-work/bor.infra.network](https://github.com/labrats-work/bor.infra.network)
- **Method**: Declarative Infrastructure as Code (IaC)
- **Provider**: Terraform MikroTik provider
- **Benefits**:
  - Version-controlled network configuration
  - Automated deployment and updates
  - Configuration drift detection
  - Reproducible infrastructure
  - Full audit trail via Git history
  - Disaster recovery capability

### Configuration Management

All MikroTik configuration is managed through Terraform resources including:
- VLANs and network interfaces
- Firewall rules (input, forward, NAT)
- DHCP servers and pools
- DNS configuration
- WireGuard VPN
- Routing rules
- Address lists

Manual changes to the router are discouraged as they will be overwritten on next Terraform apply.

## Security Model

### Defense-in-Depth Strategy
1. **Edge Security**: NAT at D-Link router
2. **Network Segmentation**: 12 isolated VLANs
3. **Zone Isolation**: Management, Production, Staging, Dev, Sandbox
4. **DMZ**: Separate ingress zone (VLAN 29)
5. **Firewall**: Default deny with explicit allow rules
6. **VPN**: Secure remote access via WireGuard

### Zero Trust Principles
- All inter-VLAN traffic blocked by default
- Explicit allow rules for required services only
- Production isolated from non-production
- DMZ restricted to HTTP/HTTPS only
- Management access restricted to trusted networks

---
*Last Updated: 2025-11-01*
*Network documentation generated from homelab configuration*

**Note**: The MikroTik CRS317 core switch configuration is managed via Terraform in the [bor.infra.network](https://github.com/labrats-work/bor.infra.network) repository. This ensures all network configuration is version-controlled and reproducible.
