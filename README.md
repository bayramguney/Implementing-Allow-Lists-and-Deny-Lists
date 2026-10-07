# Implementing-Allow-Lists-and-Deny-Lists

# 🛡️ Assisted Lab: Implementing Allow Lists and Deny Lists

> **Windows AppLocker | Application Control | Least Privilege | Security+ (SY0-701)**

## 📌 Overview

This lab demonstrates how to implement **application allow lists and deny lists** using **Windows AppLocker**. As a security analyst, you configure application control policies to prevent unauthorized software from executing by creating rules based on **file paths** and **file hashes**.

Application control is an important security measure that supports the **Principle of Least Privilege**, helping organizations reduce malware infections, unauthorized software execution, and insider threats.

---

# 🎯 Objectives

- Configure Windows AppLocker
- Enable AppLocker rule enforcement
- Create application deny rules
- Block applications using Path rules
- Block applications using File Hash rules
- Apply Group Policy updates
- Test application control policies
- Understand allow lists and deny lists

---

# 🖥️ Lab Environment

| Machine | Operating System | Purpose |
|---------|-----------------|----------|
| **PC10** | Windows Server 2019 | Client workstation |

---

# 🛠️ Tools Used

- Local Security Policy (secpol.msc)
- Windows AppLocker
- Windows PowerShell
- Group Policy
- Registry Editor
- Firefox
- gpupdate
- Application Identity Service (AppIDSvc)

---

# 🔐 Security Concepts

- Application Allow Lists
- Application Deny Lists
- Principle of Least Privilege
- Application Control
- Local Security Policy
- Group Policy
- File Hashing
- Change Management
- Endpoint Security

---

# Lab Exercises

## Exercise 1 – Configure AppLocker Rule Enforcement

The first task is enabling AppLocker on the local system.

### Steps

- Start the **Application Identity (AppIDSvc)** service.
- Open **Local Security Policy**.
- Navigate to:

```
Application Control Policies
    └── AppLocker
```

- Configure rule enforcement for:
  - Executable Rules
  - Windows Installer Rules
  - Script Rules
  - Packaged App Rules

### Result

AppLocker is enabled and ready to enforce application control policies.

---

# Exercise 2 – Create a Path Deny Rule

A deny rule is created to block **Registry Editor (regedit.exe)** using its file path.

### Rule Configuration

| Setting | Value |
|---------|-------|
| Action | Deny |
| User | Everyone |
| Condition | Path |
| Path | `%WINDIR%\regedit.exe` |

### Apply Policy

```powershell
gpupdate /force
```

### Verification

Attempting to launch **Registry Editor** results in:

> **"This app has been blocked by your system administrator."**

---

# Exercise 3 – Create a File Hash Rule

A second deny rule blocks **Mozilla Firefox** using its executable hash.

### Rule Configuration

| Setting | Value |
|---------|-------|
| Action | Deny |
| User | Everyone |
| Condition | File Hash |
| Application | firefox.exe |

### Apply Policy

```powershell
gpupdate /force
```

### Verification

Launching Firefox displays:

> **"This app has been blocked by your system administrator."**

---

# Understanding AppLocker Rule Types

## Path Rule

A **Path Rule** blocks an application based on its file location.

### Advantages

- Easy to create
- Minimal system overhead
- Simple to manage

### Limitation

If the executable is:

- Renamed
- Moved to another folder

the rule no longer applies.

---

## File Hash Rule

A **File Hash Rule** blocks an application based on its cryptographic hash.

### Advantages

- Cannot be bypassed by renaming
- Cannot be bypassed by moving the file
- More secure

### Limitation

- Must be recreated after software updates because the file hash changes.

---

# Comparison

| Feature | Path Rule | File Hash Rule |
|----------|-----------|----------------|
| Uses file location | ✅ | ❌ |
| Uses SHA hash | ❌ | ✅ |
| Survives file rename | ❌ | ✅ |
| Survives moving file | ❌ | ✅ |
| Easier to manage | ✅ | ❌ |
| More secure | ❌ | ✅ |

---

# Commands Used

Start the Application Identity service:

```cmd
net start appidsvc
```

Refresh Group Policy:

```cmd
gpupdate /force
```

---

# Skills Demonstrated

- Windows Endpoint Security
- Windows AppLocker
- Application Whitelisting
- Application Blacklisting
- Group Policy Management
- Local Security Policy Administration
- Windows PowerShell
- Windows Security Hardening
- Security Policy Enforcement
- Endpoint Protection

---

# Key Takeaways

- AppLocker provides centralized application control for Windows systems.
- Deny lists prevent unauthorized or potentially malicious applications from running.
- Path rules are simple but can be bypassed if a file is renamed or moved.
- File Hash rules offer stronger security because they identify applications by their cryptographic hash.
- Application control supports the Principle of Least Privilege by allowing users to run only approved software.
- Group Policy updates are required before new AppLocker rules take effect.

---

# 🏷️ GitHub Topics

```text
applocker
application-control
allow-list
deny-list
securityplus
cybersecurity
windows-security
windows-server
group-policy
powershell
endpoint-security
least-privilege
security-hardening
system-administration
blue-team
soc-analyst
windows
incident-prevention
comptia-security-plus
github-lab
```
