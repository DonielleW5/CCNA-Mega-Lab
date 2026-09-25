# Part 1 — Initial Setup

## Objective

Prepare the routers and switches for the rest of the lab with consistent device identity, local authentication, console settings, and saved configurations.

## Work Completed

- Configured the appropriate hostname on each router and switch.
- Configured an enable secret.
- Created a local user account using a secret.
- Configured console access to authenticate against the local user database.
- Configured a 30-minute console inactivity timeout.
- Enabled synchronous logging.
- Saved each completed configuration.

## Cisco IOS Concepts Practiced

```text
enable
configure terminal
hostname <DEVICE-NAME>
copy running-config startup-config
```

## Verification Evidence

![Console security and session settings](../screenshots/part1-console-security-settings.png)

This screenshot verifies `login local`, `logging synchronous`, and the 30-minute console inactivity timeout without exposing lab passwords or secrets.

## Why This Matters

A consistent base configuration makes later troubleshooting easier. Device naming improves identification, local authentication controls access, console settings improve usability, and saving the running configuration ensures changes survive a reload.

## Status

**Complete**
