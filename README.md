#Capstone Project 3: Red Team, Blue Team, and Network Forensic Analysis
Summary: This capstone outlines the process a security engineer would use to set alerts and analyze traffic using various systems. Vulnerable machines are attacked to test the alerts and produce auditable traffic.
##Capstone Breakdown
- Defensive Security
  - Refer back to Capstone #2 for Kibana alerts and thresholds.
  - Configure and implement alerts and thresholds. 
- Offensive Security
  - Assess a vulnerable VM.
  - Attack a machine on the network.
  - Verify that the Kibana rules work as expected.
- Network Forensics
  - Capture and analyze traffic on the virtual network with Wireshark. 
  - Explain the actions that users are doing on the network.
  - Collect corporate misuse evidence
##Lab Environment


The following machines were identified on the network:
-Host
  - Windows
  - Username: azadmin
  - Password: p4ssw0rd*
  - Azure VM Host to RDP into nested machines
- ELK
  - **Operating System**:
  - Username: vagrant
  - Password: vagrant
  - Set Alerts, Kibana Dashboard
  - 192.168.1.100
- Capstone
  - **Operating System**:
  - Alert Testing, Attack Target
  - 192.168.1.105
- Target1
  - **Operating System**:
  - Vulnerable Wordpress, Attack 2nd
  - 192.168.1.110
- Kali
  - Linux
  - Username: root
  - Password: toor
  - Tools, Pen Test Machine
  - 192.168.1.110


| Name     | Function | IP Address | Operating System |Purpose |
|----------|----------|------------|------------------|-----------------|
|Host| Gateway| NEED| Linux |Azure VM Host to RDP into nested machines|
|ELK| Server| 192.168.1.100| Linux |Set Alerts, Kibana Dashboard|
|Capstone|Server| 192.168.1.105 |Linux|Alert Testing, Attack Target|
|Target1|Server| 192.168.1.110|Linux|Vulnerable Wordpress, Attack 2nd|
|Kali |Server| 192.168.1.110|Linux|Tools, Pen Test Machine|
