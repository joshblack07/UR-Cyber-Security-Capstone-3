# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

![Network Diagram](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/final-project-setup.png "Network Diagram")

| Name      | IP Address |OS|Purpose |
|----------|------------|-|----------------|
|Host| 192.168.1.1 | Microsoft Windows |Azure VM Host to RDP into nested machines|
|ELK|  192.168.1.100| Linux Ubuntu |Set Alerts, Kibana Dashboard|
|Capstone| 192.168.1.105 | Linux |Alert Testing, Attack Target|
|Target1| 192.168.1.110| Linux Debian 3.16.57 |Vulnerable Wordpress, Attack 2nd|
|Kali | 192.168.1.110| Linux |Tools, Pen Test Machine|


### Description of Targets

The target of this attack was: `Target 1` IP: '192.168.1.110'

Target 1 is an Apache web server and has SSH enabled, so `port 80` and `port 22` are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors

The alert Excessive HTTP Errors is implemented as follows:

- `WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes`

- Metric:
  - WHEN count() GROUPED OVER top 5 ‘http.response.status_code’
- Threshold:
  - IS ABOVE 400
- Vulnerability Mitigated:
  - Enumeration/Brute Force
- Reliability:
  - The alert is highly reliable. Measuring by error codes 400 and above will filter out any normal or successful responses. 400+ codes are client and server errors which are of more concern. Especially when taking into account these error codes going off at a high rate.


#### HTTP Request Size Monitor

The alert HTTP Request Size Monitor is implemented as follows:

- `WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute`

- Metric:
  - WHEN sum() of http.request.bytes OVER all documents
- Threshold:
  - IS ABOVE 3500
- Vulnerability Mitigated:
  - Code injection in HTTP requests (XSS and CRLF) or DDOS
- Reliability:
  - Alert could create false positives. It comes in at a medium reliability. There is a possibility for a large non malicious HTTP request or legitimate HTTP traffic.

#### CPU Usage Monitor

The alert CPU Usage Monitor is implemented as follows:

- `WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes`

- Metric:
  - WHEN max() OF system.process.cpu.total.pct OVER all documents
- Threshold:
  - IS ABOVE 0.5
- Vulnerability Mitigated:
  - Malicious software, programs (malware or viruses) running taking up resources
- Reliability:
  - The alert is highly reliable. Even if there isn’t a malicious program running this can still help determine where to improve on CPU usage.

### Suggestions for Going Further

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:

- Vulnerability 1: Excessive HTTP Errors
  - **Patch**: Password Hardening
    - Configure Windows Group Policies to have a strong password policy for accounts.
    - Implementation of Multi-Factor Authentication or CAPTCHA ([reference](https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks "HTTP_Error_Hardening")) 
  - **Why It Works**: Having a strong password will make it harder to guess or brute force.
  - **Patch**: WordPress-specific hardening ([reference](https://wordpress.org/support/article/hardening-wordpress/ "WordPress_Hardening")) 
    - Make sure wordpress is regularly updated
    - Implementation of a security plugin such as [WordFence](https://www.wordfence.com/?gclid=CjwKCAiAksyNBhAPEiwAlDBeLFXu4fn-ttlQzFbdL4dR8QZGqN2yfi9_3OcO9-43tXo2y24LpgizxBoCbb8QAvD_BwE "WordFence_Website")
    - Disable public access to sections such as `/wp-admin` and `/wp-login.php`
  - **Why It Works**: Having a strong password will make it harder to guess or brute force.
  
- Vulnerability 2: HTTP Request Size Monitor
  - **Patch**: Code Injection/DDOS Hardening
    - Implementation of HTTP Request Limit on the web server ([reference](https://www.tomaz.me/2013/09/15/avoiding-ddos-attacks-caused-by-large-http-request-bodies-by-enforcing-a-hard-limit-in-your-web-server.html "HTTP_Request_Limit"))
    - Use of modern intrusion prevention and threat management systems that include firewalls, VPN's, content filtering, and load balancing.  
  - **Why It Works**: Monitoring request sizes of HTTP packets can minimize denial of service threats. This will help reject these requests that are too large.
  
- Vulnerability 3: CPU Usage Monitor
  - **Patch**: Virus and Malware Hardening
    - Using Host Intrusion Prevention System (HIDS) to identify potential denial of service attacks.
    - Implementing at least one anti-virus software
  - **Why It Works**: This preventative measure can alert and stop malware by monitoring processing behavior. 
