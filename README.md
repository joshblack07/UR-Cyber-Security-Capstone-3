# Capstone Project 3: Red Team, Blue Team, and Network Forensic Analysis

Summary: This capstone outlines the process a security engineer would use to set alerts and analyze traffic using various systems. Vulnerable machines are attacked to test the alerts and produce auditable traffic.

## Capstone Breakdown
- [Defensive Security Report](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Reports/Defensive_Report.md "Defensive Security Report")
  - Refer back to [Capstone #2](https://github.com/joshblack07/UR-Cyber-Security-Red_vs_Blue "Capstone #2")  for Kibana alerts and thresholds.
  - Configure and implement alerts and thresholds. 
- [Offensive Security Report](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Reports/Offensive_Report.md "Offensive Security Report")
  - Assess a vulnerable VM.
  - Attack a machine on the network.
  - Verify that the Kibana rules work as expected.
- Network Forensics (Report)
  - Capture and analyze traffic on the virtual network with Wireshark. 
  - Explain the actions that users are doing on the network.
  - Collect corporate misuse evidence

## Lab Environment

![Network Diagram](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/final-project-setup.png "Network Diagram")

| Name      | IP Address |OS|Purpose |
|----------|------------|-|----------------|
|Host| 192.168.1.1 | Microsoft Windows |Azure VM Host to RDP into nested machines|
|ELK|  192.168.1.100| Linux Ubuntu |Set Alerts, Kibana Dashboard|
|Capstone| 192.168.1.105 | Linux |Alert Testing, Attack Target|
|Target1| 192.168.1.110| Linux Debian 3.16.57 |Vulnerable Wordpress, Attack 2nd|
|Kali | 192.168.1.110| Linux |Tools, Pen Test Machine|


## Group

- [Josh Black](https://github.com/joshblack07)
- [Laura Pratt](https://github.com/laurapratt87)
- [Courtney Templeton](https://github.com/cltempleton1127)
- [Robbie Drescher](https://github.com/RobDresch)
- Julian Baker

