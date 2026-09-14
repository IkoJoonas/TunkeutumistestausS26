## x) Lue/katso ja tiivistä

fwijqof

## a) Totally Legit Sertificate

Aloitin tehtävän lataamalla ZAP:in komennolla `sudo apt install zaproxy`. Käynnistin ohjelman komennolla `zaproxy &`.

<img width="996" height="741" alt="a)" src="https://github.com/user-attachments/assets/46938dc3-f2a2-4c9d-936c-a320d7c0fb73" />

Seuraavaksi menin **tools** -> **options** -> **Network** -> **Server Certificates**

<img width="932" height="721" alt="a)1" src="https://github.com/user-attachments/assets/ad1c76b2-fce2-48ec-8cc0-06f5a3ea2793" />

Loin uuden sertifikaatin ja tallensin sen. Avasin Firefoxin ja menin asetuksien kautta **View Certificates**, importtasin tiedoston, minkä olin tallentanut ja valitsin **"Trust this CA to identify websites"**. Varmistin, että sertifikaatti näkyy **Certificate Manager** listassa.

<img width="833" height="579" alt="a)2" src="https://github.com/user-attachments/assets/05040bc9-78c3-44fe-86de-bdcb11e059ac" />

Näkyi.

Seuraavaksi menin **Connection Settings**, jossa syötin seuraavat tiedot.

<img width="942" height="566" alt="a)3" src="https://github.com/user-attachments/assets/3bc93466-4f68-4462-82af-499918e10292" />

Tämän jälkeen menin selaimen `about:config` sivulle, jossa muutin kohdan **network.proxy.allow_hijacking_localhost** `true`

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

## Cross Site Scripting (XSS)

## c) Reflected XSS into HTML context with nothing encoded

Avasin labin, joka oli blogisivu jossa artikkeleita ja hakukenttä. Hakukenttä oli ainoa asia mihin pystyi syöttämään tekstiä. Syötin siihen "testi".

<img width="912" height="236" alt="c)" src="https://github.com/user-attachments/assets/15b9bbad-7394-4e3d-81ae-265c6eb9c878" />

Ei tuloksia, mikä ei tullut yllätyksenä. Tarkistelin lähdekoodia miten syötteeni palautuu sivulle.

<img width="622" height="175" alt="c)1" src="https://github.com/user-attachments/assets/3eb062ac-50ce-484b-815a-dd1e0d43ca28" />

Palautus tapahtui siten, että hakusana tulee näkyviin ilman mitään encodausta.

Päätin kokeilla yleistä kikkaa `<script>alert(1)</script>`. Tästä tuli alert-popup.

<img width="784" height="295" alt="c)2" src="https://github.com/user-attachments/assets/372b945e-1e75-4b79-a003-76ea22d906d7" />

Painoin "ok" ja labi ratkesi.

<img width="990" height="246" alt="c)3" src="https://github.com/user-attachments/assets/d87ac023-3af7-43e5-bf33-e4321869e040" />

Haavoittuvuus toimi, koska palvelin liimaa search-parametrin arvon suoraan HTMLtemplaattiin ilman mitään output encodingia. Kyseessä on siis reflected XSS, koska haitallinen koodi tulee URL-parametrin mukana `(/?search=<script>alert(1)</script>)` ja heijastuu suoraan vastaussivuun eikä tallennu palvelimelle pysyvästi. (PortSwigger, s.a.)

## d) Stored XSS into HTML context with nothing encoded

Avasin labin, joka vaikutti samanlaiselta, kuin aikaisempi, mutta nyt hakukentän sijaan oli kommenttikenttä. Syötin taas "testi" ja sen jälkeen tarkastelin lähdekoodia.

<img width="1108" height="151" alt="d)" src="https://github.com/user-attachments/assets/d00d895b-244f-4432-81bf-a0cf9b663dbd" />

Kommenttini oli tallennettu ilman encodausta. Takaisin kommenttikenttään ja syötin `<script>alert(1)</script>`.

<img width="893" height="718" alt="d)1" src="https://github.com/user-attachments/assets/9abe6ee6-bcae-49f4-a9f9-b7f5abafab96" />

Tämän jälkeen labi ratkesi.

<img width="1291" height="253" alt="d)2" src="https://github.com/user-attachments/assets/36c7afb5-6d09-4b29-9058-7b7a83165c52" />

Haavoittuvuus toimi tässä labissa samasta syystä kuin c) kohdassa eli palvelin liimaa kommentin tekstin suoraan HTML templaattiin tagin sisään ilman output-encodingia. Erona c) kohtaan on, että kommentti tallentuu palvelimen tietokantaan, joten payload suoritetaan jokaisella käyttäjällä, joka avaa artikkelin. (PortSwigger, s.a.)

## e) Selitä esimerkin avulla, mitä hyökkääjä hyötyy XSS-hyökkäyksestä

XSS:n vaarallisuus on, että koodi ajetaan uhrin selaimessa uhrin istunnon kontekstissa eli selain luulee koodin tulevan luotettavalta sivustolta. Tämä jälkeen kirjautunut käyttäjä avaa artikkelin, hänen istuntoevästeensä lähtevät hyökkääjän palvelimelle. Hyökkääjä laittaa evästeet omaan selaimeensa ja on nyt kirjautuneena uhrin tilille. Hyökkääjä voi esim. tehdä ostoksia uhrin käyttäjällä.

alert(1) on todistus haavoittuvuudesta.

## Path traversal

## f) File path traversal, simple case

Avasin labin, joka oli jonkinlaisen kaupansivusto. Klikkailin tuotteista ja menin sen jälkeen tutkimaan ZAP:in **History** välilehteen tulleita pyyntöjä.

<img width="1172" height="938" alt="f)" src="https://github.com/user-attachments/assets/51d679c7-25ef-432e-ab22-5acb13b00055" />

Huomasin, että tuotteen kuva ladataan Get /image?filename=`kuvan numero`.jpg pyyntönä.

Kopioin pyynnön ja muutin sitä `image?filename=../../../etc/passwd` muotoon. Tästä aukesi seuraavanlainen sivusto.

<img width="750" height="208" alt="f)3" src="https://github.com/user-attachments/assets/73a31d4e-0c11-48fe-a228-fb5f34f6ee83" />

Katsoin ZAP:sta **Response** välilehteä ja muutin **Body: Text** .

<img width="818" height="513" alt="f)4" src="https://github.com/user-attachments/assets/8259f9ea-593d-4c32-9df1-6b57bb76d788" />

Mielestäni olin löytänyt labille olennaista, että se olisi ratkaistu siispä palasin takaaksepäin ja labi muuttuikin ratkenneeksi.

<img width="745" height="322" alt="f)5" src="https://github.com/user-attachments/assets/5a27a4c0-c616-4718-96aa-7fc68b5f7972" />

Tässä haavoittuvuus toimii, koska palvelin yhdistää kuvakansion polun ja filename parametrin arvon suoraan tarkistamatta onko syötteessä ../ -sekvenssejä.

## g) File path traversal, traversal sequences blocked with absolute path bypass

Avasin labin ja aloitin lähestymisen niin, kuin aiemmissa labeissa.

<img width="1169" height="909" alt="g)" src="https://github.com/user-attachments/assets/60c89d39-ee39-4e90-9f09-39314524dd02" />

Materiaaleissa luki, että voi kokeilla suoraan `/etc/passwd` joten kokeilin sitä.

<img width="1177" height="604" alt="g)2" src="https://github.com/user-attachments/assets/18542a50-3d74-4c8d-be0b-476c315ab430" />

Menin takaisin labiin ja päivitin sivun, labi oli ratkaisutu.

<img width="748" height="586" alt="g)3" src="https://github.com/user-attachments/assets/e1462b10-97af-4ccf-93d7-62689a1fbe55" />

Haavoittuvuus toimi, koska sovellus suodattaa ../ -sekvenssit pois käytöstä, mutta se ei estä absoluuttisia polkuja.

## h) File path traversal, traversal sequences stripped non-recursively

Aloitus tässäkin sama, kuten aiemmin.

<img width="1173" height="933" alt="h)" src="https://github.com/user-attachments/assets/93817e42-f605-452e-8b9e-a126af261c57" />

Materiaalia lukemalla ratkaisu eli sisäistämällä ../ -sekvenssit muotoon `....//` sovellus näkee vain yhden `../` ja poistaa sen niin jäljelle jää kuitenkin toinen.

<img width="1908" height="940" alt="h)1" src="https://github.com/user-attachments/assets/626444fa-a739-4beb-b4c4-3c55336316f0" />

Labi oli ratkaistu tällä.

<img width="744" height="556" alt="h)2" src="https://github.com/user-attachments/assets/849ac8ef-eeee-4098-b69f-38160375d932" />

## i) Insecure direct object references (IDOR)

Avasin labin ja klikkasin **live chat**, tänne syötin tekstin "testi" ja lähetin sen.

Sain Get -pyynnön 2.txt . Tästä lähdin miettimään miksi aloittaa luvusta 2, eikä 1.

Muokkasin pyyntöä.

<img width="1169" height="609" alt="i)1" src="https://github.com/user-attachments/assets/8ead5628-98c7-4f4c-9ded-ef2babd6f39f" />

Kopioin salasanan ja kokeilin sitä Carlosille.

<img width="746" height="650" alt="i)2" src="https://github.com/user-attachments/assets/d2ee736c-4077-4c22-afad-596fd4251448" />

Salasana oli oikein ja labi oli ratkaistu.

Haavoittuvuus toimi, koska sovellus tarjosi transcript -tiedostot suoraan tiedostonumeron perusteella tarkastamatta niitä riippumatta onko kyseinen tiedosto kirjautuneelle käyttäjälle.

## Lähteet

- PortSwigger. s.a. Cross-site scripting: https://portswigger.net/web-security/cross-site-scripting
- PortSwigger. s.a. Path traversal: https://portswigger.net/web-security/file-path-traversal
- PortSwigger. s.a. Insecure direct object references (IDOR): https://portswigger.net/web-security/access-control/idor
- Karvinen, T. 2026. https://terokarvinen.com/tunkeutumistestaus/#h4-taysin-laillinen-sertifikaatti
- OWASP 2021: OWASP Top 10:2021: A01:2021 – Broken Access Control: https://owasp.org/Top10/A01_2021-Broken_Access_Control/


