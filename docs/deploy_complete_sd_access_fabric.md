# Step 5 (Stretch) - Deploy a Complete SD-Access Fabric

## Overview

In this advanced stretch goal, you'll deploy a complete Software Defined Access (SDA) fabric using the Network as Code framework. This represents a production-ready deployment scenario.

!!! warning "Stretch Goal"
    This is an advanced exercise. Complete Steps 1-4 before attempting this challenge.

## What You'll Deploy

A complete SDA fabric including:

- **Sites and Buildings** - Logical hierarchy
- **Network Settings** - DHCP, DNS, NTP
- **IP Pools** - For fabric endpoints  
- **Fabric Domains** - SD-Access fabric definition
- **Virtual Networks** - VNs for traffic segmentation
- **Transit Networks** - Inter-fabric connectivity
- **Authentication Templates** - 802.1X configuration
- **Access Policies** - Scalable groups and contracts

## Architecture Overview

```
┌─────────────────────────────────────────────────┐
│             Global Site Hierarchy                │
├─────────────────────────────────────────────────┤
│  Region: Americas                                │
│    └─ Building: HQ-Building                      │
│         └─ Floor: Floor-1                        │
└─────────────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────┐
│           Network Infrastructure                 │
├─────────────────────────────────────────────────┤
│  Control Plane Nodes: 2                          │
│  Border Nodes: 2                                 │
│  Edge Nodes: 3                                   │
└─────────────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────┐
│              Fabric Services                     │
├─────────────────────────────────────────────────┤
│  Virtual Networks:                               │
│    - EMPLOYEE_VN                                 │
│    - GUEST_VN                                    │
│    - IOT_VN                                      │
└─────────────────────────────────────────────────┘
```

## Prerequisites

- Completed Steps 1-4
- Access to all lab devices
- Clean Catalyst Center (or ability to create new site)
- Approximately 45-60 minutes

## Configuration Files Structure

```
DEVWKS-1709/
└── nac-complete-fabric/
    ├── sites.yaml           # Site hierarchy
    ├── network.yaml         # Network settings
    ├── ip-pools.yaml        # IP address pools
    ├── fabric.yaml          # Fabric configuration
    ├── virtual-networks.yaml # VN definitions
    └── policies.yaml        # Access policies
```

## Step-by-Step Deployment

### 1. Review the Configuration

Navigate to the complete fabric directory:

```bash
cd DEVWKS-1709/nac-complete-fabric
```

Examine each YAML file to understand the configuration.

### 2. Customize for Your Environment

Update `sites.yaml` with your site details:

```yaml
sites:
  - name: "HQ-Building"
    parent: "Global/Americas"
    type: building
    address: "123 Network Street, San Jose, CA"
    latitude: 37.3382
    longitude: -121.8863
```

### 3. Configure Network Settings

Update `network.yaml`:

```yaml
network_settings:
  - site: "Global/Americas/HQ-Building"
    dhcp_servers:
      - "10.10.10.10"
    dns_servers:
      - "8.8.8.8"
      - "8.8.4.4"
    ntp_servers:
      - "time.cisco.com"
    timezone: "America/Los_Angeles"
```

### 4. Define IP Pools

Configure `ip-pools.yaml`:

```yaml
ip_pools:
  - name: "EMPLOYEE_POOL"
    type: "Generic"
    ip_subnet: "10.20.0.0/16"
    gateway: "10.20.0.1"
    dhcp_server: "10.10.10.10"
    dns_servers:
      - "8.8.8.8"
  
  - name: "GUEST_POOL"
    type: "Generic"
    ip_subnet: "10.30.0.0/16"
    gateway: "10.30.0.1"
```

### 5. Configure Fabric Domain

Update `fabric.yaml`:

```yaml
fabric_sites:
  - site_name: "Global/Americas/HQ-Building"
    authentication_profile: "Closed Authentication"
    pub_sub_enabled: true
    control_plane_nodes:
      - device_name: "Control-Plane-1"
        role: "CONTROL_PLANE"
    border_nodes:
      - device_name: "Border-1"
        role: "BORDER_NODE"
        external_connectivity: true
      - device_name: "Border-2"
        role: "BORDER_NODE"
        external_connectivity: true
    edge_nodes:
      - device_name: "Edge-1"
        role: "EDGE_NODE"
      - device_name: "Edge-2"
        role: "EDGE_NODE"
      - device_name: "Edge-3"
        role: "EDGE_NODE"
```

### 6. Define Virtual Networks

Configure `virtual-networks.yaml`:

```yaml
virtual_networks:
  - name: "EMPLOYEE_VN"
    vn_segment_id: 4096
    traffic_type: "DATA"
    ip_pools:
      - "EMPLOYEE_POOL"
  
  - name: "GUEST_VN"
    vn_segment_id: 4097
    traffic_type: "DATA"
    ip_pools:
      - "GUEST_POOL"
  
  - name: "IOT_VN"
    vn_segment_id: 4098
    traffic_type: "DATA"
```

### 7. Validate the Configuration

Run comprehensive validation:

```bash
nac validate --config-dir . --verbose
```

Review any warnings or errors and fix them.

### 8. Pre-deployment Checks

Verify prerequisites:

```bash
# Check device connectivity
nac check-devices

# Verify licenses
nac check-licenses

# Test API connectivity
nac test-connection
```

### 9. Deploy the Fabric

Execute the deployment:

```bash
nac deploy --config-dir . --confirm
```

The deployment will proceed in phases:
1. Site hierarchy
2. Network settings
3. IP pools
4. Fabric domain
5. Virtual networks
6. Policies

### 10. Monitor Deployment Progress

Watch the deployment in real-time:

```bash
nac status --watch
```

Expected deployment time: 15-20 minutes

### 11. Verify the Deployment

Check fabric status:

```bash
# Overall fabric health
nac fabric-status

# Verify control plane
nac show control-plane

# Check border nodes
nac show border-nodes

# List virtual networks
nac show virtual-networks
```

### 12. Validate in Catalyst Center UI

Log into Catalyst Center and verify:

1. **Provision > Sites** - Site hierarchy created
2. **Design > Network Settings** - Settings applied
3. **Design > IP Address Pools** - Pools configured
4. **Provision > Fabric** - Fabric is operational
5. **Policy > Virtual Networks** - VNs are active

## Post-Deployment Testing

### Test 1: Fabric Connectivity

Verify devices can communicate within VNs:

```bash
# From Edge-1 connected endpoint
ping <endpoint-on-edge-2-same-VN>
```

### Test 2: Virtual Network Segmentation

Verify isolation between VNs:

```bash
# Should FAIL - different VNs
ping <endpoint-in-different-VN>
```

### Test 3: Border Node Connectivity

Test external connectivity through border:

```bash
ping 8.8.8.8
```

## Troubleshooting

### Issue: Fabric Provisioning Fails

**Symptoms**: Deployment hangs at fabric creation
**Resolution**:
```bash
# Check device readiness
nac check-devices --verbose

# Verify device roles
nac show device-roles

# Review logs
nac logs --level debug
```

### Issue: Virtual Network Not Working

**Symptoms**: Endpoints can't communicate
**Resolution**:
1. Check VN to pool mapping
2. Verify DHCP server reachability  
3. Confirm edge node fabric membership
4. Review control plane reachability

### Issue: Border Node External Connectivity

**Symptoms**: Can't reach external resources
**Resolution**:
1. Verify border handoff configuration
2. Check external routing
3. Confirm NAT settings if applicable

## Cleanup

To remove the complete fabric:

```bash
# Remove in reverse order
nac destroy --config-dir . --confirm

# Or remove specific components
nac destroy --component policies
nac destroy --component virtual-networks
nac destroy --component fabric
```

## Key Learnings

After completing this stretch goal, you've learned:

✅ Complete SDA fabric architecture
✅ Multi-component deployment orchestration  
✅ Configuration dependencies and ordering
✅ Validation and verification techniques
✅ Troubleshooting fabric issues
✅ Production-ready deployment practices

## Congratulations!

You've successfully deployed a complete Software Defined Access fabric using Network as Code! This represents a real-world, production-ready deployment scenario.

## Next Steps

- Explore additional fabric features (multicast, QoS)
- Implement advanced policies and contracts
- Set up fabric monitoring and analytics
- Practice Day-2 operations (moves, adds, changes)
- Export your configuration to version control

## Additional Resources

- [Cisco SD-Access Design Guide](https://cisco.com/go/sda-design)
- [Catalyst Center API Documentation](https://developer.cisco.com/catalyst-center)
- [Network as Code GitHub Repository](https://github.com/cisco-network-as-code)
