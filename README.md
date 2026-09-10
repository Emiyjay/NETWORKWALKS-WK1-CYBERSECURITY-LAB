# Network Walks — Week 1 Cybersecurity Lab Setup

**Participant:** John Emmanuel Sani  
**Repository:** `NETWORKWALKS-WK1-CYBERSECURITY-LAB`  
**Status:** In progress

## 1. Project Overview

This repository documents my Week 1 cybersecurity lab setup for the Network Walks project. The goal is to build and verify a small local cybersecurity practice environment using VirtualBox and Kali Linux, while documenting the configuration, troubleshooting process, and evidence from my own system.

This is an original lab record. Hardware specifications, network addresses, screenshots, errors, and solutions will be recorded from my actual environment rather than copied from reference projects.

## 2. Objectives

- Prepare the host computer for cybersecurity laboratory work.
- Install and configure Oracle VirtualBox.
- Install and boot Kali Linux as a virtual machine.
- Create and configure a dedicated NAT Network.
- Verify communication between Kali Linux and the virtual network gateway.
- Verify Internet connectivity from Kali Linux.
- Configure useful host/guest integration features.
- Configure the required shared-folder arrangement.
- Create a clean VM snapshot after successful setup.
- Document problems encountered and how they were solved.

## 3. Lab Environment

### Host Machine

| Item | Actual value |
|---|---|
| Operating system | To be verified from host |
| Processor | To be verified from host |
| RAM | To be verified from host |
| Storage | To be verified from host |
| VirtualBox version | To be verified |

### Kali Linux VM

| Item | Actual value |
|---|---|
| Guest OS | Kali Linux |
| VM RAM | To be verified |
| VM storage | To be verified |
| Network adapter | Adapter 1 |
| Network mode | NAT Network |
| NAT Network name | `Kali-NAT` |

## 4. Network Configuration

The lab NAT Network was created as follows:

```text
Network name: Kali-NAT
IPv4 network: 10.0.0.0/24
Gateway:      10.0.0.1
DHCP:         Enabled
IPv6:         Disabled
```

The Kali Linux IPv4 address will be recorded only after it has been verified from the running VM.

> **Important:** The final Kali IP address must come from the actual lab. It will not be copied from a sample repository.

## 5. Setup Progress

- [x] GitHub repository created
- [x] Kali Linux installed and booted
- [x] NAT Network `Kali-NAT` created
- [x] NAT Network configured with `10.0.0.0/24`
- [x] DHCP enabled on `Kali-NAT`
- [ ] Verify Kali IPv4 address
- [ ] Verify default gateway
- [ ] Verify gateway connectivity
- [ ] Verify Internet connectivity by IP
- [ ] Verify DNS resolution
- [ ] Configure clipboard integration
- [ ] Configure drag and drop if required
- [ ] Configure shared `/downloads` folder
- [ ] Create final VM snapshot
- [ ] Capture final evidence screenshots
- [ ] Publish final project documentation
- [ ] Prepare LinkedIn project post

## 6. Verification Commands

The following commands will be used inside Kali Linux to record the real network state:

```bash
ip -br addr
ip route
ping -c 4 10.0.0.1
ping -c 4 8.8.8.8
ping -c 4 google.com
```

The command output will be added to the evidence documentation after the host computer is available again.

## 7. Problem Encountered During Setup

During the network configuration stage, the VM was changed to use the NAT Network, but the expected network information was not immediately appearing as expected. The issue is still being investigated from the actual machine.

The troubleshooting process will be documented rather than presenting an assumed successful configuration.

### Troubleshooting approach

1. Confirm that the VM is powered off before changing VirtualBox network settings.
2. Confirm Adapter 1 is enabled.
3. Confirm the attachment type is **NAT Network**, not ordinary **NAT**.
4. Confirm the selected network is exactly `Kali-NAT`.
5. Confirm the virtual network uses `10.0.0.0/24`.
6. Confirm DHCP is enabled.
7. Boot Kali and inspect the interface with `ip -br addr`.
8. Inspect routing with `ip route`.
9. Test the gateway, Internet address, and DNS separately.

## 8. Evidence

Screenshots will be added as the lab is completed.

Planned evidence includes:

- Host computer specifications
- VirtualBox installation/version
- Kali Linux VM running
- Kali VM network adapter settings
- `Kali-NAT` configuration
- Kali IPv4 address
- Routing table
- Successful gateway ping
- Successful Internet connectivity test
- DNS resolution
- Shared-folder configuration
- Final VM snapshot

## 9. Lessons Learned

The first week is focused not only on getting the tools installed, but also on learning how to verify a cybersecurity lab instead of assuming that a configuration is correct. Each network setting will therefore be checked from both the VirtualBox side and the Kali Linux side.

A failed or unexpected configuration is also useful evidence when the troubleshooting process is recorded accurately.

## 10. Security Notes

- No passwords, tokens, API keys, or private credentials will be committed to this repository.
- VM disk images will not be uploaded.
- Screenshots will be checked for sensitive information before publication.
- Network addresses will represent the actual lab configuration and will not be fabricated.

## 11. Project Status

**Current stage:** Lab documentation and network verification pending host-machine access.

The next technical task is to verify the Kali interface, gateway, routing table, and Internet/DNS connectivity from the running VM.
