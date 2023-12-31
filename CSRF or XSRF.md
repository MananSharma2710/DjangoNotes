## CSRF/XSRF

* **Cross-Site Request Forgery (CSRF)**, also known as *session riding* or *XSRF*, is a type of security vulnerability that occurs when an attacker tricks a user into unknowingly performing actions on a website without their consent.
* CSRF attacks exploit the user's authenticated session on a different site to perform unauthorized actions on the target site.
* In a CSRF attack, the attacker crafts a malicious request and tricks the victim into unknowingly sending that request to a website where the victim is authenticated.
* The website processes the request with the victim's credentials, potentially causing actions to be taken on the victim's behalf without their intention.

## Real Life Example

**Scenario: Online Bank Transfer Application**

Imagine we are logged into our online bank account and have an active session. We want to make a legitimate fund transfer to our friend's account. The bank's website processes this transaction as follows:

1. We access the page to initiate a transfer.
2. The server generates a unique token (CSRF token) and associates it with our session.
3. The token is embedded in the HTML form as a hidden field.
4. We fill out the form with the transfer details and submit it.
5. The server verifies the CSRF token. If it matches the token associated with our session, the transaction is authorized.

Now, let's consider a CSRF attack:

1. We're logged into our online bank account.
2. We visit an attacker's website that contains a hidden form with malicious actions, targeting the bank's fund transfer endpoint.
3. The malicious form is submitted automatically (using JavaScript) or by tricking us into clicking on a seemingly harmless link.
4. Because we're still authenticated in our bank's session, the browser includes our cookies in the request to the bank's website.
5. The bank's server receives the request, including our cookies, and processes the malicious action, transferring funds to the attacker's account.

In this scenario, the attacker leverages our active session to perform an unauthorized action on our behalf. The CSRF attack exploits the trust that websites have in our authenticated session.


Depending on which forms on our site are vulnerable, an attacker might be able to do the following to our victims:
* Log the victim out of our site.
* Change the victim's site preferences on our site.
* Post a comment on our site using the victim's login.
* Transfer funds to another user's account.

Attacks can also be based on the victim's IP address rather than cookies:
* Post an anonymous comment that is shown as coming from the victim's IP address.
* Modify settings on a device such as a wireless router or cable modem.
* Modify an intranet wiki page.
* Perform a distributed password-guessing attack without a botnet.


To prevent CSRF attacks, developers can implement countermeasures like using CSRF tokens, which are unique tokens embedded in forms. These tokens are checked before processing any sensitive actions. Modern frameworks and libraries provide built-in CSRF protection mechanisms to help developers guard against such attacks.


## CSRF token

* A CSRF token is a unique and random value generated by a web application and associated with a user's session.
* It's used to prevent Cross-Site Request Forgery (CSRF) attacks by ensuring that the requests sent to the server originate from the same site and are not coming from a malicious source.
* In short, a CSRF token is a security measure that helps verify the authenticity of requests and protects against unauthorized actions performed by exploiting a user's active session.