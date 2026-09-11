# Week 1 Lab Notes — Cybersecurity & Pentesting Lab Setup

## Environment

- Host: Windows 10, 8 GB RAM, 500 GB storage
- VirtualBox: 7.2.4r170995
- Guest: Kali GNU/Linux Rolling 2025.4

## Network Configuration

VirtualBox NAT Network:

```text
Name:        Kali-NAT
Network:     10.0.0.0/24
Gateway:     10.0.0.1
DHCP:        Enabled
IPv6:        Disabled
```

Kali's working interface was `eth0` with DHCP address `10.0.0.3/24`.

## Verification

Final routing showed:

```text
default via 10.0.0.1 dev eth0
10.0.0.0/24 dev eth0
```

Connectivity verification:

- Gateway `10.0.0.1`: PASS, 0% packet loss
- Internet `8.8.8.8`: PASS, 0% packet loss
- DNS/Internet `google.com`: PASS, 0% packet loss

## Shared Folder

Guest Additions modules `vboxguest` and `vboxsf` were loaded and the user was in the `vboxsf` group. The Windows Downloads folder was shared as `downloads` and mounted at:

```text
/downloads
```

The contents of the Windows Downloads directory were successfully visible from Kali.

## Integration

Bidirectional clipboard was configured and confirmed working. Drag-and-drop was configured in VirtualBox.

## Troubleshooting Record

The first active Kali connection used the ordinary NAT adapter (`eth1`, `10.0.3.15/24`) instead of the required NAT Network adapter. Adapter/MAC mapping identified `eth0` as VirtualBox Adapter 1, which was attached to `Kali-NAT`. Activating `eth0` with `nmcli` restored the required `10.0.0.3/24` address and `10.0.0.1` gateway.

A sudo hostname warning was also resolved by adding the active hostname to `/etc/hosts`:

```text
127.0.1.1 kali-temp-1786642011
```

## Evidence

Screenshots captured for the project cover the VirtualBox/Kali environment, NAT Network configuration, Kali network state, connectivity tests, shared Downloads folder, and VM snapshot.
