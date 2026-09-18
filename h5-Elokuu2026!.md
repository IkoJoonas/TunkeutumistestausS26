## x)

gjeopgjepw

## a) Asenna Hashcat ja testaa sen toiminta

Aloitin tehtävän seuraamalla Karvinen 2022: Cracking Passwords with Hashcat ohjeita. Loin hakemista `mkdir hashed` komennolla. 

Latasin sanalistan `wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz` purin sen `tar xf rockyou.txt.tar.gz` ja poistin ylimääräiseksi jääneen tiedosto `rm rockyou.txt.tar.gz`.

Testasin, että sanalista toimii `wc -l rockyou.txt`.

<img width="269" height="67" alt="Näyttökuva 2026-09-18 kello 17 02 04" src="https://github.com/user-attachments/assets/6f448748-040f-43f6-abb5-d6a7b1610ea3" />

Toimi.

Tunnistin tiivisteen tyypin `hashid -m 6b1628b016dff46e6fa35684be6acc96` komennolla.

<img width="495" height="390" alt="Näyttökuva 2026-09-18 kello 17 03 04" src="https://github.com/user-attachments/assets/a61547b8-09b3-4064-88a9-d0ac6d078fc2" />

Valitsin MD5 niinkuin esimerkissä. Aloitin murtamaan tiivistettä `hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved` komennolla.

<img width="659" height="604" alt="Näyttökuva 2026-09-18 kello 17 05 09" src="https://github.com/user-attachments/assets/1defb031-bb4c-4bb1-aca6-bd58d1a2d192" />

Katsoin tuloksen `cat solved` komentoa käyttäen.

<img width="384" height="77" alt="Näyttökuva 2026-09-18 kello 17 05 28" src="https://github.com/user-attachments/assets/6e814a0a-45d6-4a62-838b-d1badba006ce" />

## b) Asenna John the Ripper ja testaa sen toiminta

Aloitin tehtävän luomalla sitä varten oman hakemiston `mkdir john`.

Latasin Karvinen 2023: Crack File Password With John olevan esimerkkitiedoston `wget https://TeroKarvinen.com/2023/crack-file-password-with-john/tero.zip`

Kokeilin arvata tiedoston salasanan, mutta tuloksetta.

<img width="524" height="161" alt="Näyttökuva 2026-09-18 kello 17 08 33" src="https://github.com/user-attachments/assets/392da94c-0c13-4b48-a50d-6165c21ffb30" />

Irroitin hashin zip-tiedostosta komennolla `zip2john tero.zip >tero.zip.hash`

<img width="664" height="136" alt="Näyttökuva 2026-09-18 kello 17 09 55" src="https://github.com/user-attachments/assets/15f1f6df-5f82-48d8-9f01-85926211fc57" />

Käytin komentoa `john tero.zip.hash ` hashin murtamiseen.

<img width="670" height="279" alt="Näyttökuva 2026-09-18 kello 17 10 22" src="https://github.com/user-attachments/assets/e0aa4989-b6f5-4d40-8026-662aeb82c39a" />

Salasana löytyi **butterfly** ja kokeilin tätä. Pääsin kirjautumaan tiedostoon ja löysin sieltä tehtävän päätöksen.

<img width="667" height="196" alt="Näyttökuva 2026-09-18 kello 17 11 15" src="https://github.com/user-attachments/assets/bdcd344e-71d0-4c23-840c-252005aa8b47" />

Halusin kuitenki kokeilla John the Ripperiä lisää, joten loin **testijohn** hakemiston ja lisäsin sinne SecLists (https://github.com/danielmiessler/seclists).

<img width="662" height="64" alt="Näyttökuva 2026-09-18 kello 17 45 59" src="https://github.com/user-attachments/assets/fea97989-15e7-46fc-92a6-a5afd08b29ce" />

Koska repo on niin kattava, päätin yhdistää kaikki .txt salasanatiedostot yhdeksi isoksi tiedostoksi komennolla `find SecLists-master/Passwords -type f -name '*.txt' -print0 \
| xargs -0 cat > /home/joonas/testijohn/all-passwords.txt`.

<img width="616" height="65" alt="Näyttökuva 2026-09-18 kello 17 46 28" src="https://github.com/user-attachments/assets/bf6f71ae-312a-45a9-9146-22f72193a1e1" />

Loin **salainen.txt** tiedoston ja muutin sen `zip -e salainen.zip salainen.txt` komennolla zip -tiedostoksi. Salasanaksi keksin **ironball**.

Irrotin taas hashin zip -tiedosta `zip2john salainen.zip > salainen.zip.hash`.

Mursin hashin aiemmin luomallani **all-passwords.txt** tiedostolla.

<img width="680" height="243" alt="Näyttökuva 2026-09-18 kello 17 57 18" src="https://github.com/user-attachments/assets/786d6acd-45f7-41f5-a439-08dcc748fe3a" />

Salasanan murtaminen onnistui.






