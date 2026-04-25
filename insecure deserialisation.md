Insecure Deserialisation = problem z KONWERSJĄ danych
Prototype Pollution      = problem z STRUKTURĄ obiektów JS

 
Dane w RAM = specyficzne dla procesu, maszyny, języka Dane w sieci = muszą być uniwersalne i przenośne Konwersja = tłumacz między tymi dwoma światami
Bez konwersji każda aplikacja mówiłaby własnym, niezrozumiałym dla innych językiem.

 marshalling (Ruby) or pickling (Python). These terms are synonymous with "serialization" in this context.

 
Aplikacja = kod działający na serwerze – to on deserializuje dane i jest podatny.
Przeglądarka tylko wysyła – serwer przetwarza. Problem leży zawsze po stronie serwera.

<br><br>
<hr>
<br><br>
<h2>Lab: Modifying serialized objects</h2>

Login > intercept > Cookies > burp inspector > b0 na b1 > forward
znów to samo, tylko /admin/delete?username=carlos

<br><br>
<hr>
<br><br>
<h2>Lab: Modifying serialized data types</h2>

Login > intercept > Cookies > burp inspector

O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}
/admin/delete?username=carlos

<br><br>
<hr>
<br><br>
<h2>Lab: Using application functionality to exploit insecure deserialization</h2>

<img width="1336" height="447" alt="image" src="https://github.com/user-attachments/assets/3a878e0b-a149-4bbc-8265-8dda2752e33c" />


 
