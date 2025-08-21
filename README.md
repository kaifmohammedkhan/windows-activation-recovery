# 🛠️ Windows Activation Recovery: A DevOps Case Study

## 📌 Summary
After a motherboard swap, my Windows 10 system failed to activate due to missing system files, broken services, and corrupted registry keys. This case study documents how I diagnosed and repaired the activation system using kernel-level registry recovery and strategic troubleshooting — without reinstalling Windows or losing data.

---

## ⚠️ Problem Statement

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

### 1. Prepare Recovery Script
- Downloaded [`rearm.cmd`](https://github.com/asdcorp/rearm) from GitHub
- Placed script at `C:\rearm.cmd`

### 2. Boot into Windows Recovery
- Selected: Troubleshoot → Advanced Options → Command Prompt

### 3. 3. Execute Registry Repair
  
   C:\rearm.cmd

- If not recognized:
   
   bcdedit | find "osdevice"
E:\rearm.cmd  # Replace with actual OS volume

### 4. Reboot and Verify

sppsvc restored

Windows activated with digital license linked to Microsoft account

✅ Outcome:
Windows 10 Pro activated without reinstall

sppsvc service fully functional

Registry corruption resolved

🧠 Lessons Learned:
Kernel-protected registry keys require recovery environment access

bcdedit is a powerful tool for dynamic volume detection

GitHub scripts like rearm.cmd can be life-saving

📸 Screenshots:
See /screenshots for activation success and recovery command prompt.

Strategic troubleshooting beats brute-force reinstallations

System stability restored```bash
##shutdown /f /r /o /t 0
