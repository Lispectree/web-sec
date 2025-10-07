# High-level summary

File upload vulnerabilities occur when an application allows users to upload files without proper security checks. Attackers can exploit this to upload scripts or other malicious files, potentially executing code on the server. Learning about these flaws helps developers secure file upload features and prevent unauthorized access.

## Lab 1 — Remote Code Execution via Web Shell Upload

**What this teaches:** How uploading a PHP file can let you execute commands on the server.

**Simple beginner walkthrough:**

1. Log in and upload any image as your avatar.
2. In Burp, find the GET request for your avatar and send it to Repeater.
3. Create a file called exploit.php with a simple script to read Carlos's secret.
4. Upload this PHP file as your avatar.
5. Use Burp Repeater to GET the PHP file and observe that the server executes it. Submit the secret to complete the lab.

![image alt](

## Lab 2 — Web Shell Upload via Path Traversal

**What this teaches:** How directory traversal in filenames can let scripts be placed outside the normal folder.

**Simple beginner walkthrough:**

1. Upload any avatar image and locate the GET request in Burp Repeater.
2. Create exploit.php to read Carlos's secret.
3. Modify the POST request filename to "../exploit.php" and forward it.
4. URL-encode the traversal sequence (..%2f) and forward the request again.
5. GET the file in the browser and submit the secret.

*Images (placeholders — add 2–3 screenshots):*

* file\_upload\_path\_traversal\_step1.png
* file\_upload\_path\_traversal\_step2.png
* file\_upload\_path\_traversal\_step3.png


## Lab 3 — Web Shell Upload via Extension Blacklist Bypass

**What this teaches:** How server checks on file extensions can be bypassed with a crafted .htaccess file.

**Simple beginner walkthrough:**

1. Upload any avatar image and find the GET request in Burp.
2. Create exploit.php to read Carlos's secret.
3. Upload a .htaccess file mapping .l33t to PHP.
4. Rename exploit.php to exploit.l33t and upload it.
5. GET exploit.l33t in Burp Repeater to read the secret and submit it.

*Images (placeholders — add 2–3 screenshots):*

* file\_upload\_extension\_bypass\_step1.png
* file\_upload\_extension\_bypass\_step2.png
* file\_upload\_extension\_bypass\_step3.png



## Lab 4 — Web Shell Upload via Obfuscated File Extension

**What this teaches:** How null bytes or hidden characters in filenames can bypass file type restrictions.

**Simple beginner walkthrough:**

1. Upload any avatar image and locate the GET request in Burp Repeater.
2. Create exploit.php to read Carlos's secret.
3. Modify the filename in the POST request to exploit.php%00.jpg and forward it.
4. GET exploit.php in Repeater and observe the secret.
5. Submit the secret to finish the lab.

*Images (placeholders — add 2–3 screenshots):*

* file\_upload\_obfuscation\_step1.png
* file\_upload\_obfuscation\_step2.png
* file\_upload\_obfuscation\_step3.png

