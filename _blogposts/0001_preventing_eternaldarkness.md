---
layout: blogpost
type: article
title: "Save yourself from SMBv3 Exploit (CVE-2020-0796) which is a wormable Windows SMBv3 RCE flaw leaked, but not patched"
description: CVE-2020-0796 is a &quot;wormable&quot; vulnerability in the Microsoft Server Message Block (SMB) protocol that has yet to be fixed. This article will guide to implement a workaround for this critical vulnerability.
tags:
    - "CVE-2020-0796"
    - Vulnerability Patch
    - Windows
    - SMB
    - Vulnerability Disclosure
    - Microsoft
---

On Tuesday, 10th of March 2020, when Microsoft released its regular Patch Tuesday fixes, Cisco Talos and Fortinet "mistakenly" also published information about CVE-2020-0796, a "wormable" vulnerability in Microsoft Server Message Block (SMB) protocol version 3 that has yet to be fixed.

*CVE-2020-0796 is a remote code execution vulnerability in Microsoft Server Message Block 3.0 (SMBv3). An attacker could exploit this bug by sending a specifically crafted packet to the target SMBv3 server, which the victim needs to be connected to. Users are encouraged to disable SMBv3 compression and block TCP port 445 on firewalls and client computers. The exploitation of this vulnerability opens systems up to a "wormable" attack, which means it would be easy to move from victim to victim.*

Cisco Talos has since removed the entry but a few hours later, Microsoft published an [advisory](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/adv200005) containing detailed information and workarounds to be implemented until a fix is made available via Windows Update Service.

To know more about this vulnerability go to [MITRE's website](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-0796).

Now, I am going to guide you step-by-step on how to implement the workaround suggested by Microsoft.

## Workaround Implementation
Luckily, a github user [@T13nn3s](https://github.com/T13nn3s) has created a PowerShell script to automate that workaround.

First of all, we need to enable external script execution on PowerShell. For that, Press &#x229E; WindowsKey+X to open Power User Menu. Select "Windows PowerShell (Admin)" to open PowerShell with elevated privileges.

After PowerShell Windows is focused, type "Set-ExecutionPolicy Bypass" (without quotes) and press <kbd>Enter</kbd>. If prompted, Press "Y" and then Press <kbd>Enter</kbd>. Don't worry, we will revert this setting in the end to keep your default settings.

Now go to [https://github.com/T13nn3s/CVE-2020-0976](https://github.com/T13nn3s/CVE-2020-0976) and press Green Button labeled "Clone or Download" and then select "Download ZIP".

After Download has completed, extract that ZIP file to your desktop.

Now go to already opened PowerShell window and type the following command to switch to Desktop:

```powershell
cd ([Environment]::GetFolderPath("Desktop"))
```

Now, enter in to the extracted folder using following command:

```powershell
cd CVE-2020-0976-master
```

It&quot;time to execute that main script. USe the following command to do so:

```powershell
.\CVE-2020-0796-Smbv3-checker.ps1
```

You will be promted with four options like this:

```
================ Mitigation for CVE-2020-0796 (CoronaBlue) ================
1: Press '1' for check your current SMBv3 Compression setting
2: Press '2' to disable SMBv3 Compression <= This is the mitigation for CVE-2020-0796
3: Press '3' Enable SMBv3 Compression
Q: Press 'Q' to quit.
```

Press '2' and then press <kbd>Enter</kbd>
Press <kbd>Enter</kbd> again and then Press choose option 'Q' to quit that script.

Now you have successfully disabled that vulnerability. It's time to reset that Execution Policy for future.

Type the following command and press <enter> and then press 'y' if prompted.

```powershell
Set-ExecutionPolicy Default
```

## Conclusion
That was all!! You have successfully disabled the "wormable" vulnerability in Microsoft SMBv3. Please keep checking for newer updates on Windows so the vulnerability is fully patched when it's patch becomes available.