## COOKIES

* A cookie is a small piece of text data set by Web server that resided on the client's browser for the purpose of storing information.
* Once it's been set, the client automatically returns the cookie to the web server with each request that it makes.
* This allows the server to place value it wishes to 'remember' in the cookie, and have access to them when creating a response.
* Cookies are commonly used to remember user preferences, track user behavior, and provide personalized experiences on websites.

## Key aspects of cookies:

1. **Purpose**:
    + Cookies are primarily used to maintain state and store data that needs to persist between different requests or sessions. 
    + They allow websites to remember user preferences, keep users logged in, and track user activity.

2. **Data**:
    + Cookies contain small pieces of data, usually in the form of key-value pairs.
    + The data stored in cookies can include information like user IDs, session IDs, shopping cart contents, language preferences, and more.

3. **Expiration**:
    + Cookies have an expiration time, after which they are automatically deleted from the user's browser.
    + Some cookies are set to expire when the browser session ends, while others can have a specific expiration date.

4. **Domain and Path**:
    + Cookies are associated with a specific domain and path.
    + This means that a cookie set by one website can't be accessed by another website, and the cookie is only sent to the server when making requests to the domain and path it belongs to.

5. **Security**:
    + Cookies are sent between the browser and the server with every HTTP request and response, making them susceptible to certain security vulnerabilities like cross-site scripting (XSS) attacks.
    + To mitigate these risks, it's important to properly validate and sanitize cookie data.

6. **Types of Cookies**:
    - **Session Cookies**:
        + These cookies are temporary and are deleted when the user closes their browser.
        + They are often used to maintain session information, such as keeping a user logged in.

    - **Persistent Cookies**:
        + These cookies have an expiration date set in the future and are stored on the user's device even after the browser is closed.
        + They are commonly used for remembering user preferences or tracking behavior over time.

7. **HTTP-Only and Secure Flags**:
    + Cookies can be marked as "HTTP-only" to prevent client-side scripts from accessing them.
    + Additionally, cookies can be marked as "secure," meaning they will only be sent over secure (HTTPS) connections.

8. **Same-Site Attribute**:
    + The Same-Site attribute restricts when cookies are sent to the server based on the context of the request, helping to prevent certain types of cross-site request forgery (CSRF) attacks.


## How Cookie Works

Cookies work by establishing a communication mechanism between a web server and a user's web browser.Here's a step-by-step explanation of how cookies work:

1. **Cookie Creation**:
   + When a user visits a website, the web server can include a "Set-Cookie" header in the HTTP response.
   + This header contains the data that the server wants to store as a cookie on the user's browser.
   + The cookie data is typically in the form of key-value pairs.

2. **Storing Cookies**:
   + The user's browser receives the "Set-Cookie" header and stores the cookie data as a text file on the user's device.
   + This data includes information like the cookie's name, value, expiration time, domain, and path.

3. **Sending Cookies**:
   + Whenever the user makes subsequent requests to the same website, the browser automatically includes the stored cookies in the "Cookie" header of the HTTP request.
   + This allows the server to identify the user and retrieve the relevant data associated with the cookies.

4. **Server Response**:
   + The web server receives the request along with the included cookies.
   + It can then process the cookies to recognize the user, maintain user sessions, and provide personalized content based on the stored data.

5. **Expiration and Deletion**:
   + Cookies have an expiration time, after which they are automatically deleted from the user's browser.
   + This can happen when the user closes the browser session (for session cookies) or when the specified expiration date is reached (for persistent cookies).

6. **Security and Privacy**:
   + Cookies can be configured with attributes such as "HTTP-only" to prevent client-side scripts from accessing them, and "Secure" to ensure they are sent only over secure connections (HTTPS).
   + Additionally, the "Same-Site" attribute helps prevent cross-site request forgery (CSRF) attacks.