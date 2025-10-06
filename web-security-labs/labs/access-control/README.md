# High-level summary

Access control vulnerabilities happen when an application does not properly enforce who can do what. This can let users view or change data, perform actions, or access pages they shouldn't. Understanding these issues helps ensure users only get the permissions they are supposed to have.

## Lab 1 — Unprotected Admin Panel

**What this teaches:** How hidden URLs can still allow unauthorized access.

**Simple beginner walkthrough:**

1. View the lab home page source in your browser or Burp.
2. Look for JavaScript that shows the admin panel URL.
3. Open the admin panel and complete the lab task.

   ![image alt](https://github.com/Lispectree/web-sec/blob/8dc05cf749b36defe855a82cd955375c129dd404/labs/sql-injection/access%20control%20lab1%20photo%201.jpg)
This shows that the admin subdomain isn’t found

![image alt](https://github.com/Lispectree/web-sec/blob/120bbc6a0faf6eb4d872b44978d8007ddf56a8c0/labs/sql-injection/access%20control%20lab1%20photo%202.jpg)
/robots.txt shows hidden subdomains

![image alt](https://github.com/Lispectree/web-sec/blob/5226e16c869b8109f5f226568b53f2eb2428aab6/labs/sql-injection/access%20control%20lab1%20photo%203.jpg)
Delete that user that was instructed by the lab

## Lab 2 — User Role Modification

**What this teaches:** How modifying profile data can escalate privileges.

**Simple beginner walkthrough:**

1. Log in and go to your account page.
2. Update your email and observe your role ID in the response.
3. Send the request to Burp Repeater and change the roleid to 2.
4. Forward the request and confirm your new role.
5. Access /admin and complete the lab task.

*Images (placeholders — add 2–3 screenshots):*

* access\_control\_role\_mod\_step1.png
* access\_control\_role\_mod\_step2.png
* access\_control\_role\_mod\_step3.png


## Lab 3 — URL-based Access Control Bypass

**What this teaches (one line):** How modifying request headers can bypass front-end restrictions.

**Simple beginner walkthrough:**

1. Try loading /admin and notice you are blocked.
2. Send the request to Burp Repeater, change URL to /, and add X-Original-URL: /invalid.
3. Change the header to /admin and forward the request.
4. Use ?username=carlos in the query string with X-Original-URL: /admin/delete to complete the task.

*Images (placeholders — add 2–3 screenshots):*

* access\_control\_url\_bypass\_step1.png
* access\_control\_url\_bypass\_step2.png
* access\_control\_url\_bypass\_step3.png


## Lab 4 — Referer-based Access Control

**What this teaches:** How access rules based on the Referer header can be bypassed.

**Simple beginner walkthrough:**

1. Log in as admin and perform an action on carlos, sending the request to Burp Repeater.
2. Open an incognito window, log in as a non-admin, and try the same request.
3. Copy the non-admin session cookie into Burp, adjust the username to yours, and forward the request.
4. Complete the lab task.

*Images (placeholders — add 2–3 screenshots):*

* access\_control\_referer\_step1.png
* access\_control\_referer\_step2.png
* access\_control\_referer\_step3.png



