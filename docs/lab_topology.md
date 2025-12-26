# Lab Topology

## Network Diagram

[Add your topology diagram here]

## Components

### Cisco Catalyst Center

- **Role**: DNA Center for managing the SDA fabric
- **Management IP**: [TBD]
- **Version**: [TBD]

### Fabric Devices

#### Underlay Devices

**Spine Switches**
- Spine-1: [Details TBD]
- Spine-2: [Details TBD]

**Border Nodes**
- Border-1: [Details TBD]
- Border-2: [Details TBD]

#### Overlay Devices

**Edge Nodes**
- Edge-1: [Details TBD]
- Edge-2: [Details TBD]
- Edge-3: [Details TBD]

### Control Plane Nodes

- Control Plane Node 1: [Details TBD]
- Control Plane Node 2: [Details TBD]

### Additional Components

**External Connectivity**
- Internet Gateway
- External Services

**Hosts/Endpoints**
- Test endpoints in various VLANs

## Network Segments

| Segment | VLAN | Subnet | Purpose |
|---------|------|--------|---------|
| Management | [TBD] | [TBD] | Device management |
| User Data | [TBD] | [TBD] | End user traffic |
| Guest | [TBD] | [TBD] | Guest access |

## Connectivity Requirements

- All devices have management connectivity
- Underlay uses IS-IS or OSPF
- Overlay uses VXLAN EVPN
- External connectivity through border nodes
