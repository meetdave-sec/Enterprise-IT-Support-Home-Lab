# DNS Troubleshooting Guide

## Overview

DNS (Domain Name System) is responsible for translating hostnames into IP addresses.

In an Active Directory environment, DNS is critical for:

* Domain authentication
* Domain Controller discovery
* Group Policy processing
* Shared resource access

---

## Common Symptoms

### Hostname Resolution Failure

Examples:

```text
ping dc01

Ping request could not find host dc01
```

### Domain Join Failure

```text
An Active Directory Domain Controller could not be contacted.
```

### Shared Folder Access Failure

```text
\\DC01\Finance

Network path not found.
```

---

## Diagnostic Commands

### View Network Configuration

```powershell
ipconfig /all
```

Verify:

* IP Address
* Default Gateway
* DNS Server

---

### Test DNS Resolution

```powershell
nslookup dc01
```

Expected:

```text
Name: dc01.corp.local
Address: 192.168.100.10
```

---

### Test Connectivity

```powershell
ping dc01
```

---

### Flush DNS Cache

```powershell
ipconfig /flushdns
```

---

### Register DNS Records

```powershell
ipconfig /registerdns
```

---

## Common Root Causes

### Incorrect DNS Server

Incorrect:

```text
8.8.8.8
1.1.1.1
```

Correct:

```text
192.168.100.10
```

---

### DNS Service Stopped

Check:

```powershell
Get-Service DNS
```

---

### Missing DNS Records

Verify records exist in:

```text
DNS Manager
→ Forward Lookup Zones
→ corp.local
```

---

## Best Practices

* Use Domain Controller DNS for domain-joined devices.
* Avoid public DNS servers on Active Directory clients.
* Verify DNS before troubleshooting authentication issues.
* Document all DNS changes.
