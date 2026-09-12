## x) Lue/katso ja tiivistä

fwijqof

## a) Totally Legit Sertificate

Aloitin tehtävän lataamalla ZAP:in komennolla `sudo apt install zaproxy`. Käynnistin ohjelman komennolla `zaproxy &`.

<img width="996" height="741" alt="a)" src="https://github.com/user-attachments/assets/46938dc3-f2a2-4c9d-936c-a320d7c0fb73" />

Seuraavaksi menin **tools** -> **options** -> **Network** -> **Server Certificates**

<img width="932" height="721" alt="a)1" src="https://github.com/user-attachments/assets/ad1c76b2-fce2-48ec-8cc0-06f5a3ea2793" />

Loin uuden sertifikaatin ja tallensin sen. Avasin Firefoxin ja menin asetuksien kautta **View Certificates** importtasin tiedoston, minkä olin tallentanut ja valitsin **"Trust this CA to identify websites"**. Varmistin, että sertifikaatti näkyy **Certificate Manager** listassa.

<img width="833" height="579" alt="a)2" src="https://github.com/user-attachments/assets/05040bc9-78c3-44fe-86de-bdcb11e059ac" />

Näkyi.

Seuraavaksi menin **Connection Settings**, jossa syötin seuraavat tiedot.

<img width="942" height="566" alt="a)3" src="https://github.com/user-attachments/assets/3bc93466-4f68-4462-82af-499918e10292" />

Tämän jälkeen kirjoitin selaimen `about:config` sivulle, jossa muutin kohdan **network.proxy.allow_hijacking_localhost** `true`

<img width="1154" height="338" alt="a)4" src="https://github.com/user-attachments/assets/92d09401-54c5-45d3-bee4-f93afd7d269b" />

Nyt Firefox ohjaa localhost liikennettä proxyn läpi.

Kävin vielä laittamassa kuvien sieppauksen päälle ZAP:issa. **tools** -> **options** -> **Display** -> **Process images in HTTP requests/responses**.

Testasin näenkö liikennettä menemällä `http://example.com` sivulle.

<img width="930" height="756" alt="a)5" src="https://github.com/user-attachments/assets/edb5ab9b-ce84-456c-8b94-eb0c9a03eb29" />

Näkyi.

## b) Kettumaista

Aloitin ottamalla proxyn pois päältä Firefoxin asetuksien **Connection Settings** kohdasta.

<img width="949" height="567" alt="b)" src="https://github.com/user-attachments/assets/45fafd50-9770-484b-a4ba-8afedc73f454" />

Asensin FoxyProxyn selaimen addoneista.

<img width="1325" height="611" alt="b)1" src="https://github.com/user-attachments/assets/0ed80de0-e184-463f-a081-fba7a0e84380" />

Avasin FoxyProxyn asetukset ja **Proxies** välilehdelle täytin seuraavanlaisesti.

<img width="1266" height="587" alt="b)2" src="https://github.com/user-attachments/assets/57bb15d8-a968-4586-8035-a22b8f29d0c2" />

Tämän jälkeen alempana olevaan **Proxy by Patterns** osioon lisäsin kolme patternia, jotka ohjaavat ZAP:iin vain ennalta määritetyt osoitteet.

<img width="1134" height="192" alt="b)3" src="https://github.com/user-attachments/assets/09fcde23-e0c0-401e-93e6-cf3581d77cb4" />

Tallensin asetukset ja käynnistin FoxyProxyn **Proxy by Patterns**.

Testasin olinko saanut laitettua asetukset oikein menemällä PortSwiggerin sivuille ja valitsemalla labin, jonka olin aiemmin tehnyt.

<img width="1862" height="766" alt="b)4" src="https://github.com/user-attachments/assets/14a97e3d-1c0b-4db7-bd7c-56792953aa2e" />

Patterns toimi oikein ja vain määritellyt sivustot tulivat ZAP läpi.

# Cross Site Scripting (XSS)

## c) Reflected XSS into HTML context with nothing encoded
