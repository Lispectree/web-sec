# High-level summary

Server-side template injection (SSTI) occurs when user-supplied input is rendered inside a server-side template without proper sanitization. SSTI can allow attackers to execute arbitrary code, access sensitive objects, or manipulate server-side logic. These labs demonstrate SSTI in multiple template engines: ERB (Ruby), Freemarker (Java), Handlebars, and Django, showing how attackers can exploit template engines to perform destructive or sensitive operations safely in a lab environment.

---

## Lab 1 — Basic server-side template injection (ERB / Ruby)

**What this teaches:** How unsanitized template input can be used to execute system commands in ERB templates.

**Simple beginner walkthrough:**

1. Open the lab and view the first product details.
2. Observe that a `message` parameter is rendered in the template. Test with `<%= 7*7 %>` to confirm that expressions are evaluated.
3. From Ruby documentation, discover that the `system()` method can execute OS commands.
4. Construct the payload `<%= system("rm /home/carlos/morale.txt") %>` and URL-encode it.
5. Add the payload to the `message` parameter in the URL:
   `https://YOUR-LAB-ID.web-security-academy.net/?message=<%25+system("rm+/home/carlos/morale.txt")+%25>`
6. Load the URL to execute the command and solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* ssti_erb_step1.png
* ssti_erb_step2.png
* ssti_erb_step3.png


## Lab 2 — Server-side template injection using documentation (Freemarker / Java)

**What this teaches:** How reading template engine documentation can guide the creation of SSTI exploits in Freemarker templates.

**Simple beginner walkthrough:**

1. Log in and edit a product description template.
2. Identify Freemarker syntax using `${someExpression}`.
3. Study the documentation for the dangerous `new()` built-in and locate the `Execute` class to run OS commands.
4. Construct the payload:
   `<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("rm /home/carlos/morale.txt") }`
5. Save the template and view the product page. The command executes and the lab is solved.

*Images (placeholders — add 2–3 screenshots):*

* ssti_freemarker_step1.png
* ssti_freemarker_step2.png
* ssti_freemarker_step3.png

---

## Lab 3 — SSTI in an unknown template language with documented exploit (Handlebars)

**What this teaches:** How to exploit SSTI in an unfamiliar template engine by adapting a publicly documented exploit.

**Simple beginner walkthrough:**

1. Log in and edit a product description template.
2. Introduce an invalid template expression to detect the engine. Errors hint that Handlebars is in use.
3. Adapt the documented exploit by @Zombiehelp54 to execute system commands.
4. URL-encode the payload and set it as the `message` parameter in the URL.
5. Load the URL to execute the command (`rm /home/carlos/morale.txt`) and solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* ssti_handlebars_step1.png
* ssti_handlebars_step2.png
* ssti_handlebars_step3.png

---

## Lab 4 — SSTI with information disclosure (Django)

**What this teaches:** How SSTI can be used to access sensitive framework objects, such as Django’s `settings.SECRET_KEY`.

**Simple beginner walkthrough:**

1. Log in and edit a product description template.
2. Introduce an invalid template expression (e.g., `$ {{<%[%'"}}% \`) to detect Django.
3. Use `{% debug %}` in the template to enumerate accessible objects. Notice the `settings` object.
4. Access the secret key using `{{settings.SECRET_KEY}}`.
5. Save the template and submit the rendered key to solve the lab.

*Images (placeholders — add 2–3 screenshots):*

* ssti_django_step1.png
* ssti_django_step2.png
* ssti_django_step3.png


