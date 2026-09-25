# Troubleshooting & Validation Notes

## Workflow

1. Configure the feature.
2. Run the relevant `show` command.
3. Compare the operational state with the intended design.
4. Correct any mismatch.
5. Verify again.
6. Save the configuration.

## Access vs. Trunk Verification

```text
show interfaces <interface> switchport
```

I used this to confirm administrative/operational mode, access VLAN, voice VLAN, native VLAN, allowed VLANs, and DTP status.

## Voice VLAN Correction

A phone/PC-facing port needs a data VLAN and a separate voice VLAN:

```text
switchport mode access
switchport access vlan 10
switchport voice vlan 20
```

![Phone data and voice VLAN verification](../screenshots/asw-a3-phone-data-voice-vlan.png)

## WLC Trunk Correction

The WLC link needed to carry Wi-Fi and Management traffic, so the connection required a trunk rather than a normal single-VLAN access port.

![WLC trunk verification](../screenshots/asw-a1-wlc-trunk-vlan40-99.png)

## Unused-Port Verification

I used:

```text
show interfaces status
```

before disabling ports so I could distinguish active links from unused interfaces.

- `notconnect` = no current active link
- `disabled` = administratively shut down

![Unused distribution switch ports disabled](../screenshots/dsw-b2-unused-ports-disabled.png)

## Configuration Persistence

After completing each device:

```text
copy running-config startup-config
```

The main lesson is that configuration and verification are separate tasks. A command being accepted does not automatically mean the network is operating as intended.
