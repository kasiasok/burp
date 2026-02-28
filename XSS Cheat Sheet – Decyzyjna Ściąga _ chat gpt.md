```
🧠 XSS Cheat Sheet – Decyzyjna Ściąga
🔎 1️⃣ Najpierw ustal kontekst

Gdzie trafia input?

HTML body

Atrybut

JavaScript

URL

JSON

👉 Kontekst determinuje klasę wektora.

🛡 2️⃣ WAF Bypass – Klasy Technik
Tier 1 – Obfuskacja

kodowanie znaków (HTML / Unicode)

base64 + dekodowanie runtime

rozbijanie słów kluczowych

Tier 2 – Alternatywne eventy

nietypowe event handlery

rzadko filtrowane atrybuty

Tier 3 – DOM-based

manipulacja location

javascript: URI

execution przez DOM sink

🔐 3️⃣ CSP Bypass – Logika Decyzyjna

Sprawdź nagłówek:

Content-Security-Policy
Jeśli img-src pozwala na zewnętrzne domeny

→ resource loading możliwy

Jeśli script-src pozwala na zewnętrzne domeny

→ external script execution możliwe

Jeśli inline JS zablokowany

→ eventy / external only

Jeśli wszystko blokowane

→ szukaj:

JSONP

open redirect

subdomain takeover

gadget chain

DOM clobbering

👻 4️⃣ Blind XSS – Priorytety

Cel:

brak popup

brak widocznych efektów

cicha exfiltracja

Preferowane klasy:

pasywny resource load

asynchroniczna wysyłka danych

external loader

📊 5️⃣ Kolejność Testowania (Praktyka)

1️⃣ Czy można wstrzyknąć element HTML
2️⃣ Czy działają eventy
3️⃣ Czy można ładować zewnętrzne zasoby
4️⃣ Czy inline JS działa
5️⃣ Czy CSP ogranicza
6️⃣ Czy da się łańcuchować podatności

🎯 6️⃣ Mental Model Senior Pentestera

Nie pytaj:

jaki payload wkleić?

Pytaj:

jaki mechanizm wykonania kodu jest dozwolony?

📈 Real-World Heurystyka

Proste resource load działa częściej niż złożone JS

Im krótszy payload → tym większa kompatybilność

SVG często blokowane jako pierwsze

CSP decyduje o kierunku ataku

⭐ Najważniejsza Zasada

Najpierw mapujesz ograniczenia.
Potem dobierasz klasę techniki.
Payload to tylko implementacja.
```
