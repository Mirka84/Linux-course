## Webbi

#### Podcast

Kuuntelin Indie Hackerin sivuilta Sofware Socialin jakson 126, https://share.transistor.fm/s/428eaeff, Qualitative and Quantitative data. Jakson kesto oli 34 min. 

Jaksossa ydinpointit: 
+ kun mietitään, miten kehittää omaa bisnestä, hyvä vaihtoehto on selvittää asia suoraan omilta asiakkailta
+ tämä tapahtuu: 
1. tutkimalla, ketä ovat omat asiakkaat
2. ketkä esim. uudistavat tilauksensa
3. ketkä eivät uudista tilausta
4. ketkä luovat tilin mutta eivät maksa palveluista
5. millä aloilla asiakkaat työskentelevät
6. minkälaisia kilpailijoita markkinoilla on
+ dataa on paljon, haastavaa tietää, mikä on merkittävää dataa. 

### Apache-sivun vaihto

Apache2-palvelin oli asennettu edellisen luennon jälkeen, joten uudelleen asennusta ei tarvittu. Palvelin käynnistettiin sudo systemctl start apache2-komennolla. 
Testasin palvelimen käynnistymisen selaimessa: kirjoitin localhostin ja selain palautti Apachen sivun. Tässä vaiheessa kaikki hyvin. 

Komennolla $ echo "Hello world"|sudo tee /var/www/html/index.html lisäsin Hello World-tekstin localhostin sivulle. 

![apachen_sivu_vaihdettu](https://user-images.githubusercontent.com/82024427/216117553-519c8352-536f-4ed8-ac3c-6eef0b75163f.png)

Seuraavaksi komennolla $ sudo a2enmod userdir "käynnistettiin" apachen moduuli, ja $ sudo systmctl restart apache2-komennolla käynnistettiin apache uudelleen. Testasin
$ curl http://localhost/~mirkah, ja terminaali palautte 403, Forbidden. Tämän jälkeen tein seuraavat komennot: 

+ $ mkdir public_html
+ $ cd public_html
+ $ micro index.html

Lopputulema: 
![oma_kotisivu](https://user-images.githubusercontent.com/82024427/216122544-4f34329e-e4c3-44cb-aee8-480b108e1627.png)

### Käyttäjän kotisivu

Apachen asennuksen jälkeen ja localhostin toimivuuden testaamisen jälkeen kirjotin selaimeen http://example.com/~tero ja sain vastauksen: 

![example_kotisivu](https://user-images.githubusercontent.com/82024427/216123147-5342cd2a-18aa-4096-9b20-ed77b3643851.png)

### Käyttäjän luominen

Komennolla $ sudo adduser elmeri lisäsin Elmeri-nimisen käyttäjän. Annoin salasanan ja koko nimen. Muita tietojakin olisi voinut antaa, esim. puh.nro, mutta jätin ne tyhjiksi. Tämän jälkeen kirjauduin ulos omalta tililtä ja kirjauduin uudelleen käyttäjänä Elmeri. 

![kayttajan_lisays](https://user-images.githubusercontent.com/82024427/216124283-4bc45b1d-1d89-4af9-a99c-271fa0d5d1f9.png)

Käyttäjänä Elmeri komento $ curl http://localhost palautti "Hello world". Komento $ curl http://localhost/~elmeri palautti 403, Forbidden. 

![Elmerin_kotisivu_testi](https://user-images.githubusercontent.com/82024427/216125456-b8fa3033-8668-49df-8698-ec29e72d903b.png)

Käyttäjä Elmeri loi myös oman sivun: 

+ $ mkdir public.html
+ $ cd public.html
+ $ micro index.html

![Elmerin_kotisivu_toimii](https://user-images.githubusercontent.com/82024427/216125780-9f3869bc-32d1-4fc7-a5e5-7df35d3e37d6.png)

### Validointi

Kotisivuni ei ole julkinen, joten kopioin validoitavan tekstin teksti-inputtina validaattoriin, https://validator.w3.org/nu/#textarea. 

![validointi](https://user-images.githubusercontent.com/82024427/216129403-4e9b868a-56dc-461a-af4a-73f06ed8d0b5.png)

Kotisivu näyttää vielä tältä: 

![kotisivu](https://user-images.githubusercontent.com/82024427/216129888-76990ada-3326-4d0b-b346-55feeaada5c5.png)





