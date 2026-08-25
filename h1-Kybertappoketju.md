## x) Lue/katso/kuuntele ja tiivistä

  Herrasmieshakkerit

- Päivittäin mietitään mitä kautta Keskoa vastaan voidaan hyökätä.
- Keskitetty tietoturvatiimi

  Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains, chapters Abstract, 3.2 Intrusion Kill Chain.

- Tietoverkkojen hyökkäysketjussa on seitsemän vaihetta: 1. Tiedustelu 2. Aseistaminen 3. Toimitus 4. Hyväksikäyttö 5. Asennus 6. Komento ja ohjaus 7. Tavotteiden toteuttaminen.

  € Santos et al: The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance.

- Nmap on suosituin porttiskanneri
- Masscan on nopein porttiskanneri
- Udpprotoscanner on nopea UDP porttiskanneri

  KKO 2003:36

- A oli suorittanut porttiskannauksen Osuuspankkikeskus-OPK osuuskunnan tietojärjestelmään.

## a) Asenna Kali

Olen asentanut Kalin aiemmin

<img width="842" height="426" alt="Näyttökuva 2026-08-25 kello 16 43 23" src="https://github.com/user-attachments/assets/9c9d71bd-c17c-4a7a-91aa-54afcfa48bee" />

<img width="384" height="237" alt="Näyttökuva 2026-08-25 kello 16 41 46" src="https://github.com/user-attachments/assets/9247c1ae-f657-46ec-be2b-1442405d55df" />

## b) Irrota Kali-virtuaalikone verkosta

Katkaisin verkkoyhteyden ja varmistin, ettei kone saa yhteyttä internettiin komennolla `ping 8.8.8.8`

<img width="471" height="236" alt="Näyttökuva 2026-08-25 kello 16 45 22" src="https://github.com/user-attachments/assets/e894e7df-d14d-4d18-a547-96e72744108f" />

Ei yhteyttä.

## c) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi

Suoritin skannauksen komennolla `nmap -T4 -A localhost`

<img width="858" height="273" alt="Näyttökuva 2026-08-25 kello 16 54 15" src="https://github.com/user-attachments/assets/c917ce06-cebd-4ea3-8a0d-cef08a888c7d" />

Parametrit:

- `-T4` on nmapin aggressiivinen profiili
-  `-A` on aggressiivinen tunnistus

localhost-osoitteessa ei tällä hetkellä kuunnella mitään TCP-palvelua, jotka ovat nmapin 1000 yleisimmissä porteissa.

## d) Asenna kaksi vapaavalintaista demonia ja skannaa uudelleen.

Minulla oli valmiiksi asennettuna ssh ja apache2 demonit. Käynnistin ne ja ajoin komennon `nmap -T4 -A localhost` uudestaan.

<img width="595" height="226" alt="Näyttökuva 2026-08-25 kello 17 06 47" src="https://github.com/user-attachments/assets/71546cc9-1a4f-44bf-aae0-65143ea4ffc4" />

Nmap löysi portit, tunnisti palveluiden statuksen, nimet ja versiot.

## e) Ratkaise vapaavalintainen kone HackTheBoxista

Ratkaisin koneen `Fawn`

<img width="910" height="92" alt="Näyttökuva 2026-08-25 kello 17 29 06" src="https://github.com/user-attachments/assets/a9635d16-a01e-4e06-b451-52dab03ae47b" />

## Lähteet

- Herrasmieshakkerit. 25.9.2024. Tietoturvan Niksipirkka, vieraana Juho Rikala | 0x34. https://open.spotify.com/episode/4jBaSSkXdfsEWJrg0QRaVA?si=8693682c057c470b
- Hutchins et al. 2011. Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains. 3.2 Intrusion Kill Chain. https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf
- Santos et al. 2019. The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance. https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_03/
- Finlex. 2003. KKO:2003:36. https://www.finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36
