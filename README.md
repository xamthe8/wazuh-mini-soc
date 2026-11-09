- Wazuh Mini SOC

Home SOC lab built with Wazuh SIEM. Attack simulation, detection engineering, and incident response write-ups.

-- Why I built this

I'm building toward an entry-level SOC analyst role. I hold the ISC2 CC certification and practice on TryHackMe, and I wanted hands-on experience with the full blue team workflow: collecting logs, detecting attacks, triaging alerts, and tuning detections.

My main focus is alerting and tuning, so the right high-severity alerts reach me quickly without drowning in noise.

Lab environment

- Host: Windows laptop, i7-10870H, 32 GB RAM, VirtualBox
- Wazuh 4.14 (all-in-one) on Ubuntu Server
- Windows VM endpoint with Sysmon (SwiftOnSecurity config)
- Atomic Red Team for attack simulation

-- What's in this repo

- [Baseline and false positive triage](notes/phase3-baseline.md)
- [Attack simulation and first detection gap](notes/phase4-attack-simulation.md)
- [Custom detection rule 100100](Detections/100100-schtasks-create.xml)
