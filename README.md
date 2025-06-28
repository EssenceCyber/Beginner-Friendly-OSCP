# Beginner-Friendly-OSCP
I realized that OSCP is hard to start out for those who are not in the industry thus I decided to make a guide through my experience

This is meant to help those start out on their journey and is not a comprehensive guide on how to pass the exam.



Beginner-Friendly OSCP Guide
This guide is designed to help beginners—especially those not already in the cybersecurity industry—get started on their journey toward the OSCP (Offensive Security Certified Professional) certification.

Note: This is not a comprehensive guide to passing the OSCP exam, but rather a collection of practical steps and tools I found useful during my preparation.

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
