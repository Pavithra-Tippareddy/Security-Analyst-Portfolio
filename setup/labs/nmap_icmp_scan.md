# Lab: ICMP & Nmap Scanning

## Objective
Practice basic host discovery and scanning using **ping**, **Nmap**, and **Wireshark**.

## Tools Used
- `ping` (ICMP echo request/reply)
- `nmap` (network scanner)
- `wireshark` (packet capture & analysis)

## Steps Performed
1. **Identify target machine IP (Ubuntu VM)**  
   - Ran `ip addr show` inside Ubuntu VM.  
   - Noted interface IP `192.168.30.128`.

2. **Ping test (ICMP)**  
   - From Kali:  
   
     ping -c 4 192.168.30.128
     
   - Verified host is reachable.  
   - Captured ICMP traffic in Wireshark (filter: `icmp`).

3. **Nmap SYN scan**  
   - From Kali:  
   
     nmap -sS 192.168.30.128
      
   - Result: All 1000 scanned ports closed.

4. **Nmap service version detection**  
     nmap -sV 192.168.30.128
     
   - No services detected (all ports closed).

5. **Nmap OS detection**  
     sudo nmap -O 192.168.30.128
     
   - Output suggested target OS is **Linux (kernel 2.6–5.x range)**.

## Validation / Observations
- ICMP confirmed connectivity between Kali and Ubuntu.  
- Wireshark successfully captured ICMP requests and replies.  
- Nmap scans showed no open services, only OS fingerprinting.  
- Helps demonstrate how attackers start with host discovery before deeper exploitation.

## Screenshots Reference
- `screenshots/nmap_icmp/ping_test.png` – Ping results.  
- `screenshots/nmap_icmp/wireshark_icmp.png` – ICMP traffic in Wireshark.  
- `screenshots/nmap_icmp/nmap_scan.png` – Nmap scan output.  
- `screenshots/nmap_icmp/nmap_os.png` – OS detection result.

