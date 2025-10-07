# High-level summary

JSON Web Tokens (JWTs) are used to carry authentication data between clients and servers. If the server accepts tokens without proper verification (bad algorithms, weak keys, or trusting remote keys) an attacker can forge tokens to escalate privileges or impersonate other users. These labs show three common JWT pitfalls and safe, beginner-friendly ways to test them.

## Lab 1 — JWT authentication bypass via flawed signature verification (alg=none)

**What this teaches:** How an application that accepts `alg: none` allows attackers to bypass signature checks and impersonate other users.**

**Simple beginner walkthrough:**

1. Log in to the lab and find the post-login request that contains your session JWT (look in Proxy > HTTP history) and send it to Repeater.
2. In the JWT editor/Inspector, change the payload claim `sub` to `administrator` and apply the change.
3. In the JWT header change `alg` to `none` and remove the signature portion of the token (leave the trailing dot after the payload).
4. Send the modified request to `/admin`. If accepted, you will see the admin panel — navigate to `/admin/delete?username=carlos` to finish the lab.

![image alt](https://github.com/Lispectree/web-sec/blob/9b4cd9d306f70e772a64f1333d5a6d90d8cd2e87/web-security-labs/labs/jwt/JWT%20LAB1%20PHOTO1.jpg)
Request that contains JWT are highlighted


![image alt](https://github.com/Lispectree/web-sec/blob/546e0fec425116122fe0b9a416064ad1eea107ba/web-security-labs/labs/jwt/JWT%20LAB1%20PHOTO2.jpg)
The payload section of the JWT shows the sub field
Edit it to admin to access the admin page


![image alt](
## Lab 2 — JWT authentication bypass via weak signing key

**What this teaches:** **How weak or guessable signing keys can be brute-forced to create valid tokens.**

**Simple beginner walkthrough:**

1. Log in and capture your session JWT from the post-login request. Send that request to Repeater so you can work with the token.
2. Use a JWT cracking tool or hashcat with a wordlist of likely secrets to brute-force the token’s signing key (for example: `hashcat -a 0 -m 16500 <YOUR-JWT> /path/to/jwt.secrets.list`).
3. When the secret is found (e.g., `secret1`), use it to sign a new token whose `sub` claim is `administrator` (the JWT Editor extension can help), then resend the request to `/admin`.
4. If the admin panel opens, go to `/admin/delete?username=carlos` to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* web-security-labs/labs/jwt/images/jwt_weak_key_bruteforce_step1.png
* web-security-labs/labs/jwt/images/jwt_weak_key_bruteforce_step2.png
* web-security-labs/labs/jwt/images/jwt_weak_key_bruteforce_step3.png


## Lab 3 — JWT authentication bypass via JKU header injection

**What this teaches:** **How trusting a remote JWK Set (via the `jku` header) can let an attacker upload their public key and forge valid tokens.**

**Simple beginner walkthrough:**

1. Generate a fresh RSA key pair (the JWT Editor in Burp can generate one). Copy the public key as a JWK and host it in a JWK Set JSON file on your exploit server (body should be `{"keys":[ <your JWK> ]}`).
2. Capture the post-login JWT request and open it in the JWT editor. Change the token header to set `kid` to the JWK’s `kid`, and add a `jku` parameter pointing to your hosted JWK Set URL.
3. In the JWT payload change `sub` to `administrator`. Use your private RSA key to sign the token (use the JWT editor’s Sign feature), then send the request to `/admin`.
4. If successful you’ll see the admin panel — visit `/admin/delete?username=carlos` to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* web-security-labs/labs/jwt/images/jwt_jku_injection_step1.png
* web-security-labs/labs/jwt/images/jwt_jku_injection_step2.png
* web-security-labs/labs/jwt/images/jwt_jku_injection_step3.png
