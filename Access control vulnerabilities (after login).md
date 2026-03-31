<br><br>
<hr>
<br><br>
<h2>Lab: Unprotected admin functionality</h2>

/robots.txt


<br><br>
<hr>
<br><br>
<h2>Lab: Unprotected admin functionality with unpredictable URL</h2>

JavaScript on homepage source that discloses the URL of the admin panel

<br><br>
<hr>
<br><br>
<h2>Lab: User role controlled by request parameter</h2>

Login weak user


/admin

Cookie: Admin=false. Change it to Admin=true

<br><br>
<hr>
<br><br>
<h2>Lab: User role can be modified in user profile</h2>

Change mail
(przekleic cale body z response i zmienić imie i role id)
"roleid":2

<br><br>
<hr>
<br><br>
<h2>Lab: User ID controlled by request parameter</h2>

URL id: /my-account?id=carlos

<br><br>
<hr>
<br><br>
<h2>Lab: User ID controlled by request parameter, with unpredictable user IDs</h2>

Find a blog post by carlos
Click on carlos and observe that the URL contains his user ID

<br><br>
<hr>
<br><br>
<h2>Lab: User ID controlled by request parameter with data leakage in redirect</h2>

Response body on fail changing /id=carlos

<br><br>
<hr>
<br><br>
<h2>Lab: User ID controlled by request parameter with password disclosure</h2>

id" parameter in the URL to administrator.
View the response in Burp and observe that it contains the administrator's password.

<br><br>
<hr>
<br><br>
<h2>Lab: Insecure direct object references</h2>

1.txt

<br><br>
<hr>
<br><br>
<h2>Lab: URL-based access control can be circumvented</h2>

Dodać nagłówek:
X-Original-Url: /admin
X-Original-Url: /admin/delete

<br><br>
<hr>
<br><br>
<h2>Lab: Method-based access control can be circumvented</h2>

Log in using the admin credentials.
Browse to the admin panel, promote carlos, and send the HTTP request to Burp Repeater.
Open a private/incognito browser window, and log in with the non-admin credentials.
Attempt to re-promote carlos with the non-admin user by copying that user's session cookie into the existing Burp Repeater request, and observe that the response says "Unauthorized".
Change the method from POST to POSTX and observe that the response changes to "missing parameter".
Convert the request to use the GET method by right-clicking and selecting "Change request method".
Change the username parameter to your username and resend the request.

<br><br>
<hr>
<br><br>
<h2>Lab: Multi-step process with no access control on one step</h2>

Copy the non-admin user's session cookie into the existing Burp Repeater request, change the username to yours, and replay it.

<br><br>
<hr>
<br><br>
<h2>Lab: Referer-based access control</h2>

Copy the non-admin user's session cookie into the existing Burp Repeater request, change the username to yours, and replay it.

 

