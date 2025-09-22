# Network Scanning with Nmap

## Objective
Discover open ports on devices in the local network to understand network exposure and potential security risks.

## Tools Used
- Nmap (v7.95)
- (Optional) Wireshark

## Steps Performed
1. Installed Nmap on Kali Linux.
2. Found local IP range: `172.29.208.X/24`.
3. Ran TCP SYN scan:
   ```bash
   sudo nmap -sS 172.29.208.X/24
   ```
4. Identified live hosts and open ports.
5. Researched common services running on discovered ports.
6. Analyzed potential risks.
7. Saved scan results (`scan-results.txt`).

## Scan Results
**Command executed:**
```
sudo nmap -sS 172.29.208.X/24
```

**Output (simplified):**
```
Nmap scan report for DESKTOP-07EUH6U (172.29.208.X)
Host is up.

PORT     STATE SERVICE
135/tcp  open  msrpc
2179/tcp open  vmrdp
3000/tcp open  ppp

Nmap done: 256 IP addresses (1 host up) scanned in 7.24 seconds
```

## Analysis
- **135/tcp (msrpc)** → Microsoft RPC service. Common in Windows environments but often targeted by malware. Should not be exposed to the internet.  
- **2179/tcp (vmrdp)** → Hyper-V Remote Desktop Protocol. Used for VM management. Restrict access if not needed.  
- **3000/tcp (ppp)** → Typically used by developer applications (e.g., Node.js, Grafana). Investigate which process is listening on this port.

## Security Risks
- RPC and RDP services can be exploited if exposed publicly.
- Unknown service on port 3000 should be verified and restricted.
- Best practice: close unused ports, enable firewall, and keep services updated.

## How to reproduce the scan
To save the scan results in text format:
```bash
sudo nmap -sS -sV 172.29.208.X -oN scan-results.txt
```

## Files included in this repo
- `README.md` (this file)
- `scan-results.txt` (raw output summary)
