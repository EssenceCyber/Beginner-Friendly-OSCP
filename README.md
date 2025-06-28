# Beginner-Friendly-OSCP

This guide is designed to help beginners—especially those not already in the cybersecurity industry—get started on their journey toward the OSCP (Offensive Security Certified Professional) certification.

Note: This is not a comprehensive guide to passing the OSCP exam, but guide on how to get started without being overwhelming.

# Practice Labs
To practice your skills, you can use platforms like:

Hack The Box

OffSec Proving Grounds

TryHackMe

(Some machines may require a paid subscription to access.)

# Connecting to the VPN
Download the .ovpn configuration file from the platform.

Use the following command to connect:


sudo openvpn filename.ovpn
Replace filename.ovpn with the actual file name.

Once connected, start a machine. You’ll receive an IP address (RHOST) for the target machine. Note that this IP may change every time the machine is restarted—make sure to keep track of it.

# Scanning with Nmap
Use nmap to identify open ports and services:


nmap -sC -sV -oN scan.txt RHOST
-sC: Runs default scripts

-sV: Detects service versions

-oN scan.txt: Saves the output to scan.txt

Common ports to look out for:

80: HTTP (Web Server)

22: SSH (Remote Shell)

21: FTP (File Transfer Protocol)

# FTP Enumeration
If port 21 (FTP) is open, try accessing it anonymously:


ftp RHOST
Username: anonymous

Password: (leave blank)

You may find files with credentials or other useful information here.

# HTTP & Directory Enumeration
If port 80 is open, visit the site:


http://URL
To discover hidden directories and files, use feroxbuster:


feroxbuster -u http://RHOST/ -t 10 -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt --filter-status 400,401,403,404 -L 2
# Breakdown of the Command
-u http://RHOST/ — URL to scan

-t 10 — Number of threads (speed of scan)

-w /usr/share/seclists/... — Wordlist to use

--filter-status 400,401,403,404 — Ignore common error responses

-L 2 — Recursion depth for scanning (e.g., http://site/dir/dir1/dir2/)

# Helpful links

Links which are helpful that may help with starting out on your OSCP journey

https://book.hacktricks.wiki/en/index.html

Hacktricks gives an explaination and guide on pentesting, and what you can do against the common ports

https://crackstation.net/

Crackstation is useful for cracking hashes and identifying the hash type

https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview

A useful site on what machines to start off with to get used to OSCP
