# Exam Preparation

## OS INT - for the exam

- Google
- Bing
- Duckduckgo
- GitHub
- Gitlab
- Pastebin

## Cheat Sheets

- [HackTricks](https://book.hacktricks.xyz/sw)
- [ChatGPT](https://chatgpt.com/)


## Example steps

Start an `nmap` port scan and save the result in a file.

```bash
nmap -p- 192.168.0.204 -vv -oN
```

`-p-`: Tells Nmap to scan all 65,535 TCP ports on the target (192.168.1.100). By default, Nmap only scans the top 1,000 ports unless specified otherwise.
`192.168.1.100`: The target IP address to be scanned.
`-vv`: Sets very verbose output mode, which provides detailed feedback during the scan process. It shows what Nmap is doing in real-time, such as which ports are being scanned and what responses are being received.
`-oN`: Output is stored in a standard text file

![image](https://github.com/user-attachments/assets/39ee27ff-c1d9-4a01-9cc8-4bd885485501)


The open ports are:

```
80,135,139,445,2179,5040,5357,5938,7680,32400,49664,49665,49666,49667,49668,49673,49674,49704
```

Scan each open port with the `nmap`

```bash
nmap -sC -sV -p 80,135,139,445,2179,5040,5357,5938,7680,32400,49664,49665,49666,49667,49668,49673,49674,49704 192.168.0.204 -vv -oN nmapFull.txt
```

- `-sC`: Enables the default scripts from Nmap's script library. These scripts gather additional information about services running on open ports (e.g., version details, vulnerabilities, misconfiguration).
- `-sV`: Enables version detection, which attempts to determine the versions of the services running on the specified ports.
- `-p`: Specifies the list of ports to scan. In this case, Nmap will focus only on these specific ports.

![image](https://github.com/user-attachments/assets/20f0e55b-9811-44bd-83f4-f8bd80f64e27)



