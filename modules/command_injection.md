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

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| Spark | Very Easy | |
| Prequel | Very Easy | |
| Enlightenment | Very Easy | |
| Bashed | Easy | |
| Wind | Easy | |
| Spectra | Easy | |
| TwoMillion | Easy | |
| Secret | Easy | |
| ScriptKiddie | Easy | |
| RouterSpace | Easy | |
| Referrals | Easy | |
| Optimum | Easy | |
| OpenAdmin | Easy | |
| Previse | Easy | |
| Photobomb | Easy | |
| Headless | Easy | |
| Haystack | Easy | |
| Sea | Easy | |
| Sau | Easy | |
| Liberty | Easy | |
| Flipper | Easy | |
| Click | Easy | |
| Networked | Easy | |
| WindHose | Medium | |
| Union | Medium | |
| Sewers | Medium | |
| RedCross | Medium | |
| Meta | Medium | |
| Mentor | Medium | |
| Jarvis | Medium | |
| Investigation | Medium | |
| Haircut | Medium | |
| FluxCapacitor | Medium | |
| Feldspar | Medium | |
| Extension | Medium | |
| EvilCUPS | Medium | |
| Europa | Medium | |
| Dynstr | Medium | |
| Droider | Medium | |
| Cronos | Medium | |
| Craft | Medium | |
| Carrier | Medium | |
| Catch | Medium | |
| Bastard | Medium | |
| Awkward | Medium | |
| AI | Medium | |
| Monitors | Hard | |
| Visor | Hard | |
| Admirer | Hard | |
| Charon | Hard | |
| EarlyAccess | Hard | |
| Cup | Hard | |
| Formula | Hard | |
| FormulaX | Hard | |
| Identifier | Hard | |
| Holiday | Hard | |
| Helpline | Hard | |
| Mailroom | Hard | |
| Phoenix | Hard | |
| Oouch | Hard | |
| Spooktrol | Hard | |
| Stacked | Insane | |
| Sekhmet | Insane | |
| Reddish | Insane | |
| Perspective | Insane | |
| Multimaster | Insane | |
| Mischief | Insane | |
| Hackback | Insane | |
| Fortune | Insane | |
| Smasher2 | Insane | |
| Fingerprint | Insane | |
| Derailed | Insane | |
| CrossFit | Insane | |
| Bankrobber | Insane | |
| Ariekei | Insane | |


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
- [SecLists - Command Injection Commix](https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/command-injection-commix.txt)
- [Quick Command Injection Check](https://github.com/ThomasRose23/Wordlists_and_Payloads/blob/main/Web_App/simple_command_injection)
- [Quick Blind Command Injection Check](https://github.com/ThomasRose23/Wordlists_and_Payloads/blob/main/Web_App/simple_blind_command_injection)
#
**Command Injection Prevention**
- [OWASP Command Injection Defence Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/OS_Command_Injection_Defense_Cheat_Sheet.html)
#


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
```bash
python commix.py --url="http://site.com/path/to/vuln/#" --data="id=1&Submit=submit" --cookie="PHPSESSID=nq30op434117mo7o2oe5bl7is4"
```
- Use other automated tools to discover Command Injection:
  - Wfuzz - filter out responses using -hc (response code) and -hh response size
```bash
# GET Request
wfuzz -c -z file,<path-to-wordlist> -u "http://site.com/index.php?id=FUZZ"

# POST Request

wfuzz -c -z file,<path-to-wordlist> -u "http://site.com/index.php" -d "id=FUZZ"
```
