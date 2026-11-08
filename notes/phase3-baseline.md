# Phase 3: Getting a baseline

Before attacking anything, I wanted to know what normal looks like on my Windows VM. If I can't tell what's normal, I can't tell what's an attack.

## Setup so far
Wazuh 4.14 runs on an Ubuntu VM. My Windows VM (agent 004) sends its Sysmon logs to it. I first installed the agent on my own laptop by mistake, then moved it into the VM, because I don't want to run attack tests on my real machine.

## What I saw
About 90 minutes after setup, Wazuh had raised 97 Sysmon alerts. Most came in two bursts, which lined up with me running setup commands and Windows installing updates. When I left the VM alone, it went quiet.

## The alerts that looked scary
| Rule | What it says | Level | What it actually was |
|---|---|---|---|
| 92058 | Application Compatibility Database launched | 12 | Windows maintenance |
| 92213 | Executable file dropped in folder commonly used by malware | 15 | PowerShell's own policy-test file |
| 92205 | PowerShell created an executable in the Windows root folder | 9 | My setup commands |

## How I checked 92058
The process was sdbinst.exe in System32, started by svchost.exe (the PcaSvc service) as SYSTEM, with the flags -m -bg and no .sdb file named. A real shim attack would name a custom database. This one installed nothing, so I called it a false positive.

## How I checked 92213
The file was __PSScriptPolicyTest_*.ps1 in my Temp folder, created by my own account at 23:58 Lagos time, when I was using PowerShell. PowerShell makes that file itself. False positive.

## What I got wrong at first
I told myself an alert was safe because it said manager.name: socadmin. That field is just my Wazuh server's name and it appears on every alert, so it proves nothing. The fields that matter are inside data.win.eventdata: what ran, who ran it, from where, and when.

## What I'm thinking about next
A level 15 alert that fires every time I open PowerShell would be useless on my phone. I don't want to switch these rules off, because they catch real things. I want narrow exceptions instead.
