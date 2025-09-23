# High-level summary

XML External Entity (XXE) vulnerabilities occur when an application parses XML input that contains references to external resources. Attackers can exploit XXE to read sensitive files, interact with internal systems, or perform SSRF attacks. Understanding XXE helps developers safely handle XML input and disable unsafe entity processing.

## Lab 1 — Exploiting XXE Using External Entities to Retrieve Files

**What this teaches:** How XXE can be used to read local files on the server.

**Simple beginner walkthrough:**

1. Visit a product page, click "Check stock," and intercept the POST request in Burp.
2. Insert an external entity definition referencing /etc/passwd before the stockCheck element.
3. Replace the productId with \&xxe; and forward the request.
4. Observe the response containing the /etc/passwd contents.

*Images (placeholders — add 2–3 screenshots):*

* xxe\_localfile\_step1.png
* xxe\_localfile\_step2.png
* xxe\_localfile\_step3.png


## Lab 2 — Exploiting XXE to Perform SSRF Attacks

**What this teaches:** How XXE can trigger server-side requests to internal services.

**Simple beginner walkthrough:**

1. Visit a product page, click "Check stock," and intercept the POST request.
2. Insert an external entity referencing [http://169.254.169.254/](http://169.254.169.254/).
3. Replace the productId with \&xxe; and forward.
4. Iteratively update the URL to reach /latest/meta-data/iam/security-credentials/admin.
5. Observe the JSON response containing the SecretAccessKey.

*Images (placeholders — add 2–3 screenshots):*

* xxe\_ssrf\_step1.png
* xxe\_ssrf\_step2.png
* xxe\_ssrf\_step3.png


## Lab 3 — Exploiting Blind XXE via Error Messages

**What this teaches:** How to use a malicious DTD to exfiltrate data when the response doesn’t directly show it.

**Simple beginner walkthrough:**

1. Save the provided malicious DTD on your exploit server.
2. Visit a product page, click "Check stock," and intercept the POST request.
3. Insert an external entity referencing your malicious DTD.
4. Forward the request and observe the error message revealing /etc/passwd contents.

*Images (placeholders — add 2–3 screenshots):*

* xxe\_blind\_step1.png
* xxe\_blind\_step2.png
* xxe\_blind\_step3.png

## Lab 4 — Exploiting XInclude to Retrieve Files

**What this teaches:** How XInclude features in XML can be abused to read local files.

**Simple beginner walkthrough:**

1. Visit a product page, click "Check stock," and intercept the POST request.
2. Set productId to use an XInclude element pointing to file:///etc/passwd.
3. Forward the request.
4. Observe that the server returns the contents of /etc/passwd.

* xxe\_xinclude\_step1.png
* xxe\_xinclude\_step2.png
* xxe\_xinclude\_step3.png

