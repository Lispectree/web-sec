# High-level summary

Race conditions occur when an application does not properly handle multiple operations happening at the same time. Attackers can exploit timing gaps to bypass restrictions, duplicate actions, or manipulate sensitive processes. Understanding these flaws helps developers design systems that safely manage simultaneous actions.

## Lab 1 — Limit Overrun Race Conditions

**What this teaches:** How sending multiple requests at the same time can bypass quantity or usage limits.

**Simple beginner walkthrough:**

1. Log in and add a cheap item to your cart using a discount code.
2. Identify the endpoints for adding items and applying discount codes.
3. In Burp Repeater, duplicate the POST /cart/coupon request into a group with 20 tabs.
4. Send the requests in parallel and observe that the discount is applied multiple times.
5. Add the leather jacket and repeat to reduce the total below your store credit, then complete the purchase.

![image alt](https://github.com/Lispectree/web-sec/blob/f41a5f6289c1781a414abd7e26e9b2368f7b5128/web-security-labs/labs/race-conditions/RACE%20LAB1%20PHOTO1.jpg)
After logging in it shows you have a promo code


![image alt](

## Lab 2 — Multi-endpoint Race Conditions

**What this teaches:** How exploiting timing across multiple endpoints can bypass purchase restrictions.

**Simple beginner walkthrough:**

1. Log in and add a gift card to your cart.
2. Identify the POST /cart and POST /cart/checkout endpoints.
3. In Burp Repeater, send the requests in parallel instead of sequentially.
4. Observe if the checkout succeeds even with insufficient funds.
5. Repeat with the leather jacket until the purchase completes successfully.

*Images (placeholders — add 2–3 screenshots):*

* race\_conditions\_multi\_endpoint\_step1.png
* race\_conditions\_multi\_endpoint\_step2.png
* race\_conditions\_multi\_endpoint\_step3.png

## Lab 3 — Exploiting Time-Sensitive Vulnerabilities

**What this teaches:** How simultaneous requests can produce identical tokens for password resets.

**Simple beginner walkthrough:**

1. Submit a password reset for your account and observe the token in the email.
2. Send multiple POST /forgot-password requests in parallel using different session cookies.
3. Observe when two requests generate identical tokens.
4. Change the username in one request to target another user, like carlos.
5. Use the shared token to reset the other user's password and complete the lab.

*Images (placeholders — add 2–3 screenshots):*

* race\_conditions\_time\_sensitive\_step1.png
* race\_conditions\_time\_sensitive\_step2.png
* race\_conditions\_time\_sensitive\_step3.png


