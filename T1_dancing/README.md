## Dancing Hackthebox


#### Step 0x01: `Network Scan`
as usual, we will run a nmap scan to find open ports and services.
```bash
# nmap command:
nmap -A -sV --privileged -T4 <ip> -p- -O -sC -v
```
|PORT|STATE|SERVICE|VERSION|
|----|----|----|----|
|135/tcp|open|msrpc|Microsoft Windows RPC|
|135/tcp|open|msrpc|Microsoft Windows RPC|
|445/tcp|open|microsoft-ds?| |
|5985/tcp|open|http|Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)|
|47001/tcp|open|http|Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)|
|49664/tcp|open|msrpc|Microsoft Windows RPC|

**Script Result**
```terminal
Host script results:
| smb2-time: 
|   date: 2024-06-28T10:59:42
|_  start_date: N/A
|_clock-skew: 3h59m59s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
```

