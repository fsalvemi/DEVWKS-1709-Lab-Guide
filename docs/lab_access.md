# Lab Access

## Overview

This lab is hosted in a cloud-based environment that provides you with access to Cisco Catalyst Center and network devices. You will connect to the lab environment using one of the methods described below.

## Access Methods

You have two primary options to access the lab environment:

### Option 1: Web-Based Access (Recommended)

The easiest way to access your lab is through the web-based interface provided in the dCloud portal. This method requires no additional software installation.

1. Navigate to your dCloud session
2. Click on the **Workstation** or **Developer Workstation** to access the environment
3. Use the built-in terminal and tools to complete the lab exercises

**Advantages:**
- No local software installation required
- Works from any device with a web browser
- Pre-configured environment ready to use

### Option 2: VPN + RDP Access

For users who prefer working with native applications on their local machine, you can connect via VPN and use Remote Desktop Protocol (RDP) to access the lab workstation.

!!! info "VPN Connection Details"
    VPN connection details are provided in your dCloud session page under the **Session Details** section. Look for:
    
    - VPN Server Address
    - VPN Username
    - VPN Password
    - VPN Type (typically Cisco AnyConnect)

**Steps to Connect:**

1. **Download and Install VPN Client:**
    - Download Cisco AnyConnect from the dCloud session page or [cisco.com](https://www.cisco.com)
    - Install the client on your local machine
    - Follow the platform-specific installation instructions

2. **Connect to VPN:**
    - Launch Cisco AnyConnect
    - Enter the VPN server address from your dCloud session
    - Authenticate with the provided credentials
    - Wait for the connection to establish

3. **Connect via RDP:**
    - Once VPN is connected, use your RDP client:
        - **Windows:** Built-in Remote Desktop Connection (mstsc.exe)
        - **macOS:** Microsoft Remote Desktop from the App Store
        - **Linux:** Remmina, FreeRDP, or similar
    - Connect to the workstation IP address (see [Topology and Device Credentials](lab_topology.md) page)
    - Enter the workstation credentials when prompted

**Advantages:**
- Use your preferred local tools and applications
- Better performance for resource-intensive operations
- Ability to work offline (once files are downloaded)

## Lab Workstation Details

### Pre-installed Software

Your lab workstation comes with the following tools pre-installed:

- **Python 3.9+** - For running scripts and automation tools
- **Git** - For version control and repository management
- **Visual Studio Code** - Recommended IDE for lab exercises
- **Terraform** - For infrastructure as code deployments
- **Network as Code (NaC) CLI** - Cisco's NaC framework tools
- **Postman** or **curl** - For API testing
- **SSH Client** - For device access

### Working Directory

All lab files and exercises are located in the home directory under:

```
/home/developer/DEVWKS-1709/
```

or on Windows:

```
C:\Users\Developer\DEVWKS-1709\
```

!!! tip "Best Practice"
    Always work within the lab directory structure to ensure all paths and configurations work correctly.

## Accessing Cisco Catalyst Center

Cisco Catalyst Center is the network controller used throughout this lab. You will interact with it via:

1. **Web GUI:** Access via browser at the URL provided in the [Topology](lab_topology.md) page
2. **REST API:** Programmatic access for automation (covered in lab exercises)
3. **NaC Framework:** High-level abstraction for deployment automation

### Login Credentials

See the [Topology and Device Credentials](lab_topology.md) page for:

- Catalyst Center URL
- Admin username and password
- API credentials
- Device access credentials

## Troubleshooting Access Issues

### Cannot Connect to VPN

- Verify VPN credentials are correct
- Check that your local firewall allows VPN connections
- Ensure Cisco AnyConnect is up to date
- Try disconnecting and reconnecting

### Cannot Connect via RDP

- Verify VPN connection is established
- Confirm workstation IP address is correct
- Check RDP port (default 3389) is not blocked
- Verify workstation credentials

### Web Interface Not Loading

- Clear browser cache
- Try a different browser (Chrome or Firefox recommended)
- Check dCloud session is still active
- Restart the session if necessary

### Cannot Access Catalyst Center

- Verify network connectivity to Catalyst Center IP
- Check credentials match those in topology documentation
- Ensure browser accepts self-signed certificates
- Try accessing from the lab workstation directly

## Getting Help

If you encounter issues accessing the lab:

1. Check the dCloud session status page
2. Review the troubleshooting section above
3. Contact your lab proctor or instructor
4. Submit a support ticket through the dCloud portal

## Next Steps

Once you have successfully accessed the lab environment, proceed to:

- **[Lab Overview](lab_overview.md)** - Understand the lab objectives and structure
- **[Topology and Device Credentials](lab_topology.md)** - Review the lab topology
- **[Step 1](simple_example_nac_catalyst_center.md)** - Begin your first lab exercise
