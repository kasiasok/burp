>JWT

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







Lab: JWT authentication bypass via kid header path traversal
może wygasnąc sesja dla tokena EXP > zalogować się na wienr podobnie. żeby rozwiazać GET /admin

kid 
../../../../../../../dev/null

<img width="1577" height="913" alt="image" src="https://github.com/user-attachments/assets/a436452c-8214-4053-a2c1-a9f508887522" />


<img width="1177" height="932" alt="image" src="https://github.com/user-attachments/assets/2c605d39-dd72-42fb-90cc-bce3f93b872e" />




************************
<img width="889" height="637" alt="image" src="https://github.com/user-attachments/assets/5e1d22cd-9611-4156-ada4-fd5b1372e3e7" />

<img width="837" height="799" alt="image" src="https://github.com/user-attachments/assets/7d7a5dc5-7926-469a-8228-2d4819463d16" />


<img width="818" height="827" alt="image" src="https://github.com/user-attachments/assets/6cd16c41-fb8a-4c2f-9720-bd64c17c2faf" />


