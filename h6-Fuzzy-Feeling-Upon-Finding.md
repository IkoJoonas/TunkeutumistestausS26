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

<img width="933" height="325" alt="c1)2" src="https://github.com/user-attachments/assets/3ed9a4a8-d5fb-40d9-b9c3-2881adc6b4f2" />

Selkeyden vuoksi filtteröin vielä status 200 pois lisäämällä `-mc 200` parametrin.

<img width="685" height="62" alt="c1)3" src="https://github.com/user-attachments/assets/5435d3de-e85b-4dcc-922c-b698ff240bd9" />

<img width="930" height="203" alt="c1)4" src="https://github.com/user-attachments/assets/0c136b6a-ab24-4b42-b343-9a718e435506" />

Tehtävän tavoitteeseen päästy.

## c2) The interesting non-200

Aloitin fuzzaamisen ottamalla kaikki status koodit `-mc all`.

<img width="603" height="65" alt="c2)" src="https://github.com/user-attachments/assets/51414e5c-8b2c-4670-a4a7-79c24006408b" />

<img width="930" height="519" alt="c2)1" src="https://github.com/user-attachments/assets/f583f5a4-6feb-4254-89d2-a57ba90a7692" />

Seuraavaksi filtteröin status 200 pois näkyvistä.

<img width="935" height="654" alt="c2)2" src="https://github.com/user-attachments/assets/9121dfb5-b72a-48de-863c-66637e84b9da" />

Suoritettu.

