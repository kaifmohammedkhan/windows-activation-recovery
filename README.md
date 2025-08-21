# 🛠️ Windows Activation Recovery: A DevOps Case Study

## 📌 Summary
After a motherboard swap, my Windows 10 system failed to activate due to missing system files, broken services, and corrupted registry keys. This case study documents how I diagnosed and repaired the activation system using kernel-level registry recovery and strategic troubleshooting — without reinstalling Windows or losing data.

---

## ⚠️ Problem Statement

> ⚠️ Initial diagnosis revealed a malware-induced deletion of `sppsvc.exe`, the core Software Protection service. Activation tools failed, and registry corruption was evident. This case study documents the full recovery journey — from malware detection to permanent activation.

- Windows edition mismatch (Enterprise → Pro)
- `sppsvc` (Software Protection Platform) service missing or broken
- Activation errors due to corrupted `WPA` registry keys
- High CPU usage from `sppsvc`
- Digital license not recognized despite valid hardware ID

---

## 🔍 Diagnosis Process

- Inspected `sppsvc` dependencies and registry entries
- Verified missing system files (`tokens.dat`, `sppsvc.dll`)
- Attempted DISM repair and ISO-based file extraction
- Identified corrupted `HKEY_LOCAL_MACHINE\SYSTEM\WPA` key
- Confirmed kernel-level protection preventing deletion

---

## 🧪 Solution Steps

This recovery flow documents how I diagnosed and resolved a deep Windows activation failure after hardware changes, using registry repair and CLI-based activation.

### 🔧 1. Registry Repair via Recovery Environment
- Detected corruption in `HKLM\SYSTEM\WPA` registry hive
- Booted into Windows Recovery Command Prompt
- Executed custom `rearm.cmd` script to reset licensing state
- Rebooted to apply registry changes

🧱 Fixing WPA Registry (Kernel-Protected Key)

To repair the corrupted HKEYLOCALMACHINE\SYSTEM\WPA registry key — which was blocking sppsvc and activation — I followed the Gravesoft method:

1. Downloaded rearm.cmd
2. Placed it in C:\rearm.cmd
3. Rebooted into Windows Recovery using:
   `cmd
   shutdown /f /r /o /t 0
   `
4. Opened Command Prompt via Troubleshoot > Advanced Options
5. Ran:
   `cmd
   C:\rearm.cmd
   `
   (or used bcdedit | find "osdevice" to locate the correct drive letter)

This cleared the kernel-protected WPA key and allowed sppsvc to start successfully.

🔗 Gravesoft Guide: Fix WPA Registry

### 💻 2. Launch Activation CLI via PowerShell
- Opened PowerShell as Administrator
- Ran:
  powershell
  
  irm https://get.activated.win | iex
  
- This launched the Microsoft Activation CLI tool

### 🧩 3. Attempted Activation
- Selected option [1] for Windows activation
- Initial result: Activation failed with error `0xC004F213` (no product key found)

### 🧠 4. Troubleshooting
- Verified restored registry entries and licensing services
- Confirmed `sppsvc` was running
- Re-ran activation via CLI

### ✅ 5. Success
- Activation completed successfully
- Verified with: Windows Activation on settings and on CMD Cli
  ```
- Status: Windows 10 Pro activated with digital license linked to Microsoft account

---

## 📘 Key Learnings
- Recovery from kernel-level licensing failures is possible without reinstalling Windows
- CLI tools like `slmgr` and custom scripts can bypass GUI limitations
- Documenting each step builds credibility and helps others facing similar issues

-----

## 📂 Repo Contents

| File              | Description |
|-------------------|-------------|
| `README.md`       | Full case study and solution steps |
| `activation-error.txt` | Raw error logs from failed activation attempts |
| `recovery-steps.txt`   | Step-by-step manual recovery flow |
| `timeline.md`     | Chronological breakdown of troubleshooting |
| `.gitignore`      | Git tracking exclusions |
| `LICENSE`         | Repository license |

---

## 🧠 Case Study Summary

After a hardware change triggered a Windows activation failure (`0xC004F213`), I diagnosed and repaired kernel-level registry corruption without reinstalling the OS. This repo documents the full recovery flow, including CLI activation, service validation, and registry restoration.

Why it matters: 
- Demonstrates deep troubleshooting under pressure  
- Highlights DevOps mindset: automation, documentation, and resilience  
- Turns adversity into a technical branding asset

