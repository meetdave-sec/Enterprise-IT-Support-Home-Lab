# Name Resolution Issue - Troubleshooting Case Study

## Scenario

A user reported inability to access internal resources using hostnames.

Examples:

```text
\\DC01\Finance
```

and

```text
ping dc01
```

were failing.

---

## Initial Investigation

Verified workstation configuration.

Command:

```powershell
ipconfig /all
```

Finding:

```text
DNS Server: 8.8.8.8
```

---

## Root Cause

The workstation was configured to use Google Public DNS.

Google DNS could not resolve:

```text
corp.local
dc01.corp.local
```

because those records only exist inside the organization's Active Directory DNS zone.

---

## Resolution

Updated DNS configuration.

Changed:

```text
8.8.8.8
```

to:

```text
192.168.100.10
```

Executed:

```powershell
ipconfig /flushdns
```

---

## Verification

Executed:

```powershell
nslookup dc01
```

Result:

```text
dc01.corp.local
192.168.100.10
```

Executed:

```powershell
ping dc01
```

Result:

Successful.

---

## Lessons Learned

Always verify:

1. Network connectivity
2. Default gateway
3. DNS server configuration
4. Name resolution

before escalating issues.

Many Active Directory issues originate from incorrect DNS settings.
