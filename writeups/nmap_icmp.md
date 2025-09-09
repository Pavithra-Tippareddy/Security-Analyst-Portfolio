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

4. Service Version Detection
   * nmap -sV 192.168.30.128
## Result:
* No open services discovered.
* Confirmed target was hardened / had no listening services.

   


