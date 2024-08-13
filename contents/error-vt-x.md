# แก้ปัญหา VT-x is not available

People who are struggling with the following error:

```bash
Command: ["startvm", "d3da0d72-3297-4e35-b301-23c8cfb4db96", "--type", "headless "]

Stderr: VBoxManage.exe: error: VT-x is not available (VERR_VMX_NO_VMX) VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
```

Please try these steps and let me know if nothing works:

- Enable virtualization in the BIOS.
- Make sure you have Hyper-V turned off in Windows 10 For Windows 10: Press Windows key. Type "Turn Windows features on or off" Deselect checkbox next to Hyper-V. Select OK. Select Restart now.
