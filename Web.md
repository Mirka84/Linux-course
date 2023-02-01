### Webbi

## Apache-sivun vaihto

Apache2-palvelin oli asennettu edellisen luennon jälkeen, joten uudelleen asennusta ei tarvittu. Palvelin käynnistettiin sudo systemctl start apache2-komennolla. 
Testasin palvelimen käynnistymisen selaimessa: kirjoitin localhostin ja selain palautti Apachen sivun. Tässä vaiheessa kaikki hyvin. 

Komennolla echo "Hello world"|sudo tee /var/www/html/index.html lisäsin Hello World-tekstin localhostin sivulle. 

![apachen_sivu_vaihdettu](https://user-images.githubusercontent.com/82024427/216117553-519c8352-536f-4ed8-ac3c-6eef0b75163f.png)

Seuraavaksi komennolla sudo a2enmod userdir "käynnistettiin" apachen moduuli, ja sudo systmctl restart apache2-komennolla käynnistettiin apache uudelleen. Testasin
curl http://localhost/~mirkah, ja terminaali palautte 403, Forbidden. Tämän jälkeen tein seuraavat komennot: 

+ mkdir public_html
+ cd public_html
+ micro index.html

Lopputulema: 
![oma_kotisivu](https://user-images.githubusercontent.com/82024427/216122544-4f34329e-e4c3-44cb-aee8-480b108e1627.png)

## Käyttäjän kotisivu



