Red Team: Summary of Operations

Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

`nmap -sP 192.168.1.1-255`


`nmap -sV 192.168.1.110`

Due to port 80 being open, we went directly to the website via port 80 (192.168.1.110:80) and discovered that Raven Security is a WordPress Commenter, giving us the clue to run the wordpress scan. 


This scan identifies the services below as potential points of entry:
- Target 1
  - 22 - SSH
  - 80 - HTTP

_TODO: Fill out the list below. Include severity, and CVE numbers, if possible._

The following vulnerabilities were identified on each target:
- Target 1
  - List of
  - Critical
  - Vulnerabilities

_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: `flag1.txt` hash value:
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - `grep -RE flag html`

  - `flag2.txt`: _TODO: Insert `flag2.txt` hash value_


  - **Exploit Used**
    - `ssh michael@192.168.1.110`
    - `Guess-Enter password: michael`  → success

Flag3.txt:

    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Identify the command used_


    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Identify the command used_
