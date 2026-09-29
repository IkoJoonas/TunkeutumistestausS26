## x) Tiivistä

Hoikkala 2026: Fuzzing with Fuff, kalvot joohoin esityksestä kurssilta.

- Ffuf:illa voi fuzzata nettisivujen URL:ia, headereita ja dataa
- Sanalistojen käyttö on suotavaa

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

## c3) Recursion

Suoritin komennon

<img width="953" height="72" alt="c3)" src="https://github.com/user-attachments/assets/535c66f2-ad67-4954-bfd1-53596e5a435b" />

<img width="948" height="814" alt="c3)1" src="https://github.com/user-attachments/assets/50ccf06e-3644-47f9-a7c9-3cb855be90c2" />

Onnistuin.

## c4) Virtual hosts

Suoritin kommenon valmiiksi annetuilla flageilla.

<img width="937" height="613" alt="c4)" src="https://github.com/user-attachments/assets/bf55994f-8f33-41d6-b0f8-1d8c73c370f1" />

Muutin parametrejä ja löysin mielestäni loput kaksi.

<img width="899" height="28" alt="c4)1" src="https://github.com/user-attachments/assets/f1d273de-3e79-429e-b220-28dd8ddb8b7c" />

<img width="906" height="28" alt="c4)2" src="https://github.com/user-attachments/assets/3e7f76ce-fe2b-44ad-9e0d-749110ba17ea" />

## c9) The login you cannot replay

Aloitin ottamalla curlilla login -sivun tiedot.

<img width="856" height="781" alt="c9)" src="https://github.com/user-attachments/assets/5d2e106c-9477-452d-8d83-b5f812f9517e" />

Tämän jälkeen loin **preflight.txt** tiedoston, jonne lisäsin tiedot curlista.

<img width="508" height="123" alt="c9)1" src="https://github.com/user-attachments/assets/c3196127-b06f-4be2-950d-5638f43848a8" />

Ajoin komennon ja tulosteessa oli valtava määrä eri vaihtoehtoja.

<img width="791" height="877" alt="c9)2" src="https://github.com/user-attachments/assets/e4fa613e-7865-43b8-be4d-86adac07f22e" />

Huomasin, että sanamäärä 237 toistuu, joten filtteröin sen pois `-fw 237` parametrillä.

<img width="829" height="635" alt="c9)3" src="https://github.com/user-attachments/assets/4b25910f-ab1b-4fc5-9921-d53a0d068202" />

Sain näkyville oletetun salasanan.

<img width="861" height="381" alt="c9)4" src="https://github.com/user-attachments/assets/1b2e322b-fa0a-4817-bdd0-7fa491a44617" />

Salasana toimi ja tehtävä oli suoritettu.

## Lähteet

Karvinen, T. 2026 Tunkeutumistestaus. Luettavissa: https://terokarvinen.com/tunkeutumistestaus/#h6-fuzzy-feeling-upon-finding. Luettu 29.9.2026

Ffuf How to play. Luettavissa: https://ffuf.io.fi/play. Luettu 29.9.2026

ffuf - Fuzz Faster U Fool. Luettavissa: https://github.com/ffuf/ffuf. Luettu 29.9.2026

Hoikkala, J. 2026. Fuzzing with Fuff. Luettavissa: https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf. Luettu 29.9.2026
