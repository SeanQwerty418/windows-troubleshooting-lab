# Lab 02 – IPv4 Routing Misconfiguration and Ping Error Analysis

## Overview

This lab compares three common IPv4 configuration failures in Windows:

1. An incorrect default gateway
2. A missing default gateway
3. An incorrect static IPv4 address

The purpose of the lab is to observe how each configuration affects communication with local and remote destinations and how the resulting `ping` messages can help identify the cause of the problem.

---

## Environment

- Windows 11 virtual machine
- Oracle VirtualBox
- VirtualBox NAT networking
- Network adapter: Intel(R) PRO/1000 MT Desktop Adapter
- Local subnet: `10.0.2.0/24`
- Normal client address: `10.0.2.15`
- Correct default gateway: `10.0.2.2`
- Local test destination: `10.0.2.2`
- Remote test destination: `8.8.8.8`
![normal-ip-state](00_normal-ip-state)

---

## Testing Method

Two destinations were tested during each scenario:

```powershell
ping 10.0.2.2
ping 8.8.8.8
