# High-level summary

Access control vulnerabilities happen when an application does not properly enforce who can do what. This can let users view or change data, perform actions, or access pages they shouldn't. Understanding these issues helps ensure users only get the permissions they are supposed to have.

## Lab 1 — Unprotected Admin Panel

**What this teaches:** How hidden URLs can still allow unauthorized access.

**Simple beginner walkthrough:**

1. View the lab home page source in your browser or Burp.
2. Look for JavaScript that shows the admin panel URL.
3. Open the admin panel and complete the lab task.

![image alt](https://github.com/Lispectree/web-sec/blob/2d310a0d12df3a7dedef56bac4112695d1ba2eab/web-security-labs/labs/access-control/image%201%20lab%201%20access%20control.jpg)
This shows that the admin subdomain isn’t found



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



