# Step 3 (Optional) - Simple Example Deployment with REST API

## Overview

In this optional step, you'll learn how to interact directly with the Catalyst Center REST API to deploy configurations programmatically.

## Why Use REST API Directly?

Direct API interaction provides:

- **Maximum control** over operations
- **Real-time feedback** on operations
- **Custom workflows** and logic
- **Integration** with existing systems

## Prerequisites

- Python 3.8 or higher
- `requests` library installed
- Catalyst Center API credentials
- Basic understanding of REST APIs

## Step-by-Step Instructions

### 1. Install Required Libraries

```bash
pip install requests
```

### 2. Authenticate with Catalyst Center

Create a Python script `catalyst_api.py`:

```python
import requests
import json
from requests.auth import HTTPBasicAuth

# Disable SSL warnings for lab environment
requests.packages.urllib3.disable_warnings()

class CatalystCenterAPI:
    def __init__(self, base_url, username, password):
        self.base_url = base_url
        self.username = username
        self.password = password
        self.token = None
        self.authenticate()
    
    def authenticate(self):
        """Get authentication token"""
        url = f"{self.base_url}/dna/system/api/v1/auth/token"
        response = requests.post(
            url,
            auth=HTTPBasicAuth(self.username, self.password),
            verify=False
        )
        self.token = response.json()['Token']
        print("Authentication successful!")
    
    def get_headers(self):
        """Return headers with token"""
        return {
            'X-Auth-Token': self.token,
            'Content-Type': 'application/json'
        }
```

### 3. Retrieve Network Devices

Add methods to interact with devices:

```python
    def get_devices(self):
        """Get all network devices"""
        url = f"{self.base_url}/dna/intent/api/v1/network-device"
        response = requests.get(
            url,
            headers=self.get_headers(),
            verify=False
        )
        return response.json()
    
    def get_device_by_id(self, device_id):
        """Get specific device details"""
        url = f"{self.base_url}/dna/intent/api/v1/network-device/{device_id}"
        response = requests.get(
            url,
            headers=self.get_headers(),
            verify=False
        )
        return response.json()
```

### 4. Create a Simple Configuration

```python
    def create_site(self, site_name, site_type="area"):
        """Create a new site"""
        url = f"{self.base_url}/dna/intent/api/v1/site"
        payload = {
            "type": site_type,
            "site": {
                "area": {
                    "name": site_name,
                    "parentName": "Global"
                }
            }
        }
        response = requests.post(
            url,
            headers=self.get_headers(),
            json=payload,
            verify=False
        )
        return response.json()
```

### 5. Run the Script

Create `main.py`:

```python
from catalyst_api import CatalystCenterAPI

# Initialize API client
api = CatalystCenterAPI(
    base_url="https://<your-catalyst-center-ip>",
    username="<username>",
    password="<password>"
)

# Get all devices
devices = api.get_devices()
print(f"Found {len(devices['response'])} devices")

# Create a site
result = api.create_site("Lab-Site-01")
print(f"Site creation result: {result}")
```

Run the script:

```bash
python main.py
```

### 6. Verify the Results

Check Catalyst Center UI to verify:
- Site has been created
- Configuration is applied correctly

## API Documentation

Key Catalyst Center API endpoints:

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/dna/system/api/v1/auth/token` | POST | Authentication |
| `/dna/intent/api/v1/network-device` | GET | List devices |
| `/dna/intent/api/v1/site` | GET/POST | Manage sites |
| `/dna/intent/api/v1/template-programmer/template` | GET/POST | Manage templates |

## Error Handling

Add robust error handling:

```python
try:
    devices = api.get_devices()
except requests.exceptions.RequestException as e:
    print(f"API Error: {e}")
except KeyError as e:
    print(f"Response parsing error: {e}")
```

## Best Practices

1. **Always use authentication tokens** - Don't hardcode credentials
2. **Handle rate limiting** - Implement backoff strategies
3. **Validate responses** - Check status codes and response data
4. **Use HTTPS** - Even in lab environments (with proper cert handling)
5. **Log operations** - Track API calls for debugging

## Next Steps

Continue to [Step 4 - Review Approach Comparison](review_approach_comparison.md) to compare all three deployment methods.
