# Lab: Nmap & ICMP Traffic Analysis

## Objective
To perform active network reconnaissance using **Nmap** from Kali Linux against an Ubuntu VM and validate visibility of traffic using **Wireshark**.  
This simulates how attackers scan systems and how defenders can detect such behavior.

## Environment
- **Attacker Machine**: Kali Linux (WSL / VM)  
- **Target Machine**: Ubuntu (VM running in VMware)  
- Both systems on the same local network (NAT/Bridged).

## Steps Performed

### 1. Identify Target IP
On Ubuntu VM:
* ip addr show
* Discovered IP: 192.168.30.128

2. Basic ICMP Connectivity:
From Kali (attacker):

* ping -c 4 192.168.30.128
- Verified host is reachable.
- Captured ICMP echo requests/replies in Wireshark.

3. Nmap Scanning
a) SYN Scan (default & stealthy)
nmap -sS 192.168.30.128

## Result:
*Host responded.
*All 1000 scanned TCP ports were closed.


b) Service Version Detection
   * nmap -sV 192.168.30.128
     
## Result:
* No open services discovered.
* Confirmed target was hardened / had no listening services.


c) Operating System Detection
   * sudo nmap -O 192.168.30.128
     
## Result:
* Detected OS family: Linux Kernel 2.6.X – 5.X
* Warning shown since no open ports were available, but fingerprinting still possible.

### 4) Wireshark Validation
* On Ubuntu interface (ens33), launched Wireshark capture.
* Observed:
* ICMP Echo Request/Reply packets from ping.
* TCP SYN packets from Nmap scans.
* No full connections (SYN → SYN/ACK → ACK) were seen because ports were closed.

## Findings
* ICMP confirmed host discovery.
* Nmap SYN and service scans showed no open ports on Ubuntu host.
* OS detection still provided Linux kernel range, proving that attackers can learn about targets even with closed ports.
* Wireshark confirmed the packet flow, which analysts can detect in SOC investigations.

## SOC Analyst Notes.
* Repeated ICMP pings + Nmap-style SYN scans are strong indicators of reconnaissance activity.
* In real SOC work, we’d set detection rules in Splunk/SIEM:

## spl
* index=network_traffic "Nmap" OR "SYN scan"
  
* Analysts must distinguish between legitimate scans (IT team) and malicious probing.


  
   


