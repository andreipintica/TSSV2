# TSSV2
TSSv2: Windows PowerShell based Troubleshshooting script (TSS) toolset  This is the Windows PowerShell based equivalent for the CMD based TSS toolset.

🔧 Technologies & Tools
 
![](https://img.shields.io/badge/OS-Windows-informational?style=flat&logo=Microsoft&logoColor=white&color=2bbc8a) ![](https://img.shields.io/badge/Code-VisualStudioCode-informational?style=flat&logo=VisualStudioCode&logoColor=white&color=2bbc8a)  ![](https://img.shields.io/badge/Code-PowerShell-informational?style=flat&logo=PowerShell&logoColor=white&color=2bbc8a) ![](https://img.shields.io/badge/Cloud-MicrosoftAzure-informational?style=flat&logo=MicrosoftAzure&logoColor=white&color=2bbc8a) 

# Download
For Download please use official Microsoft sites: 

aka.ms/getTSS
https://cesdiagtools.blob.core.windows.net/windows/TSSv2.zip
**Note**: https://cesdiagtools.blob.core.windows.net/windows/TSSv2.ver will always reflect latest version number

# Description

TSSv2 (TroubleShootingScript Version 2) is PowerShell based Tool and Framework for rapid flexible data collection and diagnostic with a goal to resolve customer support cases in the most efficient and secure way. TSSv2 offers extensible framework for developers and engineers to incorporate their specific tracing scenarios. 

TSSv2 code is signed and we recommend local machine "RemoteSigned" PowerShell execution policy https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2#remotesigned

Please note that TSSv2 must be executed in the context of account with admin rights on the local system and EULA must be accepted (once EULA is accepted, TSSv2 will not prompt again)

Public KB: https://docs.microsoft.com/en-us/troubleshoot/windows-client/windows-troubleshooters/introduction-to-troubleshootingscript-toolset-tssv2

Collect ETW/WPP traces for Windows components: 
                                              - Also Netsh(packet capture)/Procmon/PerfMon/PSR/Video/SysMon/WPR/xPerf/TTD... can be taken at the same time.
                                              - This script supports -StartAutoLogger for ETW traces and in addition to this, BootLogging including BootTrace(WPR), persistent=yes(Netsh) and /BootLogging(Procmon) are also supported.

# How to run the tool:

Run 'Get-Help .\TSSv2.ps1 -full' for more detail.

   USAGE SUMMARY:
   Script accepts data collection start actions: -Start/-StartAutologger/-StartDiag/-CollectLog 
   and uses -Stop to stop data collection or stops automatically by trigger with -WaitEvent option supplied.

   a) Start multiple traces, for exmple, UEX_RDS and ADS_Kerb trace, you should use this option if you know exactly what to trace:
      PS> .\TSSv2.ps1 -UEX_RDS -ADS_Kerb

   b) Start traces for PKI Client scenario to collect ADS basic data:
      PS> .\TSSv2.ps1 -Scenario ADS_Basic

   c) Start traces for Auth scenario to collect broad set of AUTH data:
      PS> .\TSSv2.ps1 -Scenario ADS_Auth

   d) Start traces for ADCS (cert authority) service and full AUTH data (recommended way to get full set of data from ADCS):
      PS> .\TSSv2.ps1 -Scenario ADS_Auth -CustomParams ADS_PKIADCS -ADS_ADCS -netsh

   e) Start traces and WPR/Netsh(packet capturing)/Procmon at the same time:
      PS> .\TSSv2.ps1 -UEX_RDS -ADS_Auth -WPR General -Netsh -Procmon

   f) Collect WMI, WinRM, Task Scheduler and Print logs:
      PS> .\TSSv2.ps1 -CollectLog UEX_WMI,UEX_WinRM,UEX_Sched,UEX_Print

   Stop all traces including WPR/Netsh/Procmon/PSR:
      PS> .\TSSv2.ps1 -Stop

   StartAutoLogger for persistent/boot ETW traces and WPR(BootTrace), Netsh(persistent=yes) and Procmon(BootLogging):
      PS> .\TSSv2.ps1 -StartAutoLogger -UEX_RDS -WPR General -Netsh -Procmon
      PS> Restart-Computer
      PS> .\TSSv2.ps1 -Stop  # Stop all autoLogger sessions and settings

   Collect just logs for each component:
      PS> .\TSSv2.ps1 -CollectLog UEX_IME,UEX_Print,BasicLog

   Display built-in Help Menu
      PS> .\TSSv2.ps1 -Help

# Quick reference:

KB5011690 WinX: FastStart / Quick Reference: TSSv2 commands for TSS (v1) users

KB5011695 WinX: TSSv2: CX ready email template for TSSv2 Action Plans

