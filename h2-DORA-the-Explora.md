## x) Lue/katso/kuuntele ja tiivistä

Buuri 2026

- Red teamit käyttävät leg uppeja, jotta päästään ongelmatilanteissa eteenpäin jolloin aikaresurssit eivät ylity.

DORA

- TLPT suoritettava vähintään joka 3. vuosi tuotantojärjestelmissä, tämä kattaa kriittiset toiminnot ja ulkoistetut palvelut.

TIBER-FI

- Red team vaihe käynnistyy uhkatiedusteluraportin hyväksynnän jälkeen ja koostuu kahdesta osasta -> testisuunnitelman luomisesta ja aktiivisesta testauksesta.
- RTT käy läpi klassisen hyökkäysketjun: tiedustelu -> aseistaminen -> toimitus -> hyväksikäyttö -> liikkuminen verkossa -> toimet kohteessa.

## a) Asenna Metasploitable 2 virtuaalikoneeseen

Asensin Metasploitablen https://sourceforge.net/projects/metasploitable/ sivulta.

Purin zip. kansion ja tein VirtualBoxiin koneen.

<img width="922" height="549" alt="met asennus" src="https://github.com/user-attachments/assets/f3770742-34f5-4bfd-af24-f6067ea6443e" />

## b) Tee Kalin ja Metasploitablen välille virtuaaliverkko

Debianin verkkoasetukset

<img width="529" height="78" alt="debian 2 net" src="https://github.com/user-attachments/assets/1668919d-9f2d-44bb-8531-2feda09fcb73" />

Metasploitablen verkkoasetukset

<img width="522" height="69" alt="meta net" src="https://github.com/user-attachments/assets/aa3b48fb-b42f-443e-8f41-0c21fab9b04b" />

## c) Harjoittelemme omassa virtuaaliverkossa, jossa on Kali ja Metaspoitable. Osoita testein, että 1) koneet eivät saa yhteyttä Internetiin 2) Koneet saavat yhteyden toisiinsa.

Tarkistin Metasploitablen IP-osoitteen

<img width="713" height="175" alt="met ip" src="https://github.com/user-attachments/assets/dc07b928-cde9-4554-b95e-50f7eb156472" />

Kokeilin komentoa `ping 8.8.8.8`

<img width="360" height="36" alt="met ping" src="https://github.com/user-attachments/assets/a68f1882-16e9-4cd9-90df-d7dd19492890" />

Ei yhteyttä verkkoon niin, kuin pitää.

Seuraavaksi kokeilin Debianilla pingata verkkoon ja Metasploitableen.

<img width="712" height="252" alt="deb 2 ping" src="https://github.com/user-attachments/assets/835e2b8e-e679-481b-8dc0-4185c8e9c9c2" />

Molemmat onnistui, ei yhteyttä verkkoon, mutta onnistunut yhteys Metasploitableen.

## d) Etsi Metasploitable porttiskannaamalla

Ajoin komennon `nmap -sn 192.168.56.0/24`

<img width="749" height="162" alt="deb nmap" src="https://github.com/user-attachments/assets/9452eab2-9307-4fe4-a492-8601f117f609" />

Tuloksia tuli kaksi ja päätin kokeilla ensimmäistä.

<img width="1603" height="609" alt="deb met confirm" src="https://github.com/user-attachments/assets/10430ee0-1073-4dd3-980b-150f78204a72" />

Selaimella tarkistaminen osoitti, että IP oli oikea.

## e) Porttiskannaa Metasploitable huolellisesti ja kaikki portit

Ajoin komennon `nmap -A -T4 -p- 192.167.56.101`

Nmap löysi paljon avoimia portteja, mutta näin heti alussa kolme kiinnostavaa porttia.

<img width="842" height="519" alt="nmap ports" src="https://github.com/user-attachments/assets/b80eb8a3-3d61-4e03-9003-451fdc7c1910" />

`Portti 21/tcp FTP` näyttää, että palvelimelle pystyy kirjautumaan ilman käyttäjätunnusta tai salasanaa.

`Portti 22/tcp OpenSSH` vanha OpenSSh versio

`Portti 23/tcp Telnet` vanhentunut verkkoprotokolla

## f) Vapaaehtoinen bonus: Sisään vaan. Pääsetkö murtautumaan Metasploitableen?

Päätin kokeilla onnistunko murtautumisessa.

`FTP`

<img width="448" height="270" alt="f) conf3" src="https://github.com/user-attachments/assets/e2aaee92-bf23-47c7-b105-f29701825fe1" />

Kirjautumiseen riitti käyttäjätunnukseksi `anonymous` ja salasana kohdan pystyi jättämään tyhjäksi.

`OpenSSH`

<img width="906" height="414" alt="f) conf4" src="https://github.com/user-attachments/assets/6eb019de-2cc6-447b-ab16-dc792ef8bab5" />

Kirjautuminen ei vaatinut käyttäjätunnusta ja salasanaksi kelpasi Metasploitablen oletussalana `msfadmin`.

`Telnet`

<img width="892" height="843" alt="f) conf2" src="https://github.com/user-attachments/assets/75a2745a-2aaf-461a-a533-57b87127930d" />

Kirjautuminen onnistui oletustunnuksilla `msfadmin:msfadmin`.

e) kohdassa löytämistä tuloksista selaamalla alaspäin löysin vielä yhden mielenkiintoisen portin, jota päätin kokeilla.

<img width="614" height="27" alt="f) port1524" src="https://github.com/user-attachments/assets/39dcd7be-ae1b-468b-863c-a63f1b61f5fa" />

<img width="517" height="136" alt="f) conf" src="https://github.com/user-attachments/assets/1c2dbe63-8713-46be-a59d-2639fb7e387e" />

Tässä pääsin suoraan `root` käyttäjäksi ilman mitään käyttäjätunnuksia.

Kaikki murtautumiset onnistui :)

## Lähteet

- https://terokarvinen.com/tunkeutumistestaus/#h2-dora-the-explora
- Buuri 2026: https://terokarvinen.com/buuri-2026-dora-and-threat-lead-penetration-testing/buuri-2026-dora-and-threat-lead-penetration-testing--teros-pentest-course.pdf
- DORA, Article 26 "Advanced testing of ICT tools, systems and processes based on TLPT"
Article 27 "Requirements for testers for the carrying out of TLPT" https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng
- TIBER-FI, 5.4 Testing phase: Red team testing https://www.suomenpankki.fi/globalassets/bof/en/money-and-payments/the-bank-of-finland-as-catalyst-payments-council/tiber-fi/tiber-fi-2.0-procedures-and-guidelines.pdf
- https://sourceforge.net/projects/metasploitable/
- Gemini, f) kohdassa ssh-komennon saamiseen

## Laitteisto

Käytin tehtävissä Kalin sijaan Debiania

Host: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2
