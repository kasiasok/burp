JWT

Tak! Nowy klucz RSA to Twoja własna para kluczy (prywatny + publiczny).
W ataku Embedded JWK:

JWT Editor podpisuje token Twoim prywatnym kluczem
Wstrzykuje klucz publiczny do headera JWT
Serwer (jeśli podatny) używa wstrzykniętego klucza do weryfikacji zamiast swojego własnego

nie działa: alg nie jest akceptowane jako none
<img width="702" height="857" alt="image" src="https://github.com/user-attachments/assets/895ab476-8205-4590-9051-821ed3b26b42" />




działa: wygenerowanie nowego podpisu RSA i zmiana na sub: administrator > przechodze w request do /admin
<img width="1694" height="881" alt="image" src="https://github.com/user-attachments/assets/ad9a12bf-cde9-4300-9a30-c824e0736a4b" />

<img width="1041" height="852" alt="image" src="https://github.com/user-attachments/assets/edc59030-0b08-456e-b667-f81640efdec6" />


