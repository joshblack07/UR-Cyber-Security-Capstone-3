# Network Analysis

## Time Thieves

At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

- They have set up an Active Directory network.
- They are constantly watching videos on YouTube.
 -Their IP addresses are somewhere in the range 10.6.12.0/24.

You must inspect your traffic capture to answer the following questions:
What is the domain name of the users' custom site?

- [frank-n-ted.com](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_franknted_12_1.PNG "frank-n-ted.com")

What is the IP address of the Domain Controller (DC) of the AD network?

- [10.6.12.12](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_franknted_12.PNG "10.6.12.12")
 
What is the name of the malware downloaded to the 10.6.12.203 machine? Once you have found the file, export it to your Kali machine's desktop.

- [june11.dll](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_june11.PNG "june11.dll")
  - [TCP Stream](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_june11_tcp_stream.PNG "TCP_Stream")
  - [HTTP Export](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_june11_http_export.PNG "HTTP Export")
 
Upload the file to VirusTotal.com. What kind of malware is this classified as?

- [Trojan](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/virustotal_june11.PNG "Virus_Total_Trojan")

## Vulnerable Windows Machines

The Security team received reports of an infected Windows host on the network. They know the following:
- Machines in the network live in the range 172.16.4.0/24.
- The domain mind-hammer.net is associated with the infected computer.
- The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.
- The network has standard gateway and broadcast addresses.

Inspect your traffic to answer the following questions:

Find the following information about the infected Windows machine:
- Host name: [ROTTERDAM-PC](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_rotterdam.PNG "ROTTERDAM-PC")
- IP address: [172.16.4.205](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_rotterdam.PNG "172.16.4.205")
- MAC address: [00:59:07:b0:63:a4](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_rotterdam.PNG "00:59:07:b0:63:a4")

What is the username of the Windows user whose computer is infected?
- [mattijs.derives](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_matthijs.PNG "Windows User")

What are the IP addresses used in the actual infection traffic?
- [185.243.115.84, 172.16.4.205](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_infected3.PNG "Infection Traffic")

As a bonus, retrieve the desktop background of the Windows host.
- [empty.gif%3fss&ss1img.png](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_background2.PNG "Desktop Background")
  - [HTTP object list](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_background.PNG "HTTP_obecjt_list")
  
## Illegal Downloads

IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.

IT shared the following about the torrent activity:
- The machines using torrents live in the range 10.0.0.0/24 and are clients of an AD domain.
- The DC of this domain lives at 10.0.0.2 and is named DogOfTheYear-DC.
- The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic and answer the following questions:

Find the following information about the machine with IP address 10.0.0.201:
- MAC address: [00:16:17:18:66:c8](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_elmer_blanco.PNG "00:16:17:18:66:c8")
- Windows username: [elmer.blanco](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_elmer_blanco.PNG "elmer.blanco")
- OS version: [Windows 10.0](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_OS.png "Windows 10.0")


Which torrent file did the user download?
- [Betty_Boop_Rhythm_on_the_Reservation.avi](https://github.com/joshblack07/UR-Cyber-Security-Capstone-3/blob/main/Resources/wireshark_torrent.PNG "Torrent")

 
