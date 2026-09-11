# Week 1 Verification Evidence

## Software

- VirtualBox: `7.2.4r170995`
- Kali Linux: `2025.4`

## NAT Network

- Name: `Kali-NAT`
- Network: `10.0.0.0/24`
- Gateway: `10.0.0.1`
- DHCP: Enabled
- Kali interface: `eth0`
- Kali address: `10.0.0.3/24`

## Connectivity Results

| Verification | Result |
|---|---|
| Gateway `10.0.0.1` | PASS — 0% packet loss |
| Internet `8.8.8.8` | PASS — 0% packet loss |
| DNS `google.com` | PASS — 0% packet loss |

## Shared Folder

The host Downloads folder was shared as `downloads` and mounted at `/downloads`. The directory contents were verified from Kali.

## Guest Integration

- `vboxguest` loaded: Yes
- `vboxsf` loaded: Yes
- `john` belongs to `vboxsf`: Yes
- Bidirectional clipboard: Confirmed working
- Drag-and-drop: Configured

## Snapshot

A clean Week 1 baseline snapshot was captured as part of the lab evidence.

## Evidence Files

The local screenshot set should be uploaded under `screenshots/` with descriptive names such as:

```text
01-virtualbox-kali.png
02-kali-nat-network.png
03-kali-network.png
04-connectivity-test.png
05-shared-downloads.png
06-snapshot.png
```
