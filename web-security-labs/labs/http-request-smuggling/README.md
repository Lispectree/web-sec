# High-level summary

HTTP request smuggling exploits differences in how front-end and back-end servers parse HTTP requests (for example, via conflicting Content-Length and Transfer-Encoding headers). An attacker can insert a partial request that the back-end treats differently, allowing them to hijack the next request on the same connection — for example to access admin pages or trigger backend actions. Think of it as sneaking an extra message into a conversation the other side will read.

## Lab 1 — Confirming a CL.TE desync (CL.TE confirm)

**What this teaches :** **How to confirm a Content-Length / Transfer-Encoding (CL.TE) desync by observing differential responses.**

**Simple beginner walkthrough:**

1. Send a crafted POST request with `Content-Length` set and `Transfer-Encoding: chunked` that finishes the chunked body immediately (a `0` chunk).
2. Append a second request after the body (for example `GET /404 ...`) in the same TCP stream and send it.
3. Watch the server responses — if the front-end and back-end disagree, every second request may receive a different status (e.g., 404), confirming a CL.TE desync.
4. Use this confirmation as a starting point for further smuggling experiments against the lab.

*Images (placeholders — add 2–3 screenshots):*

* web-http-request-smuggling_clte_confirm_step1.png
* web-http-request-smuggling_clte_confirm_step2.png
* web-http-request-smuggling_clte_confirm_step3.png
  
## Lab 2 — Confirming a TE.CL desync (TE.CL confirm)

**What this teaches:** **How to confirm a Transfer-Encoding / Content-Length (TE.CL) desync by differential responses.**

**Simple beginner walkthrough:**

1. Build a request that sends `Transfer-Encoding: chunked` while also including a `Content-Length` header with a small value (mismatched values).
2. Include a second request after the chunked data that the back-end will interpret differently (for example `POST /404 ...` followed by a small real body and a terminating `0` chunk).
3. Send the request and observe the responses — if some responses show the injected `POST /404` was processed, you’ve confirmed a TE.CL desync.
4. Use this finding to craft smuggled payloads that the back-end will treat as separate requests.

*Images (placeholders — add 2–3 screenshots):*

* web-http-request-smuggling_tecl_confirm_step1.png
* web-http-request-smuggling_tecl_confirm_step2.png
* web-http-request-smuggling_tecl_confirm_step3.png


## Lab 3 — HTTP/2 CL request smuggling (H2.CL)

**What this teaches:** **How to smuggle an HTTP/1.1 request prefix over HTTP/2 by using `Content-Length: 0` and cause backend redirects to attacker-controlled hosts.**

**Simple beginner walkthrough:**

1. In Burp Repeater, make sure the protocol is set to HTTP/2. Send a POST with `Content-Length: 0` and a short literal payload (e.g. `SMUGGLED`). Observe that alternating requests get different behavior, confirming a prefix is being appended.
2. Craft a POST that smuggles the start of a GET request for `/resources`, including a fake `Host: foo` header in the smuggled prefix.
3. Host a malicious resource at your exploit server under `/resources` (for example a JS file with `alert(document.cookie)`).
4. Repeat the smuggling POST with the smuggled prefix pointing at your exploit server as `Host`. When timed correctly, victims will be redirected to your server and fetch the malicious resource — check your exploit server access log to confirm.

*Images (placeholders — add 2–3 screenshots):*

* web-http-request-smuggling_h2cl_step1.png
* web-http-request-smuggling_h2cl_step2.png
* web-http-request-smuggling_h2cl_step3.png


## Lab 4 — CL.0 request smuggling (CL.0 exploit)

**What this teaches (one line):** **How to trigger a CL.0 desync by smuggling a GET-prefixed request in the body and leverage it to access admin endpoints.**

**Simple beginner walkthrough:**

1. From Proxy > HTTP history send two GET / requests to Repeater and add both tabs to a new tab group.
2. Convert the first tab into a POST and place a smuggled prefix in its body that starts with a `GET /something` line (for example `GET /hopefully404 HTTP/1.1`). Set `Connection: keep-alive` on the first request and change the group send mode to "Send group in sequence (single connection)".
3. Send the sequence. If the second request's response matches what the smuggled prefix predicted (e.g., a 404), the back-end ignored the Content-Length and the CL.0 desync is confirmed.
4. Replace the smuggled prefix with `GET /admin` or `GET /admin/delete?username=carlos` and repeat the sequence to cause the backend to process your smuggled admin request. Confirm Carlos is deleted to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* web-http-request-smuggling_cl0_step1.png
* web-http-request-smuggling_cl0_step2.png
* web-http-request-smuggling_cl0_step3.png
