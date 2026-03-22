
<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting an API endpoint using documentation</h2>

    In Burp's browser, log in to the application using the credentials wiener:peter and update your email address.

    In Proxy > HTTP history, right-click the PATCH /api/user/wiener request and select Send to Repeater.

    Go to the Repeater tab. Send the PATCH /api/user/wiener request. Notice that this retrieves credentials for the user wiener.

    Remove /wiener from the path of the request, so the endpoint is now /api/user, then send the request. Notice that this returns an error because there is no user identifier.

    Remove /user from the path of the request, so the endpoint is now /api, then send the request. Notice that this retrieves API documentation.

    Right-click the response and select Show response in browser. Copy the URL.

    Paste the URL into Burp's browser to access the documentation. Notice that the documentation is interactive.

    To delete Carlos and solve the lab, click on the DELETE row, enter carlos, then click Send request.




<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting server-side parameter pollution in a query string</h2>
