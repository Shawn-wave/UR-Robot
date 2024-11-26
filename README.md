# Universal Robots Control with RTDE

## Supported Platforms
- Windows
- Ubuntu

## Prerequisites
- UR Robot
- External Control URCaps
- Direct Ethernet Connection between Host and Robot


## Installation
```bash
pip3 install ur_rtde
```

### Configuring IP Settings

#### 1. Robot IP Configuration
Navigate to **Setup >  Network** on the teach pendant
- IP address: `192.168.1.X`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.1.1`
- Preferred DNS server: `192.168.1.1`
- Alternative DNS server: `0.0.0.0`

#### 2. PC (Host) IP Configuration
Set IPv4 configuration to Manual:
- Address: `192.168.1.Y`
- Netmask: `255.255.255.0`
- Gateway: `192.168.1.1`

> **Important Notes:**
> - Replace `X` with a unique number for the robot (e.g., `192.168.1.100`)
> - Replace `Y` with a different unique number for the PC (e.g., `192.168.1.101`)
> - Ensure Robot and PC IPs are in the same subnet but different numbers


## Robot Setup Steps

### 1. Robot IP Setting
- Navigate to **Install > URCaps > External Control**
- Configure Host IP and Port in URCaps settings
> Installation of the URCaps is done by the ROS2 branch

### 2. URCaps Program Setting
- Navigate to Program > URCaps > External Control
- Confirm "Control by Host IP" appears under the Robot Program

### 3. Control Mode Switch
- Switch from Local Control to Remote Control
>  Located in top-right corner of the interface

### 4. Code Execution
- Execute the **RTDE.py**

## Additional Resources
- For more detailed documentation, refer to the [UR-RTDE Documentation](https://sdurobotics.gitlab.io/ur_rtde/)

## Authored By
UR Study in **MARS** (Koreatech)
- Lee SeungHo (Team Lead)
- KI IROO
- Park SeeWoo
- Kim SeongMin
- Lee MinSeok
