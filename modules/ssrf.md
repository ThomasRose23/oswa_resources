![image](https://github.com/user-attachments/assets/4c4b170c-1e53-4855-9e2a-27de8c00afb3)

# Server-Side Request Forgery (SSRF)

## Training Resources
---

**Courses**

*Free*
- [PortSwigger Academy - SSRF](https://portswigger.net/web-security/ssrf)

*Paid*
- [HTB - Server-Side Attacks](https://academy.hackthebox.com/course/preview/server-side-attacks)
- [THM - Intro to SSRF](https://tryhackme.com/r/room/ssrfqi)
- [THM - SSRF](https://tryhackme.com/r/room/ssrfhr)

#

### Hack The Box Machines
*These machines are tagged as containing Server-Side Request Forgery by HTB, the difficulty refers to the box as a whole and not necessarily the Server-Side Request Forgery element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| LogonShell | Very Easy | |
| Sau | Easy | |
| Editorial | Easy | |
| CloudFall | Easy | |
| Love | Easy | |
| Ready | Medium | |
| OnlyForYou | Medium | |
| Health | Medium | |
| Awkward | Medium | |
| Forge | Medium | |
| Factory | Medium | |
| Writer | Medium | |
| Slashed | Medium | |
| Sewers | Medium | |
| Travel | Hard | |
| OverGraph | Hard | |
| Mailroom | Hard | |
| Kotarak | Hard | |
| Jarmis | Hard | |
| Identifier | Hard | |
| Gofer | Hard | |
| FordwardSlash | Hard | |
| Cereal | Hard | |
| Appsanity | Hard | |
| AdmirerToo | Hard | |
| Response | Insane | |
| Perspective | Insane | |
| Kryptos | Insane | |
| Laser | Insane | |

### Other Resources
---
**PT Guides**
- [The Hacker Recipes - Server-Side Request Forgery](https://www.thehacker.recipes/web/inputs/ssrf/#ssrf-server-side-request-forgery)
- [HackTricks - SSRF](https://book.hacktricks.wiki/en/pentesting-web/ssrf-server-side-request-forgery/index.html#ssrf-server-side-request-forgery)
#
**Bug Bounty Write Ups**
- [Collection of Write Ups](https://github.com/alexbieber/Bug_Bounty_writeups#sql-injectionsqli)
#
**Methodologies**
- [OWASP Methodology - Server-Side Request Forgery](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/19-Testing_for_Server-Side_Request_Forgery)
#
**Server-Side Request Forgert Prevention**
- [OWASP Server-Side Request Forgery Prevention Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)
#

## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Applications are vulnerable to SSRF when they process user-supplied input and generate a request to a resource based on that input, essentially using the application as a proxy.
- Look for suggestive parameters such as URLs, URIs, links etc. 
  - URLs used in parameters
  - URLs in hidden form fields
  - A partial URL, eg. a URL parameter requesting a subdomain by just the subdomain name. ?sub=api requests api.site.com. 
  - A file path included somewhere eg. URL.
- Once identified, try to connect back to a web server on an attack machine
- Try to access files internal on the target machine using non-http protocols such as file:///etc/passwd
-  Can you get the server to perform actions using POST requests, consider researching and using Gopher for this, example basic Gopher payload:
  ```bash
curl gopher://127.0.0.1:80/_POST%20/status%20HTTP/1.1%0a
```
- If on cloud, can you access the instance metadata for the cloud environment. 
  - Amazon: 169.254.169.254
  - Google: metadata.google.internal
