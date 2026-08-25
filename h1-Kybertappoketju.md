## x)

finmewpo

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

