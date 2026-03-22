SSRF (Server-Side Request Forgery) to podatność, gdzie serwer wykonuje zapytanie HTTP w imieniu atakującego
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

