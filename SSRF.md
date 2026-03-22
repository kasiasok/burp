SSRF (Server-Side Request Forgery) to podatność, gdzie serwer wykonuje zapytanie HTTP w imieniu atakującego.


W SSRF localhost odnosi się do serwera ofiary, NIE do atakującego.

Wyobraź sobie:

Ty jesteś na zewnątrz budynku 🔒
Serwer jest w środku 🏢

Ty mówisz:

„Hej, idź do pokoju obok i zobacz co tam jest”

👉 localhost = „pokój obok serwera”.

<br><br>
<hr>
<br><br>
<h2>Lab: Basic SSRF against the local server</h2>

Change the URL in the stockApi parameter to http://localhost/admin

<img width="1185" height="473" alt="image" src="https://github.com/user-attachments/assets/61cb69fc-fbf8-4f1e-999c-29f5b4ac8045" />
<img width="868" height="441" alt="image" src="https://github.com/user-attachments/assets/1204e5d7-510a-43d8-a977-6790678e4d1a" />
<img width="878" height="548" alt="image" src="https://github.com/user-attachments/assets/4701ad9a-aa1e-498b-934f-be78d103a153" />


<br><br>
<hr>
<br><br>
<h2>Lab: Basic SSRF against another back-end system</h2>

This lab has a stock check feature which fetches data from an internal system.
To solve the lab, use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.

<img width="1168" height="627" alt="image" src="https://github.com/user-attachments/assets/bd6fdfaf-c32e-47ec-9621-8c9162f8b0e6" />

<img width="1173" height="508" alt="image" src="https://github.com/user-attachments/assets/5d05347a-dcd0-4e9f-8f11-829ba5ab204e" />

<img width="1128" height="556" alt="image" src="https://github.com/user-attachments/assets/d6cc414c-a7b0-4a5f-ae43-bf9e35978aea" />


<br><br>
<hr>
<br><br>
<h2>Lab: Blind SSRF with out-of-band detection</h2>

 This site uses analytics software which fetches the URL specified in the Referer header when a product page is loaded.
To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server. 

Nagłówek Referer (celowo zapisany bez drugiego „r”) to część zapytania HTTP, która informuje serwer skąd użytkownik przyszedł — czyli z jakiego URL-a została wykonana akcja.


payload:
Referer: https://6cjjiruq08yoxgyhpg4sje6tkkqbe12q.oastify.com

<img width="876" height="544" alt="image" src="https://github.com/user-attachments/assets/f3327a12-6db6-4489-904f-b6cea9e29bf0" />
<img width="876" height="594" alt="image" src="https://github.com/user-attachments/assets/2fd0e8f3-9f35-449b-aad8-69e0dc59e503" />



<br><br>
<hr>
<br><br>
<h2>Lab: SSRF with blacklist-based input filter</h2>

 This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.
The developer has deployed two weak anti-SSRF defenses that you will need to bypass. 

solution
stockId=http://127.0.0.1/
stockId=http://127.1/
stockId=http://127.1/admin
Obfuscate the "a" by double-URL encoding it to %2561 to access the admin interface and delete the target user. 

<img width="895" height="629" alt="image" src="https://github.com/user-attachments/assets/b371e4ab-3f8e-4dc6-9760-18f4169c9b0e" />
<img width="875" height="584" alt="image" src="https://github.com/user-attachments/assets/a0fbf5ae-efa4-40b3-afc9-f5c31b7032f0" />
<img width="879" height="525" alt="image" src="https://github.com/user-attachments/assets/a971a24e-c9ca-4b84-a265-2edfc2b827b4" />
<img width="873" height="505" alt="image" src="https://github.com/user-attachments/assets/0afdce7d-fb7c-4590-bb5b-c9645f28de18" />
<img width="886" height="563" alt="image" src="https://github.com/user-attachments/assets/f3f675e6-624f-40f2-a1cf-44beb6b82eca" />


<br><br>
<hr>
<br><br>
<h2>Lab: SSRF with filter bypass via open redirection vulnerability</h2>

 This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos.
The stock checker has been restricted to only access the local application, so you will need to find an open redirect affecting the application first. 


final payload:
/product/nextProduct?path=http://192.168.0.12:8080/admin/delete?username=carlos


tip:
<img width="1263" height="712" alt="image" src="https://github.com/user-attachments/assets/0f130cc2-b7af-42ec-9153-51364c3096de" />
my:
<img width="1194" height="638" alt="image" src="https://github.com/user-attachments/assets/b3976789-64c9-42a7-bec5-d868e0c68f2b" />
<img width="1236" height="739" alt="image" src="https://github.com/user-attachments/assets/016cd678-8ae8-4550-810c-26594366ddd8" />
<img width="881" height="515" alt="image" src="https://github.com/user-attachments/assets/46f2581c-ac20-4882-9da9-457cfc52a822" />
<img width="899" height="657" alt="image" src="https://github.com/user-attachments/assets/d837e3c9-7414-4223-af86-518b0e005799" />
<img width="916" height="602" alt="image" src="https://github.com/user-attachments/assets/f8571322-e1c6-4a39-86e7-398fe8e73fd7" />
<img width="874" height="519" alt="image" src="https://github.com/user-attachments/assets/2a73df06-0bad-47fc-97c7-bbb83e8124d6" />


