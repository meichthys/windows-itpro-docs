---
title: Remediate and resolve infections detected by Microsoft Defender Antivirus
description: Configure what Microsoft Defender Antivirus should do when it detects a threat, and how long quarantined files should be retained in the quarantine folder
keywords: remediation, fix, remove, threats, quarantine, scan, restore
search.product: eADQiWindows 10XVcnh
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: denisebmsft
ms.author: deniseb
ms.custom: nextgen
ms.date: 09/03/2018
ms.reviewer: 
manager: dansimp
---

# Configure remediation for Microsoft Defender Antivirus scans

**Applies to:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://go.microsoft.com/fwlink/p/?linkid=2069559)

When Microsoft Defender Antivirus runs a scan, it will attempt to remediate or remove threats that it finds. You can configure how Microsoft Defender Antivirus should react to certain threats, whether it should create a restore point before remediating, and when it should remove remediated threats.

This topic describes how to configure these settings with Group Policy, but you can also use [Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/configmgr/protect/deploy-use/endpoint-antimalware-policies#threat-overrides-settings) and [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-configure). 

You can also use the [`Set-MpPreference` PowerShell cmdlet](https://technet.microsoft.com/itpro/powershell/windows/defender/set-mppreference) or [`MSFT_MpPreference` WMI class](https://msdn.microsoft.com/library/dn439477(v=vs.85).aspx) to configure these settings.

## Configure remediation options

You can configure how remediation works with the Group Policy settings described in this section.

To configure these settings:

1. On your Group Policy management computer, open the [Group Policy Management Console](https://technet.microsoft.com/library/cc731212.aspx), right-click the Group Policy Object you want to configure and click **Edit**.

2. In the **Group Policy Management Editor** go to **Computer configuration** and click **Administrative templates**.

3. Expand the tree to **Windows components > Microsoft Defender Antivirus** and then the **Location** specified in the table below.

4. Double-click the policy **Setting** as specified in the table below, and set the option to your desired configuration. Click **OK**, and repeat for any other settings.

Location | Setting | Description | Default setting (if not configured)
---|---|---|---
Scan | Create a system restore point | A system restore point will be created each day before cleaning or scanning is attempted | Disabled
Scan | Turn on removal of items from scan history folder | Specify how many days items should be kept in the scan history | 30 days
Root | Turn off routine remediation | You can specify whether Microsoft Defender Antivirus automatically remediates threats, or if it should ask the endpoint user what to do. | Disabled (threats are remediated automatically)
Quarantine | Configure removal of items from Quarantine folder | Specify how many days items should be kept in quarantine before being removed | Never removed
Threats | Specify threat alert levels at which default action should not be taken when detected | Every threat that is detected by Microsoft Defender Antivirus is assigned a threat level (low, medium, high, or severe). You can use this setting to define how all threats for each of the threat levels should be remediated (quarantined, removed, or ignored) | Not applicable
Threats | Specify threats upon which default action should not be taken when detected | Specify how specific threats (using their threat ID) should be remediated. You can specify whether the specific threat should be quarantined, removed, or ignored | Not applicable

> [!IMPORTANT]
> Microsoft Defender Antivirus detects and remediates files based on many factors. Sometimes, completing a remediation requires a reboot. Even if the detection is later determined to be a false positive, the reboot must be completed to ensure all additional remediation steps have been completed.
>
> If you are certain Microsoft Defender Antivirus quarantined a file based on a false positive, you can restore the file from quarantine after the device reboots. See [Restore quarantined files in Microsoft Defender Antivirus](restore-quarantined-files-microsoft-defender-antivirus.md).
> 
> To avoid this problem in the future, you can exclude files from the scans. See [Configure and validate exclusions for Microsoft Defender Antivirus scans](configure-exclusions-microsoft-defender-antivirus.md).

Also see [Configure remediation-required scheduled full Microsoft Defender Antivirus scans](scheduled-catch-up-scans-microsoft-defender-antivirus.md#remed) for more remediation-related settings.

## Related topics

- [Configure Microsoft Defender Antivirus scanning options](configure-advanced-scan-types-microsoft-defender-antivirus.md)
- [Configure scheduled Microsoft Defender Antivirus scans](scheduled-catch-up-scans-microsoft-defender-antivirus.md)
- [Configure and run on-demand Microsoft Defender Antivirus scans](run-scan-microsoft-defender-antivirus.md)
- [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus.md)
- [Configure end-user Microsoft Defender Antivirus interaction](configure-end-user-interaction-microsoft-defender-antivirus.md)
- [Customize, initiate, and review the results of Microsoft Defender Antivirus scans and remediation](customize-run-review-remediate-scans-microsoft-defender-antivirus.md)
- [Microsoft Defender Antivirus in Windows 10](microsoft-defender-antivirus-in-windows-10.md)
