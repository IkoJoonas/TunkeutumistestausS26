## x) Tiivistä

åwoegjewåog

## a) Vaultline

Scope. Mikä on kohde?

-Kohde on rajattu https://ffuf.io.fi verkkosovellukseen ja sen tarjoamiin rajapintoihin.

Rules of engagement. Mitä sille saa tehdä, eli mitä tai millaisia menetelmiä saa käyttää?

- Tarkoitettu fuzzauksen harjoitteluun.

Mihin oikeutesi tehdä tietoturvatestausta tähän kohteeseen perustuu?

- Oikeus perustuu omistajan antamaan lupaan.

Riskit ja mitigointi. Tuo palvelin on Internetissä. Tunnista lyhyesti riskit ja niiden mitigointi ennen käytännön harjoittelua.

- Riskinä liian suuret määrät pyyntöjä, jotka voivat kuormittaa palvelinta.
- Mitigointina rajoitetaan pyyntöjen määrää.

## b) Asenna ffuf versio, joka tukee aivan uutta preflight-ominaisuutta.

Asensin menemällä ffuf:in Github sivustolle (https://github.com/ffuf/ffuf) ja asensin sieltä uusimman version. Asentamisen jälkeen purin kansion ja muokkasin oikeuksia.

<img width="581" height="361" alt="ffuf asennus" src="https://github.com/user-attachments/assets/d6520aa5-5797-41f5-ab4c-f56a398658e1" />

## c1) Content discovery

Aloitin tehtävän lataamalla **content.txt** ja **passwords.txt** tiedostot. Ajoin vinkeissä annetun komennon `ffuf -w content.txt -u https://ffuf.io.fi/FUZZ`.

<img width="902" height="566" alt="c1)" src="https://github.com/user-attachments/assets/58cea81b-7e07-4e08-93df-c6b694910cfb" />

Selasin tulostetta ja päätin filttereidä ne, jotka sisältävät 135 sanaa. Filtteröinti tapahtui `-fw 135` parametrillä.

<img width="602" height="64" alt="c1)1" src="https://github.com/user-attachments/assets/675706ff-b4f6-4823-bb42-9a3069ea6f1c" />

