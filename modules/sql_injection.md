![image](https://github.com/user-attachments/assets/0abfba20-93bd-4d3f-bde0-6274f14c5e70)

# SQL Injection

## Training Resources
---
### Courses
*Free*
- [PortSwigger Academy - SQLi](https://portswigger.net/web-security/sql-injection)
- [PortSwigger Academy - NoSQLi](https://portswigger.net/web-security/nosql-injection)

*Paid*
- [HTB - SQL Injection Fundamentals](https://academy.hackthebox.com/course/preview/sql-injection-fundamentals)
- [HTB - Blind SQL Injection](https://academy.hackthebox.com/course/preview/blind-sql-injection)
- [HTB - Advanced SQL Injections](https://academy.hackthebox.com/course/preview/advanced-sql-injections)
- [HTB - MSSQL, Exchange, and SCCM Attacks](https://academy.hackthebox.com/course/preview/mssql-exchange-and-sccm-attacks)
- [HTB - Introduction to NoSQL Injection](https://academy.hackthebox.com/course/preview/introduction-to-nosql-injection)
- [HTB - SQLMap Essentials](https://academy.hackthebox.com/course/preview/sqlmap-essentials)
- [THM - SQL Fundamentals](https://tryhackme.com/r/room/sqlfundamentals)
- [THM - SQL Injection](https://tryhackme.com/r/room/sqlinjectionlm)
- [THM - Advanced SQL Injection](https://tryhackme.com/r/room/advancedsqlinjection)
- [THM - SQLMap: The Basics](https://tryhackme.com/r/room/sqlmapthebasics)
- [THM - SQL Injection Lab](https://tryhackme.com/r/room/sqlilab)

#

### Hack The Box Machines
*These machines are tagged as containing SQL Injection by HTB, the difficulty refers to the box as a whole and not necessarily the SQL Injection element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| Writeup | Easy | |
| Whiskers | Easy | |
| Validation | Easy | |
| Trick | Easy | |
| Toolbox | Easy | |
| Better | Easy | |
| Stocker | Easy | |
| Soccer | Easy | |
| Shopper | Easy | |
| Rental | Easy | |
| Press2Inject | Easy | |
| PC | Easy | |
| Invalidated | Easy | |
| Pandora | Easy | |
| NodeBlog | Easy | |
| MetaTwo | Easy | |
| Library | Easy | |
| Jupiter | Medium | |
| Jarvis | Medium | |
| GoodGames | Medium | |
| Monitored | Medium | |
| Mango | Medium | |
| Magic | Medium | |
| Shared | Medium | |
| SecNotes | Medium | |
| Giddy | Medium | |
| Sneaky | Medium | |
| Gallery | Medium | |
| Faculty | Medium | |
| TechPot | Medium | |
| RedCross | Medium | |
| Socket | Medium | |
| Europa | Medium | |
| Enterprise | Medium | |
| Clicker | Medium | |
| Cache | Medium | |
| Book | Medium | |
| Unrested | Medium | |
| Unattended | Medium | |
| AI | Medium | |
| Zipping | Medium | |
| Altered | Hard | |
| Proper | Hard | |
| Charon | Hard | |
| Zeta | Hard | |
| Pheonix | Hard | |
| Spider | Hard | |
| Download | Hard | |
| Control | Hard | |
| EarlyAccess | Hard | |
| Formula | Hard | |
| Seventeed | Hard | |
| OverGraph | Hard | |
| Oz | Hard | |
| FluJab | Hard | |
| Watch | Hard | |
| Falafel | Hard | |
| Intentions | Hard | |
| Intense | Hard | |
| Holiday | Hard | |
| Monitors | Hard | |
| Nightmare | Insane | |
| Multimaster | Insane | |
| BankRobber | Insane | |
| Fatty | Insane | |
| Rabit | Insane | |

### Other Resources
---
**PT Guides**
- [HackTricks SQLi](https://book.hacktricks.xyz/pentesting-web/sql-injection)
- [Sushant OSCP Guide SQLi](https://sushant747.gitbooks.io/total-oscp-guide/content/sql-injections.html)
- [My Guide - SQLi](https://tom23rose.gitbook.io/testingmethodology/web-testing/exploitation/injection-attacks/sql-injection)
- [The Hacker Recipes - SQL Injection](https://www.thehacker.recipes/web/inputs/sqli#sql-injection)
#
**Bug Bounty Write Ups**
- [Collection of Write Ups](https://github.com/alexbieber/Bug_Bounty_writeups#sql-injectionsqli)
#
**Methodologies**
- [OWASP SQL Injection Methodology](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection)
#
**[Arsenal](https://github.com/Orange-Cyberdefense/arsenal/tree/master) Tool Cheatsheets**
- [Master Arsenal Cheatsheet - SQLMap](https://github.com/Orange-Cyberdefense/arsenal/blob/master/arsenal/data/cheats/SQL%20Injection/sqlmap.md)
- [Modified Arsenal Cheatsheet - SQL Injection](https://github.com/ThomasRose23/arsenal_cheatsheets/blob/main/webapp/sql-injection)
#
**Wordlists**
- [SecLists SQLi](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/SQLi)
#
**SQL Prevention**
- [OWASP SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
#


## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Identify inputs into the application, specifically target any area that looks like it could have interaction with a database, for example login forms, search boxes etc.
- Use automated tools like Wfuzz to help test potentially vulnerable parameters:
```bash
#fuzzing GET parameter
wfuzz -c -z file,/usr/share/wordlists/wfuzz/Injections/SQL.txt -u "http://site.com/index.php?id=FUZZ"
​
#fuzzing POST parameter
wfuzz -c -z file,/usr/share/wordlists/wfuzz/Injections/SQL.txt -d "id=FUZZ" -u "http://site.com/index.php"
```
- Use SQLMap - Spend time learning how SQLMap works, it is allowed in the exam and is extremelyt useful! I'd recommend exporting requests into txt files, marking vulnerable params with * and importing using -r as shown below:
```bash
# With exported request
sqlmap -r request_file.txt --dump

# Manual POST
sqlmap -u http://www.example.com/api --method POST --data "name=taco&sort=id&order=asc" -p "name,sort,order"

# Manual GET
sqlmap -u "http://www.example.com/vuln.php?id=1" --batch
```
- Burp Suite will attempt to discover SQL Injection vulnerabilities during an active scan.
- If discovered, understand the DB in question, read the docs and learn how to exploit this further. Can you get RCE by writing to files? 
