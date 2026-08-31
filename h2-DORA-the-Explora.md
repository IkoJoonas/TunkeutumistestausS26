## x) Lue/katso/kuuntele ja tiivistä

fqwojfjwpqf

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

Tarkistin Metasploitablen ip osoitteen

<img width="713" height="175" alt="met ip" src="https://github.com/user-attachments/assets/dc07b928-cde9-4554-b95e-50f7eb156472" />

Kokeilin komentoa `ping 8.8.8.8`

<img width="360" height="36" alt="met ping" src="https://github.com/user-attachments/assets/a68f1882-16e9-4cd9-90df-d7dd19492890" />

Ei yhteyttä verkkoon niin, kuin pitää.

Seuraavaksi kokeilin Debianilla pingata verkkoon ja Metasploitableen.

<img width="712" height="252" alt="deb 2 ping" src="https://github.com/user-attachments/assets/835e2b8e-e679-481b-8dc0-4185c8e9c9c2" />

Molemmat onnistui, ei yhteyttä verkkoon, mutta onnistunut yhteys Metasploitableen.
