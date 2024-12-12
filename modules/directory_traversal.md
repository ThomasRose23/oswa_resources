![image](https://github.com/user-attachments/assets/9ca23281-ecee-452f-86de-79fff53cd728)

# Directory Traversal

### Training Resources
---

**Courses**

*Free*
- [PortSwigger Academy - Path Traversal](https://portswigger.net/web-security/file-path-traversal)

*Paid*
- [HTB - File Inlusion](https://academy.hackthebox.com/course/preview/file-inclusion)
- [THM - File Inclusion](https://tryhackme.com/r/room/fileinc)
- [THM - File Inclusion, Path Traversal](https://tryhackme.com/r/room/filepathtraversal)

#

#### HTB Machines
*These machines are tagged as containing Directory Traversal by HTB, the difficulty refers to the box as a whole and not necessarily the Directory Traversal element.*

| Machine Name | Difficulty | Verified Directory Traversal | WriteUp | Comments |
| -- | -- | -- | -- | -- |
| Writer | Medium | No | | LFI |
| Zipping | Medium | No | | LFI |
| Waldo | Medium | No | | Directory Traversal |
| UpDown | Medium | No | | LFI |
| Unicode | Medium | No | | LFI |
| Unattended | Medium | No | | LFI / Diretory Traversal |
| Trick | Easy | No | | LFI |
| Topology | Easy | No | | LFI / Diretory Traversal |
| Timing | Medium | No | | LFI |
| TartarSauce | Medium | No | | RFI |
| Tabby | Easy | No | | LFI |
| StreamIO | Medium | No | | LFI / RFI |
| Stocker | Easy | No | | Directory Traversal |
| Spooktrol | Hard | No | | Directory Traversal |
| Snoopy | Hard | No | | LFI |
| Sniper | Medium | No | | LFI / RFI |
| Smasher | Insane | No | | LFI |
| Seventeen | Hard | No | | LFI |
| ServMon | Easy | No | | LFI  |
| Response | Insane | No | | LFI |
| Resource | Medium | No | | LFI |
| Repetitive | Easy | No | | Diretory Traversal |
| Reel2 | Hard | No | | Diretory Traversal |
| RE | Hard | No | | Diretory Traversal |
| Proper | Hard | No | | RFI |
| Pollution | Hard | No | | LFI |
| Poison | Medium | No | | LFI |
| Player | Hard | No | | LFI |
| Pilgrimage | Easy | No | | LFI |
| PikaTwoo | Insane | No | | LFI |
| Pikaboo | Hard | No | | LFI |
| Patents | Hard | No | | LFI |
| Paper | Easy | No | | Directory Traversal |
| OverGraph | Hard | No | | LFI |
| OpenSource | Easy | No | | Directory Traversal |
| OpenAdmin | Easy | No | | LFI / Directory Traversal |
| OnlyForYou | Medium | No | | LFI |
| Nineveh | Medium | No | | LFI |
| Monitors | Hard | No | | LFI |
| Moderators | Hard | No | | LFI |
| Mailing | Easy | No | | DIrectory Traversal |
| Llama | Easy | No | | LFI |
| LaCasaDePapel | Easy | No | | LFI |
| Laboratory | Easy | No | | Directory Traversal |
| Intuition | Hard | No | | LFI |
| Inject | Easy | No | | LFI |
| Haystack | Easy | No | | LFI |
| GreenHorn | Easy | No | | RFI |
| Ghoul | Hard | No | | Directory Traversal |
| GetLab | Very Easy | No | | Directory Traversal |
| Gem | Easy | No | | LFI |
| FriendZone | Easy | No | | LFI |
| ForwardSlash | Hard | No | | LFI / Directory Traversal |
| FormulaX | Hard | No | | LFI |
| Format | Medium | No | | LFI |
| Flight | Hard | No | | RFI |
| Fingerprint | Insane | No | | LFI / Directory Traversal |
| Fatty | Insane | No | | Directory Traversal |
| Faculty | Medium | No | | LFI |
| Encoding | Medium | No | | LFI |
| EarlyAccess | Hard | No | | Directory Traversal |
| Download | Hard | No | | LFI |
| Devzat | Medium | No | | LFI |
| DevOps | Medium | No | | LFI |
| Cybermonday | Hard | No | | LFI |
| CrimeStoppers | Medium | No | | LFI |
| Clicker | Hard | No | | Directory Traversal |
| Cerberus | Medium | No | | LFI |
| BroScience | Hard | No | | LFI |
| Breadcrumbs | Insane | No | | Directory Traversal |
| Bookworm | Easy | No | | LFI |
| Blunder | Insane | No | | Directory Traversal |
| BigHead | Easy | No | | LFI |
| Beep | Medium | No | | LFI |
| Bagel | Easy | No | | LFI |
| Backdoor | Easy | No | | Directory Traversal |
| Awkward | Medium | No | | LFI |
| Archive | Easy | No | | Directory Traversal |
| Ambassador | Medium | No | | Directory Traversal |

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
