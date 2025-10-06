# API Testing Labs

**High-level summary:**
API vulnerabilities occur when web applications expose endpoints that can be accessed in unexpected ways. Attackers can manipulate these endpoints to retrieve data, modify resources, or perform actions they shouldn't be allowed to. This lab set teaches beginners how to explore and test API endpoints safely.

## Lab 1 — Exploiting an API endpoint using documentation

**What this teaches:**
Learn how exposed API documentation can reveal endpoints and actions.

**Simple beginner walkthrough:**

1. Log in to the application and update your email.
2. Find the API request for updating your email and send it to Burp Repeater.
3. Try removing parts of the URL to discover the API documentation.
4. Open the interactive documentation in your browser and locate the DELETE endpoint.
5. Use the DELETE endpoint to remove the user carlos to solve the lab.

![image alt](https://github.com/Lispectree/web-sec/blob/fdc933f392dc0420334bc9d4d90a285834a0c7f0/labs/sql-injection/ap1%20lab%201%20photo%201.jpg)
Use the update email function


![image alt](https://github.com/Lispectree/web-sec/blob/991c4f87d38fb8320859f3b41f73576fa9f28f4c/labs/sql-injection/ap1%20lab%201%20photo%202.jpg)
Monitor the request and remove any other requests attached to the api to see that api documentation


![image alt](https://github.com/Lispectree/web-sec/blob/1ba09517426ff2bdbf09ccd898943e15d6a1e59f/labs/sql-injection/ap1%20lab%201%20photo%203.jpg)
Follow the api documentation of the delete request to delete the user instructed by the lab


## Lab 2 — Finding and exploiting an unused API endpoint

**What this teaches:**
Learn how to identify hidden or unused API endpoints and manipulate them.

**Simple beginner walkthrough:**

1. Click on a product and locate its API request in Burp HTTP history.
2. Send the request to Burp Repeater.
3. Change the request method to PATCH and add the Content-Type header as application/json.
4. Add a JSON body with {"price":0} to set the product price to zero.
5. Reload the product page, add it to your basket, and place the order to solve the lab.

![image alt](https://github.com/Lispectree/web-sec/blob/3527c4489eea9b2541e653e3438da9e795c156f2/web-security-labs/labs/api-testing/ap1%20lab%202%20photo%201.jpg)
This shows the request for a product we are trying to purchase

![image alt](https://github.com/Lispectree/web-sec/blob/2081cb9a020ace5f2b2e95710bdc4d94089ca81c/web-security-labs/labs/api-testing/ap1%20lab%202%20photo%202.jpg)
Changing the request to PATCH 
It shows that a json file is allowed to be attached to the request

![image alt]


## Lab 3 — Exploiting server-side parameter pollution in a REST URL

**What this teaches:**
Learn how API requests can be manipulated to access sensitive data through URL parameters.

**Simple beginner walkthrough:**

1. Trigger a password reset for the administrator account and send the request to Burp Repeater.
2. Modify the username parameter to explore different paths and API versions.
3. Identify a valid field parameter to retrieve the password reset token.
4. Use the reset token in the password reset URL to set a new password.
5. Log in as administrator and delete carlos to solve the lab.

**Images (placeholders — add 2–3 screenshots):**

* api\_testing\_parameter\_pollution\_step1.png
* api\_testing\_parameter\_pollution\_step2.png
* api\_testing\_parameter\_pollution\_step3.png
