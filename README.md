# Network Walks — Week 1 Cybersecurity Lab Setup

**Participant:** John Emmanuel Sani  
**Repository:** `NETWORKWALKS-WK1-CYBERSECURITY-LAB`  
**Status:** Lab setup and verification completed

## 1. Project Overview

This repository documents my Week 1 cybersecurity laboratory setup for Network Walks. The lab uses Oracle VirtualBox and Kali Linux to establish a controlled environment for cybersecurity learning, network testing, and future practical exercises.

The configuration and troubleshooting notes below are based on the actual lab environment and verified command output.

## 2. Objectives

- Configure Oracle VirtualBox for cybersecurity laboratory work.
- Install and boot Kali Linux as a virtual machine.
- Create a dedicated NAT Network named `Kali-NAT`.
- Configure the network as `10.0.0.0/24` with gateway `10.0.0.1` and DHCP enabled.
- Verify Kali's assigned address, routing, gateway access, Internet access, and DNS resolution.
- Configure host/guest integration and a shared Downloads folder.
- Capture evidence and create a clean VM baseline snapshot.
- Document troubleshooting and lessons learned.

## 3. Lab Environment

### Host Machine

| Item | Verified value |
|---|---|
| Operating system | Windows 10 |
| RAM | 8 GB |
| Storage | 500 GB |
| VirtualBox version | 7.2.4r170995 |

### Kali Linux VM

| Item | Verified value |
|---|---|
| Guest OS | Kali GNU/Linux Rolling 2025.4 |
| Network adapter | Adapter 1 / `eth0` |
| Network mode | NAT Network |
| NAT Network name | `Kali-NAT` |

## 4. Network Configuration

```text
Network name: Kali-NAT
IPv4 network: 10.0.0.0/24
Gateway:      10.0.0.1
DHCP:         Enabled
IPv6:         Disabled
Kali IP:     10.0.0.3/24
Interface:   eth0
```

The assignment reference used `10.0.0.2` as a target address, but DHCP assigned `10.0.0.3` in this actual environment. The documented address therefore reflects the real lab rather than an assumed value.

## 5. Verification

The final verified route was:

```text
default via 10.0.0.1 dev eth0
10.0.0.0/24 dev eth0
```

Connectivity tests completed successfully:

| Test | Result |
|---|---|
| Kali → `10.0.0.1` | PASS — 0% packet loss |
| Kali → `8.8.8.8` | PASS — 0% packet loss |
| Kali → `google.com` | PASS — DNS resolution and 0% packet loss |

## 6. Host/Guest Integration

- Guest Additions kernel modules `vboxguest` and `vboxsf` were verified as loaded.
- User `john` is a member of the `vboxsf` group.
- Windows Downloads was shared through VirtualBox as `downloads`.
- The shared folder was mounted and verified at `/downloads`.
- Bidirectional clipboard was configured and subsequently confirmed working.
- Drag-and-drop was configured in VirtualBox.

## 7. Troubleshooting

### NAT Network initially appeared unavailable from Kali

The VirtualBox NAT Network itself was correctly configured, but Kali's active connection was initially using `eth1` with an ordinary NAT address (`10.0.3.15/24`). Consequently, traffic was not using `Kali-NAT`.

The VM's adapter MAC addresses were compared with Kali's interfaces to identify the correct interface. Adapter 1 mapped to `eth0`, which was then activated with:

```bash
sudo nmcli device connect eth0
```

Kali subsequently received `10.0.0.3/24` and a default route through `10.0.0.1`. Gateway, Internet, and DNS tests then passed.

### Sudo hostname warning

`sudo` initially reported that the hostname could not be resolved because `/etc/hosts` contained only `127.0.0.1 localhost`. The active hostname was added as a local host entry:

```text
127.0.1.1 kali-temp-1786642011
```

The warning was resolved without changing the network configuration.

### Shared folder auto-mount

The VirtualBox shared-folder modules were present, but the automatically expected mount directory was not initially created. The required mount point was created and the share was mounted manually:

```bash
sudo mkdir -p /downloads
sudo mount -t vboxsf downloads /downloads
```

The Windows Downloads contents were then visible from `/downloads`.

## 8. Evidence

The repository contains captured evidence for the completed setup. Planned/added evidence includes:

- VirtualBox and Kali VM
- `Kali-NAT` configuration
- Kali IP and routing
- Successful gateway/Internet/DNS tests
- Shared `/downloads` folder
- Final VM snapshot

## 9. Lessons Learned

- A VirtualBox network can be configured correctly while the guest is still using a different adapter.
- `ip -br addr` and `ip route` are essential for identifying the interface actually carrying traffic.
- Gateway, raw Internet IP, and DNS tests verify different layers of connectivity.
- DHCP-assigned addresses should be documented from the real environment instead of forcing an address from a sample.
- Host/guest integration depends on Guest Additions and correct group membership.
- Troubleshooting evidence is part of a reproducible cybersecurity lab setup.

## 10. Security and Ethical Use

This environment is intended for authorized cybersecurity education and testing. Activities should remain inside systems and networks for which permission has been granted.

No passwords, tokens, API keys, or private credentials are included in this repository. VM disk images are not uploaded.

## 11. Author

**John Emmanuel Sani**  
Cybersecurity Student  
GitHub: [Emiyjay](https://github.com/Emiyjay)
