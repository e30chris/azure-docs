---
title: Troubleshoot Microsoft Azure Site Recovery Provider upgrade failures | Microsoft Docs
description: Understand and 
author: vDonGlover
manager: jarrettr
ms.service: site-recovery
ms.topic: troubleshooting
ms.date: 02/05/2019
ms.author: v-doglov
---

# Troubleshoot Microsoft Azure Site Recovery Provider upgrade failures

This article helps you resolve issues that can cause failures during a Microsoft Azure Site Recovery Provider upgrade.

## The upgrade fails reporting that the latest Site Recovery Provider is already installed

When upgrading Microsoft Azure Site Recovery Provider (DRA), the Unified Setup upgrade fails and issues the error message:

Upgrade is not supported as a higher version of the software is already installed.

To upgrade, use the following steps:

1. Download the Microsoft Azure Site Recovery Unified Setup:
   1. In the "Links to currently supported update rollups" section of the [Service updates in Azure Site Recovery](service-updates-how-to.md##links-to-currently-supported-update-rollups) article, select the provider to which you are upgrading.
   2. On the rollup page, locate the **Update information** section and download the Update Rollup for Microsoft Azure Site Recovery Unified Setup.

2. Open a command prompt and navigate to the folder to which you downloaded Unified Setup file. Extract the setup files from the download using the following command, MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /x:&lt;folder path for the extracted files&gt;.
	
	Example command:

	MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /x:C:\Temp\Extracted

3. In the command prompt, navigate to the folder to which you extracted the files and run the following installation commands:
   
	CX_THIRDPARTY_SETUP.EXE /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
	UCX_SERVER_SETUP.EXE /VERYSILENT /SUPPRESSMSGBOXES /NORESTART /UPGRADE

1. Return to the folder to which you downloaded the Unified Setup and run MicrosoftAzureSiteRecoveryUnifiedSetup.exe to finish the upgrade. 

## Upgrade failure due to the 3rd-party folder being renamed

For the upgrade to succeed, the 3rd-party folder must not be renamed.

To resolve the issue.

2. Start the Registry Editor (regedit.exe) and open the HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\InMage Systems\Installed Products\10 branch.
3. Inspect the `Build_Version` key value. If it is set to the latest version, reduce version number. For example, if latest version is 9.22.\* and the `Build_Version` key set to that value, then reduce it to 9.21.\*.
4. Download the latest Microsoft Azure Site Recovery Unified Setup:
   1. In the "Links to currently supported update rollups" section of the [Service updates in Azure Site Recovery](service-updates-how-to.md##links-to-currently-supported-update-rollups) article, select the provider to which you are upgrading.
   2. On the rollup page, locate the **Update information** section and download the Update Rollup for Microsoft Azure Site Recovery Unified Setup.
5. Open a command prompt and navigate to the folder to which you downloaded Unified Setup file and the extract the setup files from the download using the following command, MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /x:&lt;folder path for the extracted files&gt;.

	Example command:

	MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /x:C:\Temp\Extracted

4. In the command prompt, navigate to the folder to which you extracted the files and run the following installation commands:
   
	CX_THIRDPARTY_SETUP.EXE /VERYSILENT /SUPPRESSMSGBOXES /NORESTART

5. Use task manager to monitor the progress of the installation. When the process for CX_THIRDPARTY_SETUP.EXE is no longer visible in task manager, proceed to the next step.
6. Verify that C:\thirdparty exists and that the folder contains the RRD libraries.
1. Return to the folder to which you downloaded the Unified Setup and run MicrosoftAzureSiteRecoveryUnifiedSetup.exe to finish the upgrade. 