Unprotected Admin Functionality
Objective

The goal of this lab was to identify and exploit an application that exposes administrative functionality without proper access control.

Steps Performed
1. Intercepting Requests

I configured Burp Suite to intercept requests between my browser and the target application. While browsing the website, I observed the HTTP requests and responses to understand how the application handled user access.

2. Inspecting the Source Code

Using Burp Suite, I examined the server's response and searched for the keyword "admin". This revealed a hidden endpoint:

<a href="/admin">Admin panel</a>

Although the link was not visible to regular users, it was still present in the HTML source code, indicating that the endpoint existed and could potentially be accessed directly.

3. Accessing the Admin Panel

I manually navigated to:

/admin

Since the application did not enforce proper authorization checks, I was able to access the administrator panel successfully.

4. Deleting a User

Within the admin panel, I identified the functionality used to delete users. Burp Suite captured the following request:

GET /admin/delete?username=carlos HTTP/2

By sending the request, the server responded with:

HTTP/2 302 Found
Location: /admin

The 302 Found response confirmed that the deletion request had been processed successfully before redirecting back to the admin page.

Result

The lab was successfully completed by exploiting unprotected administrative functionality. The application exposed an administrator endpoint without verifying user privileges, allowing unauthorized access to sensitive administrative actions such as deleting users.

Key Takeaways
Administrative endpoints should never rely on hidden links for security.
Proper authentication and authorization checks must be enforced on every sensitive endpoint.
Burp Suite is an effective tool for discovering hidden functionality and analyzing HTTP requests and responses.
Security through obscurity is not a valid defense mechanism.
