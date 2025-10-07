# High-level summary

Business logic vulnerabilities happen when an application lets users bypass rules or manipulate normal processes. These flaws can let someone get extra items, discounts, or access areas they shouldn’t. Understanding these issues helps highlight the importance of proper checks in software.

## Lab 1 — Excessive trust in client side controls

**What this teaches:** How changing quantity values can trick the system into giving negative prices or extra items.

**Simple beginner walkthrough:**

1. Log in and add a cheap item to your shopping cart.
2. In Burp Suite, find the request that controls the item quantity.
3. Change the quantity to any number and forward the request. Check that the cart updates.
4. Try using a negative number to reduce the quantity. Use a bigger negative number to make the cart go below zero.
5. Add another item and use negative quantities to lower the total price below your store credit. Place the order to finish.

![image alt](https://github.com/Lispectree/web-sec/blob/d5479bd37ec967bc098faacbf2265f45dc886192/web-security-labs/labs/business-logic/BUS%20LOGIC%20photo1%20lab1.jpg)
After logging in 
You are required to buy the leather jacket
But your balance won’t be able to purchase it

![image alt](https://github.com/Lispectree/web-sec/blob/31ee40de032308b7897b4f345d1ed69b3b052709/web-security-labs/labs/business-logic/BUS%20LOGIC%20photo2%20lab1.jpg)
The add to cart request of the jacket
The price is client controlled and can be reduced to any price




## Lab 2 — Flawed enforcement of business rules

**What this teaches:** How improper checks let you reuse multiple discount codes to pay less.

**Simple beginner walkthrough:**

1. Log in and find the first coupon code (e.g., NEWCUST5).
2. Sign up for the newsletter to get another coupon (e.g., SIGNUP30).
3. Add an item to your cart and go to checkout.
4. Apply both codes, alternating between them to bypass the single-use rule.
5. Keep reusing the codes until the total is below your store credit, then place the order.

![image alt](



## Lab 3 — Authentication Bypass via Flawed State Machine

**What this teaches:** How skipping steps in login flow can give admin access.

**Simple beginner walkthrough:**

1. Log in and notice you select your role before reaching the home page.
2. Use a tool to find the /admin page. Trying to access it normally doesn’t work.
3. Log out, then log in again with Burp intercept on.
4. Forward the first login request, drop the next role-selection request, then go to the home page.
5. Observe you are now logged in as an administrator and complete the lab task.

*Images (placeholders — add 2–3 screenshots):*

* business\_logic\_auth\_bypass\_step1.png
* business\_logic\_auth\_bypass\_step2.png
* business\_logic\_auth\_bypass\_step3.png


