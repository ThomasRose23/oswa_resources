![image](https://github.com/user-attachments/assets/8baebb77-9b9e-4876-9547-a20fb8efa7b8)

# Command Injection

## Training Resources
---

### Courses

*Free*
- [PortSwigger Academy - Command Injection](https://portswigger.net/web-security/os-command-injection)

*Paid*
- [HTB - Whitebox Pentesting 101: Command Injection](https://academy.hackthebox.com/course/preview/whitebox-pentesting-101-command-injection)
- [HTB - Command Injection](https://academy.hackthebox.com/course/preview/command-injections)
- [THM - Command Injection](https://tryhackme.com/r/room/oscommandinjection)

#

### HTB Machines
*These machines are tagged as containing Template Injection by HTB, the difficulty refers to the box as a whole and not necessarily the Template Injection element.*

| Machine Name | Difficulty | Verified Directory Traversal | WriteUp | Comments |
| -- | -- | -- | -- | -- |
| Spark | Very Easy | Yes | [My Write Up](https://github.com/ThomasRose23/htb_writeups/blob/main/boxes/spark.md) | There are public exploits and a Metasploit module for this one, but if done manually is good Command Injection practice.  |
| Prequel | Very Easy | Yes | No Write Up | Does not contain manual command injection, involves basic SQL, FTP and password cracking knowledge. |
| Enlightenment | Very Easy | No | | |
| Bashed | Easy | No | | |
| Wind | Easy | No | | |
| Spectra | Easy | No | | |
| TwoMillion | Easy | No | | |
| Secret | Easy | No | | |
| ScriptKiddie | Easy | No | | |
| RouterSpace | Easy | No | | |
| Referrals | Easy | No | | |
| Optimum | Easy | No | | |
| OpenAdmin | Easy | No | | |
| Previse | Easy | No | | |
| Photobomb | Easy | No | | |
| Headless | Easy | No | | |
| Haystack | Easy | No | | |
| Sea | Easy | No | | |
| Sau | Easy | No | | |
| Liberty | Easy | No | | |
| Flipper | Easy | No | | |
| Click | Easy | No | | |
| Networked | Easy | No | | |
| WindHose | Medium | No | | |
| Union | Medium | No | | |
| Sewers | Medium | No | | |
| RedCross | Medium | No | | |
| Meta | Medium | No | | |
| Mentor | Medium | No | | |
| Jarvis | Medium | No | | |
| Investigation | Medium | No | | |
| Haircut | Medium | No | | |
| FluxCapacitor | Medium | No | | |
| Feldspar | Medium | No | | |
| Extension | Medium | No | | |
| EvilCUPS | Medium | No | | |
| Europa | Medium | No | | |
| Dynstr | Medium | No | | |
| Droider | Medium | No | | |
| Cronos | Medium | No | | |
| Craft | Medium | No | | |
| Carrier | Medium | No | | |
| Catch | Medium | No | | |
| Bastard | Medium | No | | |
| Awkward | Medium | No | | |
| AI | Medium | No | | |
| Monitors | Hard | No | | |
| Visor | Hard | No | | |
| Admirer | Hard | No | | |
| Charon | Hard | No | | |
| EarlyAccess | Hard | No | | |
| Cup | Hard | No | | |
| Formula | Hard | No | | |
| FormulaX | Hard | No | | |
| Identifier | Hard | No | | |
| Holiday | Hard | No | | |
| Helpline | Hard | No | | |
| Mailroom | Hard | No | | |
| Phoenix | Hard | No | | |
| Oouch | Hard | No | | |
| Spooktrol | Hard | No | | |
| Stacked | Insane | No | | |
| Sekhmet | Insane | No | | |
| Reddish | Insane | No | | |
| Perspective | Insane | No | | |
| Multimaster | Insane | No | | |
| Mischief | Insane | No | | |
| Hackback | Insane | No | | |
| Fortune | Insane | No | | |
| Smasher2 | Insane | No | | |
| Fingerprint | Insane | No | | |
| Derailed | Insane | No | | |
| CrossFit | Insane | No | | |
| Bankrobber | Insane | No | | |
| Ariekei | Insane | No | | |


### Other Resources
---
**PT Guides**
- [HackTrciks - Command Injection](https://book.hacktricks.wiki/en/pentesting-web/command-injection.html)
#
**Methodologies**
- [OWASP Methodology - Command Injection](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/12-Testing_for_Command_Injection)
#
**[Arsenal](https://github.com/Orange-Cyberdefense/arsenal/tree/master) Tool Cheatsheets**
- 
#
**Wordlists**
- 
#
**Command Injection Prevention**
- [OWASP Command Injection Defence Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/OS_Command_Injection_Defense_Cheat_Sheet.html)
#
**Other**
- 


## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Understand the OS you're attacking.
- Identify inputs into the application accepting alphanumeric characters. Look for functionality that could interact with the OS and likely to be suceptible to command injection, such as:
  - Converting media files
  - File archiving
  - Making backups
  - Anything using non-web protocols
- Determine if we can view the response to any injection attempt, if not test for blind command injection  
- Manually test by entering payloads into potentially vulnerable fields, observe the responses closely for clues of Command Injection. 
  - Try delimeters (|| && ; \n) and see if there are errors produced. Can you chain additional commands after the delimeter and observe the output. 
  - Try blind injection payloads such as
```bash
;time+20;
;curl+http://ip:port/path;
```
- Commix is a tool than can automate the finding of Command Injection vulnerabilities, very similar to SQLMap and easy to use. Basic usage can be seen below but read the docs for more control.
- Use other automated tools to discover Command Injection:
