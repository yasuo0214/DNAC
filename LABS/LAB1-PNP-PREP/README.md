# PnP Preparation [![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/kebaldwi/DNAC-TEMPLATES)
## Overview
This Lab is designed to be a standalone lab ot be used either in the DCLOUD environment or as part of the setup for a Proof ov Concept at a customers lab. This information may also help from a deployment or implementation point of view to ensure that all the necessary steps are complete prior to onboarding any devices within DNA Center.

## General Information
As you may recall in the informational sections of this repository we set for the various methods of discovery for a device and the preliminary things required for true zero touch provisioning. Those concepts will be set up in this lab so as to ensure a successful connection to DNA Center.

## Lab Section 1 - Device Connectivity
For PnP processes to work our intention is to have a management interface on the device in this lab we will set up a Loopback interface for management and a Vlan interface for connectivity. Obviously, you don't have to do it this way we are just giving a relatively complicated example and you can alter this to suite your needs. As the device is connected to the front facing ports by default there is little configuration. 

By default the target switch is using vlan 1 as no other vlan exists, and vlan 1 by default accepts DHCP addresses. This will be used in the pnp process. Our management vlan however, may be a different vlan, and so may the native vlan structure of our environment. To that end we must make use of the *pnp startup-vlan* command which allows the device to use this vlan in pnp and needs to be configured on the upstream switch.

### Step 1
Connect to the upstream switch and configure the following:
```
config t
pnp startup-vlan 100
```

This command will program the target switches port connected with a trunk and automatically add the vlan and SVI to the target switch making that vlan ready to accept a DHCP address. This is available on switches running 16.6 code or greater as upstream neighbors. Older switches or upstream devices that are not capable of running the command should be onboarded in vlan 1 and the vlan modified as part of the onboarding process.