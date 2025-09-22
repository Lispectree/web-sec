# Path Traversal — Simple Walkthroughs

**High-level summary of Path Traversal**

Path Traversal happens when a website lets you request files by name (for example, images). If the site doesn’t carefully check the filename you give it, you can ask for files outside the intended folder — including sensitive system files. Attackers use special filename text (like `../`) to move up the folder structure and read files the server shouldn’t reveal.

---

## Lab 1 — File path traversal (simple case)

**What this teaches (one line):**
How a basic `../` sequence in a filename can let you read files outside the intended folder.

**Simple beginner walkthrough:**

1. Use Burp Suite to capture the request that fetches a product image.
2. Edit the filename parameter to: `../../../etc/passwd`.
3. Send the modified request and check the response — if it contains `/etc/passwd` contents, the server returned a file it shouldn't.

**Images (placeholders — add 2–3 screenshots):**

* `images/path_traversal_simple_step1.png`
* `images/path_traversal_simple_step2.png`
* `images/path_traversal_simple_step3.png`


---

## Lab 2 — Traversal sequences stripped non-recursively

**What this teaches (one line):**
How naive filters that look for exact `../` sequences can be bypassed by slightly altered patterns.

**Simple beginner walkthrough:**

1. Capture the product image request in Burp.
2. Replace the filename value with: `....//....//....//etc/passwd`.
3. Send the request; if `/etc/passwd` is returned, the simple filter didn’t catch the altered traversal string.

**Images (placeholders — add 2–3 screenshots):**

* `images/path_traversal_stripped_nonrec_step1.png`
* `images/path_traversal_stripped_nonrec_step2.png`
* `images/path_traversal_stripped_nonrec_step3.png`

**Quick note:** Filters should normalize input before checking for traversal sequences.

---

## Lab 3 — Traversal sequences stripped with superfluous URL-decode

**What this teaches (one line):**
How double-encoding or extra URL decoding can bypass checks that don’t fully normalize input.

**Simple beginner walkthrough:**

1. Capture the image request and edit the filename parameter in Burp.
2. Use a double-encoded traversal value such as: `..%252f..%252f..%252fetc/passwd`.
3. Send the modified request; if `/etc/passwd` is returned, the server decoded the value and allowed traversal despite the filter.

**Images (placeholders — add 2–3 screenshots):**

* `images/path_traversal_doubleencode_step1.png`
* `images/path_traversal_doubleencode_step2.png`
* `images/path_traversal_doubleencode_step3.png`

**Quick note:** Normalizing (decode then check) prevents this bypass.

---

## Lab 4 — File extension validation bypass with null byte

**What this teaches (one line):**
How appending a null byte can bypass simple checks that only look at the filename extension.

**Simple beginner walkthrough:**

1. Intercept the product image request with Burp Suite.
2. Change the filename parameter to include a null byte after the target name, for example: `../../../etc/passwd%00.png`.
3. Send the edited request. If the response contains `/etc/passwd`, the server likely accepted the request as a `.png` but actually opened the earlier filename because of the null byte — showing the extension check was bypassed.

**Images (placeholders — add 2–3 screenshots):**

* `images/path_traversal_nullbyte_step1.png`
* `images/path_traversal_nullbyte_step2.png`
* `images/path_traversal_nullbyte_step3.png`

**Quick note:** Modern servers/libraries typically block null-byte tricks; validate and normalize filenames strictly.

---

