---
date: 2025-06-19 07:18:58
layout: post
title: OSCP Cheatsheet
description: I will be adding more to this as I go on my Journey
image: /assets/img/uploads/oscp-700x700-321861135.png
optimized_image: /assets/img/uploads/oscp-700x700-321861135.png
category: research
tags:
  - oscp
  - hacking
  - exam
  - study
author: CyberDucky
paginate: true
---
# General

<aside>
💡 For Finding all important files in Windows

`cd c:\Users` then
`tree /F`

</aside>

## Important Locations

<details>
<summary>Windows</summary>
Windows
    

</details>
<details>
<summary>Linux</summary>
    
 

```
powershell
    /etc/passwd
    /etc/shadow
    /etc/aliases
    /etc/anacrontab
    /etc/apache2/apache2.conf
    /etc/apache2/httpd.conf
    /etc/apache2/sites-enabled/000-default.conf
    /etc/at.allow
    /etc/at.deny
    /etc/bashrc
    /etc/bootptab
    /etc/chrootUsers
    /etc/chttp.conf
    /etc/cron.allow
    /etc/cron.deny
    /etc/crontab
    /etc/cups/cupsd.conf
    /etc/exports
    /etc/fstab
    /etc/ftpaccess
    /etc/ftpchroot
    /etc/ftphosts
    /etc/groups
    /etc/grub.conf
    /etc/hosts
    /etc/hosts.allow
    /etc/hosts.deny
    /etc/httpd/access.conf
    /etc/httpd/conf/httpd.conf
    /etc/httpd/httpd.conf
    /etc/httpd/logs/access_log
    /etc/httpd/logs/access.log
    /etc/httpd/logs/error_log
    /etc/httpd/logs/error.log
    /etc/httpd/php.ini
    /etc/httpd/srm.conf
    /etc/inetd.conf
    /etc/inittab
    /etc/issue
    /etc/knockd.conf
    /etc/lighttpd.conf
    /etc/lilo.conf
    /etc/logrotate.d/ftp
    /etc/logrotate.d/proftpd
    /etc/logrotate.d/vsftpd.log
    /etc/lsb-release
    /etc/motd
    /etc/modules.conf
    /etc/motd
    /etc/mtab
    /etc/my.cnf
    /etc/my.conf
    /etc/mysql/my.cnf
    /etc/network/interfaces
    /etc/networks
    /etc/npasswd
    /etc/passwd
    /etc/php4.4/fcgi/php.ini
    /etc/php4/apache2/php.ini
    /etc/php4/apache/php.ini
    /etc/php4/cgi/php.ini
    /etc/php4/apache2/php.ini
    /etc/php5/apache2/php.ini
    /etc/php5/apache/php.ini
    /etc/php/apache2/php.ini
    /etc/php/apache/php.ini
    /etc/php/cgi/php.ini
    /etc/php.ini
    /etc/php/php4/php.ini
    /etc/php/php.ini
    /etc/printcap
    /etc/profile
    /etc/proftp.conf
    /etc/proftpd/proftpd.conf
    /etc/pure-ftpd.conf
    /etc/pureftpd.passwd
    /etc/pureftpd.pdb
    /etc/pure-ftpd/pure-ftpd.conf
    /etc/pure-ftpd/pure-ftpd.pdb
    /etc/pure-ftpd/putreftpd.pdb
    /etc/redhat-release
    /etc/resolv.conf
    /etc/samba/smb.conf
    /etc/snmpd.conf
    /etc/ssh/ssh_config
    /etc/ssh/sshd_config
    /etc/ssh/ssh_host_dsa_key
    /etc/ssh/ssh_host_dsa_key.pub
    /etc/ssh/ssh_host_key
    /etc/ssh/ssh_host_key.pub
    /etc/sysconfig/network
    /etc/syslog.conf
    /etc/termcap
    /etc/vhcs2/proftpd/proftpd.conf
    /etc/vsftpd.chroot_list
    /etc/vsftpd.conf
    /etc/vsftpd/vsftpd.conf
    /etc/wu-ftpd/ftpaccess
    /etc/wu-ftpd/ftphosts
    /etc/wu-ftpd/ftpusers
    /logs/pure-ftpd.log
    /logs/security_debug_log
    /logs/security_log
    /opt/lampp/etc/httpd.conf
    /opt/xampp/etc/php.ini
    /proc/cmdline
    /proc/cpuinfo
    /proc/filesystems
    /proc/interrupts
    /proc/ioports
    /proc/meminfo
    /proc/modules
    /proc/mounts
    /proc/net/arp
    /proc/net/tcp
    /proc/net/udp
    /proc/<PID>/cmdline
    /proc/<PID>/maps
    /proc/sched_debug
    /proc/self/cwd/app.py
    /proc/self/environ
    /proc/self/net/arp
    /proc/stat
    /proc/swaps
    /proc/version
    /root/anaconda-ks.cfg
    /usr/etc/pure-ftpd.conf
    /usr/lib/php.ini
    /usr/lib/php/php.ini
    /usr/local/apache/conf/modsec.conf
    /usr/local/apache/conf/php.ini
    /usr/local/apache/log
    /usr/local/apache/logs
    /usr/local/apache/logs/access_log
    /usr/local/apache/logs/access.log
    /usr/local/apache/audit_log
    /usr/local/apache/error_log
    /usr/local/apache/error.log
    /usr/local/cpanel/logs
    /usr/local/cpanel/logs/access_log
    /usr/local/cpanel/logs/error_log
    /usr/local/cpanel/logs/license_log
    /usr/local/cpanel/logs/login_log
    /usr/local/cpanel/logs/stats_log
    /usr/local/etc/httpd/logs/access_log
    /usr/local/etc/httpd/logs/error_log
    /usr/local/etc/php.ini
    /usr/local/etc/pure-ftpd.conf
    /usr/local/etc/pureftpd.pdb
    /usr/local/lib/php.ini
    /usr/local/php4/httpd.conf
    /usr/local/php4/httpd.conf.php
    /usr/local/php4/lib/php.ini
    /usr/local/php5/httpd.conf
    /usr/local/php5/httpd.conf.php
    /usr/local/php5/lib/php.ini
    /usr/local/php/httpd.conf
    /usr/local/php/httpd.conf.ini
    /usr/local/php/lib/php.ini
    /usr/local/pureftpd/etc/pure-ftpd.conf
    /usr/local/pureftpd/etc/pureftpd.pdn
    /usr/local/pureftpd/sbin/pure-config.pl
    /usr/local/www/logs/httpd_log
    /usr/local/Zend/etc/php.ini
    /usr/sbin/pure-config.pl
    /var/adm/log/xferlog
    /var/apache2/config.inc
    /var/apache/logs/access_log
    /var/apache/logs/error_log
    /var/cpanel/cpanel.config
    /var/lib/mysql/my.cnf
    /var/lib/mysql/mysql/user.MYD
    /var/local/www/conf/php.ini
    /var/log/apache2/access_log
    /var/log/apache2/access.log
    /var/log/apache2/error_log
    /var/log/apache2/error.log
    /var/log/apache/access_log
    /var/log/apache/access.log
    /var/log/apache/error_log
    /var/log/apache/error.log
    /var/log/apache-ssl/access.log
    /var/log/apache-ssl/error.log
    /var/log/auth.log
    /var/log/boot
    /var/htmp
    /var/log/chttp.log
    /var/log/cups/error.log
    /var/log/daemon.log
    /var/log/debug
    /var/log/dmesg
    /var/log/dpkg.log
    /var/log/exim_mainlog
    /var/log/exim/mainlog
    /var/log/exim_paniclog
    /var/log/exim.paniclog
    /var/log/exim_rejectlog
    /var/log/exim/rejectlog
    /var/log/faillog
    /var/log/ftplog
    /var/log/ftp-proxy
    /var/log/ftp-proxy/ftp-proxy.log
    /var/log/httpd-access.log
    /var/log/httpd/access_log
    /var/log/httpd/access.log
    /var/log/httpd/error_log
    /var/log/httpd/error.log
    /var/log/httpsd/ssl.access_log
    /var/log/httpsd/ssl_log
    /var/log/kern.log
    /var/log/lastlog
    /var/log/lighttpd/access.log
    /var/log/lighttpd/error.log
    /var/log/lighttpd/lighttpd.access.log
    /var/log/lighttpd/lighttpd.error.log
    /var/log/mail.info
    /var/log/mail.log
    /var/log/maillog
    /var/log/mail.warn
    /var/log/message
    /var/log/messages
    /var/log/mysqlderror.log
    /var/log/mysql.log
    /var/log/mysql/mysql-bin.log
    /var/log/mysql/mysql.log
    /var/log/mysql/mysql-slow.log
    /var/log/proftpd
    /var/log/pureftpd.log
    /var/log/pure-ftpd/pure-ftpd.log
    /var/log/secure
    /var/log/vsftpd.log
    /var/log/wtmp
    /var/log/xferlog
    /var/log/yum.log
    /var/mysql.log
    /var/run/utmp
    /var/spool/cron/crontabs/root
    /var/webmin/miniserv.log
    /var/www/html<VHOST>/\_\_init\_\_.py
    /var/www/html/db_connect.php
    /var/www/html/utils.php
    /var/www/log/access_log
    /var/www/log/error_log
    /var/www/logs/access_log
    /var/www/logs/error_log
    /var/www/logs/access.log
    /var/www/logs/error.log
    \~/.atfp_history
    \~/.bash_history
    \~/.bash_logout
    \~/.bash_profile
    \~/.bashrc
    \~/.gtkrc
    \~/.login
    \~/.logout
    \~/.mysql_history
    \~/.nano_history
    \~/.php_history
    \~/.profile
    \~/.ssh/authorized_keys
    #id_rsa, id_ecdsa, id_ecdsa_sk, id_ed25519, id_ed25519_sk, and id_dsa
    \~/.ssh/id_dsa
    \~/.ssh/id_dsa.pub
    \~/.ssh/id_rsa
    \~/.ssh/id_edcsa
    \~/.ssh/id_rsa.pub
    \~/.ssh/identity
    \~/.ssh/identity.pub
    \~/.viminfo
    \~/.wm_style
    \~/.Xdefaults
    \~/.xinitrc
    \~/.Xresources
    \~/.xsession
```

</details>

### GitHub recon

* You need to find traces of the `.git` files on the target machine.
* Now navigate to the directory where the file is located, a potential repository.

# Reconnaissance

### P﻿ort Scanning:

* N﻿MAP\
  M﻿ost used commands:

  ```
  #use -Pn option if you're getting nothing in the scan
  nmap -sC -sV <IP> -v #Basic scan
  nmap -T4 -A -p- <IP> -v #complete scan
  sudo nmap -sV -p 443 --script "vuln" 192.168.50.124 #running vuln category scripts

  #NSE
  updatedb
  locate .nse | grep <name>
  sudo nmap --script="name" <IP> #here we can specify other options like specific ports...etc

  Test-NetConnection -Port <port> <IP>   #powershell utility

  1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("IP", $_)) "TCP port $_ is open"} 2>$null #automating port scan of first 1024 ports in powershell
  ```
* Rustscan (Def faster than NMAP)

### F﻿inding Subdomains and Directory Bruteforcing:

* s﻿ubdir 
* f﻿fuf (Good for directory brueforcing and subdomain finding)
* d﻿irbuster

I﻿f you are given an IP address but you find a DNS name, then you can modify your /etc/hosts files to point to the DNS name. If there is a subdomain found, add another entry in /etc/hosts file so that you can access it via your browser.

- - -

### **S﻿MB Share Finding:**

```
sudo nbtscan -r 192.168.50.0/24 #IP or range can be provided

\#NSE scripts can be used
locate .nse | grep smb
nmap -p445 --script="name" $IP 

\#In windows we can view like this
net view \<computername/IP> /all

\#crackmapexec
crackmapexec smb <IP/range>\
crackmapexec smb 192.168.1.100 -u username -p password
crackmapexec smb 192.168.1.100 -u username -p password --shares #lists available shares
crackmapexec smb 192.168.1.100 -u username -p password --users #lists users
crackmapexec smb 192.168.1.100 -u username -p password --all #all information
crackmapexec smb 192.168.1.100 -u username -p password -p 445 --shares #specific port
crackmapexec smb 192.168.1.100 -u username -p password -d mydomain --shares #specific domain
#Inplace of username and password, we can include usernames.txt and passwords.txt for password-spraying or bruteforcing.

# Smbclient

smbclient -L //IP #or try with 4 /'s
smbclient //server/share
smbclient //server/share -U <username>
smbclient //server/share -U domain/username

\#SMBmap
smbmap -H <target_ip>
smbmap -H <target_ip> -u <username> -p <password>
smbmap -H <target_ip> -u <username> -p <password> -d <domain>
smbmap -H <target_ip> -u <username> -p <password> -r <share_name>

\#Within SMB session
put <file> #to upload file
get <file> #to download file
```

- - -

# Username and Password Wordlists

## Username Wordlists

* **`SecLists/Discovery/Usernames/top-usernames-shortlist.txt`**\
  ~5,500 of the most common usernames for web-login and SSH/FTP brute-forcing. ([GitHub](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com "danielmiessler/SecLists"), [therealunicornsecurity.github.io](https://therealunicornsecurity.github.io/OSCP/ "OSCP tips and tricks – Unicorn Security – Breaching Unicorns"))
* **`SecLists/Discovery/Usernames/cirt-default-usernames.txt`**\
  ~2,500 default service accounts (e.g. FTP, MySQL, etc.). ([GitHub](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com "danielmiessler/SecLists"), [therealunicornsecurity.github.io](https://therealunicornsecurity.github.io/OSCP/ "OSCP tips and tricks – Unicorn Security – Breaching Unicorns"))
* **Username Anarchy** (tool: `urbanadventurer/username-anarchy`)\
  Generate permutations (first.last, f_last, initials, etc.) from known names or email addresses. ([Medium](https://medium.com/%40jakemcgreevy/creating-custom-username-and-password-lists-on-the-fly-2740abd8f366?utm_source=chatgpt.com "Creating custom username and password lists on the fly!"))
* **Custom (CeWL-driven)**\
  Spider the target’s web assets to grab organization-specific words—great for intranet or bespoke apps. ([Medium](https://medium.com/%40tony-fu/penetration-testing-password-cracking-part2-generate-wordlist-fbc4b1844a64?utm_source=chatgpt.com "Password Cracking Part2 — Generate wordlist | by Tony Fu ..."))

## Password Wordlists

* **`/usr/share/wordlists/rockyou.txt`**\
  The go-to 1.7 M entry list on Kali—ideal for online brute-forcing against web forms or SSH. ([Reddit](https://www.reddit.com/r/oscp/comments/1apxuuf/best_oscp_wordlists/?utm_source=chatgpt.com "Best OSCP wordlists : r/oscp"), [therealunicornsecurity.github.io](https://therealunicornsecurity.github.io/OSCP/ "OSCP tips and tricks – Unicorn Security – Breaching Unicorns"))
* **`SecLists/Passwords/Leaked-Databases/10_million_password_list_top_1000000.txt`**\
  Real-world top 1 million passwords drawn from breaches. ([GitHub](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/10-million-password-list-top-10000.txt?utm_source=chatgpt.com "10-million-password-list-top-10000.txt"))
* **`SecLists/Passwords/Common-Credentials/10k-most-common.txt`**\
  Curated “quick-win” top 10 000 list—start here for speed. ([GitHub](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/10k-most-common.txt?fbclid=IwAR0Eyfvtc3c2q-6_d7c002K3ojJv-8j89WEuJ9acelpMV6D26U5cxPQ3N7k&utm_source=chatgpt.com "SecLists/Passwords/Common-Credentials/10k-most- ..."))
* **`SecLists/Passwords/Common-Credentials/default-passwords.txt`**\
  Default creds for routers, databases, web-apps (e.g. admin:admin, root:toor). ([GitHub](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/10k-most-common.txt?fbclid=IwAR0Eyfvtc3c2q-6_d7c002K3ojJv-8j89WEuJ9acelpMV6D26U5cxPQ3N7k&utm_source=chatgpt.com "SecLists/Passwords/Common-Credentials/10k-most- ..."))
* **CUPP (Common User Passwords Profiler)**\
  OSINT-based tool to build wordlists from personal data (pets, birthdays, etc.). ([Medium](https://medium.com/%40jakemcgreevy/creating-custom-username-and-password-lists-on-the-fly-2740abd8f366?utm_source=chatgpt.com "Creating custom username and password lists on the fly!"))
* **Custom (CeWL)**\
  Spider up to a set depth on the target host to extract unique terms for your wordlist. ([Medium](https://medium.com/%40tony-fu/penetration-testing-password-cracking-part2-generate-wordlist-fbc4b1844a64?utm_source=chatgpt.com "Password Cracking Part2 — Generate wordlist | by Tony Fu ..."))
* **Rule-based mutations**\
  Use Hashcat/John rule sets (e.g. d3adgood, rockyou-lek) to add l33t, case shifts, suffixes/pre-fixes.

## Quick Usage Tips

1. **Layer your attacks**

   * Start with small lists (top 10 k users + passwords) for 1–2 minutes.
   * If nothing cracks, move to rockyou, then the 1 M list. ([Reddit](https://www.reddit.com/r/oscp/comments/1apxuuf/best_oscp_wordlists/?utm_source=chatgpt.com "Best OSCP wordlists : r/oscp"))
2. **Default creds first**

   * Always try `admin:admin`, `root:toor`, `username:username`, and service:service. ([GitHub](https://github.com/saisathvik1/OSCP-Cheatsheet?utm_source=chatgpt.com "OSCP Cheatsheet by Sai Sathvik"))
3. **Time-box online brute**

   * Limit to ~5–10 minutes per service to avoid lockouts. ([Reddit](https://www.reddit.com/r/oscp/comments/1apxuuf/best_oscp_wordlists/?utm_source=chatgpt.com "Best OSCP wordlists : r/oscp"))

- - -

# Windows SID Enumeration (Users)

```
impacket-lookupsid 'cicada.htb/guest'@cicada.htb -no-pass | grep 'SidTypeUser' |
sed 's/.*\\\(.*\) (SidTypeUser)/\1/' > users.txt
```



## W﻿indows Password Spraying(with a user wordlist)

```
crackmapexec smb cicada.htb -u users.txt -p ''
```

## E﻿numerating Domain Users (Using SMB)

```
crackmapexec smb <hostname/ipaddress> -u <username> -p '' --
users
```



## W﻿indows Remote Management (Evil-winrm)



```
evil-winrm -u <username> -p '' -i cicada.htb
```