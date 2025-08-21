# 🕰️ Troubleshooting Timeline

## Day 1: Initial Diagnosis
- Activation failed with error `0xc004f074`
- `sppsvc` service missing or broken
- DISM and SFC unable to repair system
- `tokens.dat` not found
- Attempted ISO rebuild and file extraction

## Day 2: Deep Dive
- Used `handle.exe` to identify locked files
- Killed `wimserv.exe` processes
- Mounted `install.wim` to extract missing files
- Discovered edition mismatch (Enterprise vs Pro)
- HWID activation failed due to SKU conflict

## Day 3: Breakthrough
- Found corrupted `WPA` registry key
- Used `rearm.cmd` in Windows Recovery
- Executed registry cleanup via command prompt
- Rebooted and confirmed activation success

## Final Outcome
- Windows 10 Pro activated with digital license
- No data loss, no reinstall
- Case study published on GitHub
