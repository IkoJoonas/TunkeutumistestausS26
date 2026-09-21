## x)

Karvinen 2022: Cracking Passwords with Hashcat

- Järjestelmät tallentavat salasanat tiivisteinä eli hash.

Karvinen 2023: Crack File Password With John

- Hyödyntää sanakirjahyökkäystä tiedostojen salasanojen murtamiseen.
- Ensin irroitetaan tiiviste ja sen jälkeen murretaan saatu hash.

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

## c) Tiedosto

Päätin kokeilla murtaa pdf -tiedoston. Aloitin luomalla tekstitiedoston.

<img width="417" height="57" alt="Näyttökuva 2026-09-21 kello 10 40 38" src="https://github.com/user-attachments/assets/f4eff4f6-6e76-4227-a965-a12331e4b658" />

Asensin paketinhallinnasta tarvittavat työkalut murtamiseen: `enscript` `ghostscript` ja `qpdf`.

`enscript` muuttaa tekstin PostScriptiksi.

`ghostscript` muuttaa PostScriptin pdf:ksi.

`qpdf` salaa pdf:n AES-256 salauksella.

Etenin työkalujen asentamisen jälkeen komennoilla:

`enscript -p testi.ps testi.txt`

`ps2pdf testi.ps testipdf` , ps2pdf on osa `ghostscript`ä.

`qpdf --encrypt mouse mouse 256 -- testi.pdf salatesti.pdf` , **mouse** on salasana.

Irrotin hashin salatusta pdf -tiedostosta komennolla `pdf2john salatesti.pdf > salatesti.pdf.hash`.

Tämän jälkeen mursin tiivisteen komennolla `john --wordlist=all-passwords.txt salatesti.pdf.hash`.

<img width="668" height="245" alt="Näyttökuva 2026-09-21 kello 10 39 38" src="https://github.com/user-attachments/assets/a98bbdf9-883e-45f2-b9c2-2229ba6e25c0" />

Tuloste paljasti asettamani salasanan.

## d) Tiiviste

Kokeilin murtaa Linux-käyttäjän salasanan tiivisteen. Aloitin luomalla testikäyttäjän tehtävää varten komennolla `sudo useradd -m testi`.

Asetin salasanan `sudo passwd testi` salasanaksi laitoin **password1**.

Yhdistin käyttäjätilit ja salasanahashit yhteen tiedostoon `sudo unshadow /etc/passwd /etc/shadow > ~/testilinux.hash`

<img width="568" height="68" alt="Näyttökuva 2026-09-21 kello 10 48 24" src="https://github.com/user-attachments/assets/72f77d0f-5788-4c45-822d-9a11fd797cd6" />

Yritin purkaa tiivisteen Johnilla, mutta epäonnistuin.

<img width="516" height="89" alt="Näyttökuva 2026-09-21 kello 10 48 54" src="https://github.com/user-attachments/assets/0e1c8994-4f3a-497f-9b3c-43ccd2834075" />

Ongelmana oli, että John ei tunnistanut tiivistettä, koska Kali käytti oletuksena yescrypt muotoa.

Poistin luomani käyttäjän ja oikaisin luomalla uuden käyttäjän SHA-512 tiivisteellä syöttämällä `PASS=$(openssl passwd -6 password1)` ja `sudo useradd -m -p "$PASS" testi`.

Toistin samat vaiheet mitä aiemmin ja nyt sain salasanan selville.

<img width="666" height="262" alt="Näyttökuva 2026-09-21 kello 10 51 41" src="https://github.com/user-attachments/assets/db4ec20b-f7c6-464c-9e05-f05d26fe30df" />

(Kysyin tekoälyltä apua, jotta pääsin oikotiellä etenemään tehtävässä.)

## e) Sanakirja

Loin sanakirjan käyttämällä nanoa.

<img width="669" height="180" alt="Näyttökuva 2026-09-21 kello 10 55 15" src="https://github.com/user-attachments/assets/11690e9e-3fa5-4ee7-9683-6132df157d58" />

Loin ensin tekstitiedoston ja siitä zip -tiedoston ja salasanaksi asetin sanakirjasta löytyvän sanan **raketti**.

Irroitin hashin zip -tiedostosta ja mursin sitä käyttämällä luomaani sanakirjaa.

<img width="664" height="230" alt="Näyttökuva 2026-09-21 kello 11 01 01" src="https://github.com/user-attachments/assets/3cab745c-e23f-4d12-b471-9e25dedc9f01" />

Tehtävän kulku oli aikalailla sama, kuin kohdassa b).

## f) Hash rules

Mursin tässä salasanan **Muumipeikko2026?** demonstroimalla HashCatin sääntöjä (best64, iso alkukirjain, numeroita ja erikoismerkki).

Aloitin tekemällä tekstitiedosto **oma.txt**

<img width="209" height="72" alt="Näyttökuva 2026-09-21 kello 13 54 03" src="https://github.com/user-attachments/assets/1504db2b-a67b-4df5-a3e1-dadf22581cdb" />

Tein sääntötiedoston **oma.rule**

<img width="208" height="70" alt="Näyttökuva 2026-09-21 kello 13 57 51" src="https://github.com/user-attachments/assets/3ef0ee86-120c-42f2-8081-e06b34035925" />


Loin MD5 -tiivisteen salasanasta komennolla `echo -n 'Muumipeikko2026?' | md5sum`.

<img width="368" height="72" alt="Näyttökuva 2026-09-21 kello 13 51 28" src="https://github.com/user-attachments/assets/63af8e83-4426-46d0-a36e-d96695966c39" />

Tallensin sen tiedostoon **oma.hash**.

<img width="639" height="58" alt="Näyttökuva 2026-09-21 kello 13 51 37" src="https://github.com/user-attachments/assets/70f0fc96-efcd-4a82-96d4-552ffed6e98a" />

<img width="312" height="77" alt="Näyttökuva 2026-09-21 kello 13 51 43" src="https://github.com/user-attachments/assets/7838fa0e-906f-4581-b845-6a92bdac0c58" />

Syötin komennon `hashcat -m 0 -a 0 oma.hash oma.txt -r oma.rule`

<img width="657" height="462" alt="Näyttökuva 2026-09-21 kello 14 03 48" src="https://github.com/user-attachments/assets/6486e80c-6e9a-485a-92a3-0b02a82dd808" />

Tarkistin vielä tuloksen.

<img width="532" height="87" alt="Näyttökuva 2026-09-21 kello 14 03 57" src="https://github.com/user-attachments/assets/14248a2a-2943-44f5-993f-822845137354" />

Salasanan murtaminen oli onnistunut.

## Lähteet

Karvinen, T. 2026 Tunkeutumistestaus. Luettavissa: https://terokarvinen.com/tunkeutumistestaus/#h5-elokuu2026. Luettu 21.9.2026

Karvinen, T. 2022: Cracking Passwords with Hashcat. Luettavissa: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/. Luettu 18.9.2026

Karvinen, T. 2023: Crack File Password With John. Luettavissa: https://terokarvinen.com/2023/crack-file-password-with-john/. Luettu 18.9.2026

