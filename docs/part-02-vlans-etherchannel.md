# Part 2 — VLANs & Layer 2 EtherChannel

## Objective

Build the Layer 2 foundation for two office networks using VLAN segmentation, trunking, redundant uplinks, EtherChannel, VTP, access ports, voice VLANs, and unused-port shutdowns.

## Layer 2 EtherChannel

### Office A

Configured `Port-channel1` between DSW-A1 and DSW-A2 using **PAgP**.

![Office A PAgP EtherChannel](../screenshots/office-a-pagp-etherchannel-summary.png)

### Office B

Configured `Port-channel1` between DSW-B1 and DSW-B2 using **LACP**.

![Office B LACP EtherChannel](../screenshots/office-b-lacp-etherchannel-summary.png)

The Office B infrastructure trunk state was verified after the Layer 2 configuration:

![Office B trunk verification](../screenshots/office-b-trunk-verification.png)

## Infrastructure Trunks

Common trunk settings:

```text
switchport mode trunk
switchport trunk native vlan 1000
switchport nonegotiate
```

Office A allowed VLANs:

```text
10,20,40,99
```

Office B allowed VLANs:

```text
10,20,30,99
```

## VTP Version 2

Configured one distribution switch in each office as a VTPv2 server and the access switches as VTP clients.

![VTP client verification](../screenshots/office-a-vtp-client-status.png)

## VLAN Database

![VLAN database verification](../screenshots/office-a-vlan-brief.png)

### Office A
- VLAN 10 — PCs
- VLAN 20 — Phones
- VLAN 40 — Wi-Fi
- VLAN 99 — Management

### Office B
- VLAN 10 — PCs
- VLAN 20 — Phones
- VLAN 30 — Servers
- VLAN 99 — Management

## Access Ports

### LWAP-facing port

![LWAP management access port](../screenshots/asw-a1-lwap-access-port-vlan99.png)

### Phone + PC port

```text
switchport mode access
switchport access vlan 10
switchport voice vlan 20
switchport nonegotiate
```

![Phone data and voice VLAN verification](../screenshots/asw-a3-phone-data-voice-vlan.png)

## WLC1 Trunk

```text
switchport mode trunk
switchport trunk allowed vlan 40,99
switchport trunk native vlan 99
switchport nonegotiate
```

![WLC trunk verification](../screenshots/asw-a1-wlc-trunk-vlan40-99.png)

## Unused Port Shutdown

I checked interface status before shutting down unused ports.

```text
show interfaces status
```

Distribution-switch verification:

![DSW-B2 disabled ports](../screenshots/dsw-b2-unused-ports-disabled.png)

Access-switch verification:

![ASW-B3 disabled ports](../screenshots/asw-b3-unused-ports-disabled.png)

## Save and Verify

```text
copy running-config startup-config
```

## Status

**Complete**
