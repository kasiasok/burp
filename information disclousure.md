<br><br>
<hr>
<br><br>
<h2>Lab: Information disclosure in error messages</h2>

Original: GET /product?productId=1
Non-Integer Attack: GET /product?productId=example


<br><br>
<hr>
<br><br>
<h2>Lab: Information disclosure on debug page</h2>

Go to the "Target" > "Site Map" tab.
Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to /cgi-bin/phpinfo.php

secret key value

<br><br>
<hr>
<br><br>
<h2>Lab: Source code disclosure via backup files</h2>

/robots.txt

<br><br>
<hr>
<br><br>
<h2>Lab: Authentication bypass via information disclosure</h2>

Backend ujawnia (information disclosure) coś, co pozwala obejść logowanie — w tym labie jest to nazwa specjalnego nagłówka HTTP, który daje dostęp admina.

1. Jak aplikacja powinna działać

Normalnie:

Użytkownik się loguje
Backend sprawdza:
sesję / cookie
Jeśli OK → wpuszcza do /admin

2. Co jest zepsute

Backend ma ukrytą logikę typu:

„Jeśli request zawiera specjalny nagłówek → traktuj jako zaufany (np. admin/front-end)”

Walkthrough:
1. Brute force /my-account z payloadmi panelu admina  np. https://github.com/Karanxa/Bug-Bounty-Wordlists/blob/main/admin.txt
2. Po znalezionym endpoincie 401, testy różnych metod. Działa TRACE
3. Robimy TRACE /admin i tam odkrywa nam się nowy nagłówek X-costam:728.23.12.33.
4. Robimy żadanie GET /admin z tym nagłówkiem. Zmieniamy wartość na 127.0.0.1

<img width="1698" height="723" alt="image" src="https://github.com/user-attachments/assets/ff6b3820-a107-4cc2-a3a2-da4be00eb350" />

<img width="826" height="715" alt="image" src="https://github.com/user-attachments/assets/efa08b6b-1c1f-44e2-be0a-b4595d5885e4" />

<img width="1681" height="851" alt="image" src="https://github.com/user-attachments/assets/09c1dc72-1143-4360-a7b9-854921c10c4c" />

<img width="820" height="769" alt="image" src="https://github.com/user-attachments/assets/4ce18786-c09a-4b89-bdcf-da8f10f0d71c" />

<img width="843" height="645" alt="image" src="https://github.com/user-attachments/assets/4bee6c7f-3def-4071-bbb5-967c963c6ec4" />



<br><br>
<hr>
<br><br>
<h2>Lab: Information disclosure in version control history</h2>

Ppm discover content
└─$ wget -r https://0a1600e3042864418022260d00d300f9.web-security-academy.net/.git 
Cd githubowyfolder
Cd .git
Git show
git log
git diff commit1hash commit2hash

<img width="1081" height="532" alt="image" src="https://github.com/user-attachments/assets/7259e8fc-5a4b-436e-8fe8-6985b357c76a" />

<img width="1142" height="643" alt="image" src="https://github.com/user-attachments/assets/eb181c3c-4250-4c44-a69d-1de2c1bd1dc0" />

<img width="711" height="508" alt="image" src="https://github.com/user-attachments/assets/cde2704a-97b9-4789-bbad-248a99746b80" />

<img width="1065" height="556" alt="image" src="https://github.com/user-attachments/assets/727743be-758d-44b8-a203-932cba6a7dee" />



