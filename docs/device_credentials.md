# Device Credentials

## Lab Access Information

### Cisco Catalyst Center

| Parameter | Value |
|-----------|-------|
| **URL** | [TBD] |
| **Username** | [TBD] |
| **Password** | [TBD] |
| **API Token** | [TBD] |

### Network Devices

#### Spine Switches

**Spine-1**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]
- **Enable Password**: [TBD]

**Spine-2**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]
- **Enable Password**: [TBD]

#### Border Nodes

**Border-1**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]
- **Enable Password**: [TBD]

**Border-2**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]
- **Enable Password**: [TBD]

#### Edge Nodes

**Edge-1**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]

**Edge-2**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]

**Edge-3**
- **IP Address**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]

### Additional Services

#### Git Repository

- **URL**: `https://github.com/fsalvemi/DEVWKS-1709`
- **Authentication**: GitHub token or SSH key

#### Development Environment

- **SSH Access**: [TBD]
- **Username**: [TBD]
- **Password**: [TBD]

## Important Notes

!!! warning "Security"
    These credentials are for lab use only. Do not use them in production environments.

!!! info "Credential Rotation"
    Lab credentials may be reset periodically. Check this page for updates.

## Connection Methods

### SSH Access
```bash
ssh <username>@<device-ip>
```

### HTTPS/API Access
```bash
curl -k -u <username>:<password> https://<catalyst-center-ip>/api/v1/...
```

### Python Script Example
```python
from dnacentersdk import DNACenterAPI

api = DNACenterAPI(
    username="<username>",
    password="<password>",
    base_url="https://<catalyst-center-ip>",
    verify=False
)
```
