# High-level summary

DOM-based vulnerabilities happen when a page's own JavaScript uses untrusted input (from messages, cookies, the URL, etc.) in a dangerous way. An attacker can feed data to that script and make the victim's browser run malicious code. These labs show common DOM risks like postMessage handling, JavaScript: URLs in sinks, and cookie poisoning — explained in plain language so beginners can follow.

## Lab 1 — DOM XSS using web messages

**What this teaches:** How a page that listens for `postMessage()` can be tricked into inserting attacker-controlled HTML, causing code execution.

**Simple beginner walkthrough:**

1. Notice the homepage listens for web messages (it uses `addEventListener` for `message`).
2. On the exploit server, create a page that embeds the lab homepage in an iframe and posts a message when the iframe loads. Use your lab ID in the iframe `src`.
3. Make the posted message contain an HTML payload such as `<img src=1 onerror=print()>`, then store and deliver the exploit to the victim.
4. When the victim opens the exploit, the home page receives the message, inserts the HTML into the page, and the onerror handler runs.
5. Confirm the payload executed (for example an alert) to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* dom_based_webmessage_step1.png
* dom_based_webmessage_step2.png
* dom_based_webmessage_step3.png


## Lab 2 — DOM XSS using web messages and a JavaScript URL

**What this teaches:** How weak checks for URL-like strings can be fooled into executing a `javascript:` payload via `location.href`.

**Simple beginner walkthrough:**

1. Observe the homepage listens for web messages and checks messages for the strings `http:` or `https:` before using them with `location.href`.
2. On the exploit server, make a page that iframes the lab and posts a message like `javascript:print()//http:` when the iframe loads (replace with your lab ID).
3. Store and deliver the exploit to the victim.
4. When the victim opens it, the listener sees `http:` and forwards the whole string to `location.href`, causing the `javascript:` code to run.
5. Confirm the payload executed to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* dom_based_webmessage_jsurl_step1.png
* dom_based_webmessage_jsurl_step2.png
* dom_based_webmessage_jsurl_step3.png


## Lab 3 — DOM-based cookie manipulation

**What this teaches:** How an attacker can poison a client-side cookie so the site later loads a malicious URL from that cookie.

**Simple beginner walkthrough:**

1. Note the site stores the last viewed product URL in a client cookie called `lastViewedProduct`.
2. On the exploit server, create an iframe that first loads a product URL with a small JavaScript payload appended, then immediately redirects to the homepage (use your lab ID in the iframe `src`).
3. Store and deliver the exploit to the victim; the browser will save the malicious URL to the cookie and then go back to the homepage.
4. While the poisoned cookie is present, loading the homepage causes the site to use the cookie value and execute the injected payload.
5. Confirm the payload execution to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* dom_based_cookie_poison_step1.png
* dom_based_cookie_poison_step2.png
* dom_based_cookie_poison_step3.png


## Lab 4 — Exploiting DOM clobbering to enable XSS

**What this teaches:** How creating HTML elements with certain IDs/names can overwrite JavaScript variables (DOM clobbering) and enable XSS.

**Simple beginner walkthrough:**

1. Go to a blog post and add a comment containing two anchor tags like:
   `<a id=defaultAvatar></a><a id=defaultAvatar name=avatar href="cid:&quot;onerror=alert(1)//"></a>`
2. Post a second comment with any text and reload the blog page.
3. The page’s JavaScript uses a global `defaultAvatar` object; by creating anchors with that ID/name you clobber the object so `defaultAvatar.avatar` contains your payload.
4. When the comments are loaded, the site uses the clobbered value and the `onerror` handler runs, triggering the alert.
5. Confirm the alert appears to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* dom_based_clobbering_step1.png
* dom_based_clobbering_step2.png
* dom_based_clobbering_step3.png

