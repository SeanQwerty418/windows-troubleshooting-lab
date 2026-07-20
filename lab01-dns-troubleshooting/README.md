# Lab 01 - DNS Resolution Failure Troubleshooting

## Objective

Simulate a DNS resolution failure by configuring an invalid DNS server and troubleshoot the issue using Windows networking tools.

---

## Environment

- Windows 11
- Oracle VirtualBox
- NAT Network
- PowerShell

---

## Symptoms

- Able to ping an IP address (8.8.8.8)
- Unable to resolve domain names
- nslookup timed out

---

## Diagnostic Steps

1. Verified network adapter status

```
Get-NetAdapter
```
![Get-NetAdapter](screenshot/01_Get-NetAdapter.png)

2. Verified IP configuration

```
ipconfig /all
```
![ipconfig](screenshot/02_ipconfig_all.png)

3. Tested Internet connectivity

```
ping 8.8.8.8
ping google.com
```
![ping-google](screenshot/03_ping-google.png)

4. Verified DNS resolution

```
nslookup google.com
```
![nslookup](screenshot/04_nslookup.png)

5. Changed DNS server

```
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.0.2.1
```
![bad-dns](screenshot/05_bad-dns.png)

6. Verified DNS configuration

```
Get-DnsClientServerAddress
```
![ping-ip-success](screenshot/06_ping-ip-success.png)

7. Cleared DNS cache

```
ipconfig /flushdns
```
![flushed-dns-cache](screenshot/07_flushed-dns-cache.png)

8. Tested DNS resolution again

```
ping microsoft.com
nslookup microsoft.com
```
![ping-domain-failed](screenshot/08_ping-domain-failed.png)
![nslookup-failed](screenshot/09_nslookup-failed.png)

9. Restored DNS

```
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ResetServerAddresses
```
![DNS Restored](screenshot/10_dns-restored.png)

10. Verified successful resolution

```
nslookup microsoft.com
```
![ping-microsoft-success](screenshot/11_ping-microsoft-success.png)

---

## Root Cause

The network adapter was configured with an invalid DNS server address (192.0.2.1), preventing hostname resolution while IP connectivity remained functional.

---

## Resolution

Reset the DNS server configuration to obtain DNS settings automatically via DHCP and flushed the DNS cache.

---

## Skills Demonstrated

- Windows DNS troubleshooting
- PowerShell
- Network diagnostics
- ipconfig
- ping
- nslookup
- DNS cache management
