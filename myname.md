## Vuokraa nimi

Päätin vuokrata nimen NameCheapista. Vuokraus lähti liikkeelle nimen etsimisestä. 

![image](https://user-images.githubusercontent.com/82024427/218303892-aea82f65-9b48-448b-8d4d-8f73ae065fb8.png)

Nimi mirkaheikkila.com oli halvin ja vapaana, joten sen päätin napata. Lisäsin tuotteen ostoskoriin. Mitään lisätuotteita en ostanut. Seuraavaksi klikkasin Check out-painiketta, se oli ainoa vaihtoehto etenemiseen. Sen jälkeen klikkailin nimen automaattisen uusinnan päälle, uusiutuminen 5 vuoden välein. (Tässä kohtaa ehkä tarkkasilmäiset huomaavat, että nimi on mirkaheikkila.net. Tätä nimeä en oikeasti vuokrannut, vaan nyt otan kuvat, ensimmäisellä kierroksella en tohkeissanit muistanut ottaa kuvia.) Tässäkin jätin valitsematta mitään lisäpalveluita, vaan rullailin sivun loppuun ja painoin Confirm order. 

![image](https://user-images.githubusercontent.com/82024427/218304043-c28a8a9d-c0c7-4b13-b893-344e8b64bf25.png)

Sitten oli vuorossa oman tilin luominen (tai kirjautuminen, jos jollakin on jo tili, itselläni ei). Täytin tiedot, käyttäjänimi, salasana, oma nimi ja sposti, ja painoin Create account and continue. Tämän jälkeen oli vuorossa maksutietojen syöttäminen. Syötin luottokortin tiedot. 

![image](https://user-images.githubusercontent.com/82024427/218304219-ee4d63b4-1800-43f6-985b-8596eceebdaf.png)

Maksun suorittamisen jälkeen seurasi seuraavan stepin valinta. Valitsin Set up your DNS ja painoin Getting started. Täältä ohjattiin kirjautumaan omalle NameCheapin tilille ja hallinnoimaan siellä omaa nimeä. 

![image](https://user-images.githubusercontent.com/82024427/218303552-4452c021-e005-409c-afdf-3fbf61f9befa.png)

Omalla tilillä näkyi heti vuokraamani nimi. Nimen perässä oli painike Manage, ja sitä klikkasin. 

![image](https://user-images.githubusercontent.com/82024427/218303586-af944182-0c58-4f28-81ef-8720973ee9ef.png)

Seuraavassa vaiheessa valitsin vaihtoehdon Advanced DNS. Siellä pääsin lisäämään IP-osoitteen nimelle. Lisäsin tunnilla käydyn ohjeen mukaan tyypiksi A Record, hostiksi nimeni ja toisen A Recordin pelkälle www:lle, sekä lisäsin molemmille saman IP-osoitteen. A Record osoittaa IPv4 osoitteisiin, tästä syystä tämä valinta (https://elementor.com/resources/glossary/what-are-dns-record-types/?utm_source=google&utm_medium=cpc&utm_campaign=13060922353&utm_term=&gclid=EAIaIQobChMI-9m68d2P_QIVXJBoCR0_8gSkEAAYAiAAEgIeIvD_BwE). Klikkasin painiketta Save changes ja testasin tilanteen. 

![image](https://user-images.githubusercontent.com/82024427/218303717-bfad04c7-f351-4a12-8d96-9765ad808979.png)

![image](https://user-images.githubusercontent.com/82024427/218303701-8e2206c6-19e1-4cb7-a266-ecf9b60191ae.png)

Syötin selaimeen www.mirkaheikkila.com, ja vastauksena sain oman aloitussivuni. Samaten pelkkä mirkaheikkila.comin syöttö tuotti saman aloitussivun. Muutokset siis tallentuivat onnistuneesti. 

![image](https://user-images.githubusercontent.com/82024427/218303797-6cc16d3d-79b6-4395-be4c-d4f9ebc12fab.png)

### Komennot 'host' ja 'dig'

Komennolla `$ host mirkaheikkila.com` ja `$ host www.mirkaheikkila.com` saan seuraavia tietoja: 

`mirkaheikkila.com mail is handled by 10 eforward1.registrar-servers.com` 
`www.mirkaheikkila.com has address 167.71.53.92` 

Eforward1.registrar-server viittaa NameCheapin palvelimeen. Ja toinen tieto kertoo nimen osoittaman sivun IP-osoitteen. 

![host_komento](https://user-images.githubusercontent.com/82024427/218305784-1edaec07-12ee-4471-8f03-c2831b9afe5f.png)

Komento `$ host 167.71.53.92`antaa seuraavan vastauksen: 

`mirka@debian-s-1vcpu-1gb-fra1-01:~$ host 167.71.53.92
92.53.71.167.in-addr.arpa domain name pointer example235612518.com.
mirka@debian-s-1vcpu-1gb-fra1-01:~$`

Komento kertoo domain tietoja jostain tietystä IP-osoitteesta. Example235612518.com haku tuotti kuitenkin vastauksen, ettei sivua löydy. 
  
Dig-komennon käytön aloitin testaamalla, onko paketti valmiina asennettuna, eli tein komennon `$ dig -v`. Mitään digin versiota ei ollut, joten asensin sen komennolla `$ sudo apt-get install dnsutils`.

Komennot `$ dig mirkaheikkila.com` ja `$ dig www.mirkaheikkila.com` antavat erilaisia tuloksia. Artikkelin https://phoenixnap.com/kb/linux-dig-command-examples mukaan dig-komennon vastauksessa tärkeintä on Answer-osio. Ensimmäinen komento ei tuottanut ollenkaan Answer-osiota. Ensimmäinen komento palauttaa Authority-osion. Se sisältää tietoja domainista, kuten adminin email-osoitteen, SOA-tietoa (start of authority). 

Kun taas haki www.mirkaheikkila.com-tietoja, tuolloin palautui Answer-osio. Osio sisältää tiedon siitä, mitä haettiin, kyselyn luokan (internet), tyypin (osoite) ja IP-osoitteen.

![dig_komento_www](https://user-images.githubusercontent.com/82024427/218311525-e9dc3611-c369-4767-87d4-0eb78049fd90.png)



### Lähteet 

https://elementor.com/resources/glossary/what-are-dns-record-types/?utm_source=google&utm_medium=cpc&utm_campaign=13060922353&utm_term=&gclid=EAIaIQobChMI-9m68d2P_QIVXJBoCR0_8gSkEAAYAiAAEgIeIvD_BwE

https://www.geeksforgeeks.org/host-command-in-linux-with-examples/

https://phoenixnap.com/kb/linux-dig-command-examples

https://www.cloudflare.com/learning/dns/dns-records/dns-soa-record/

https://www.cloudns.net/blog/linux-host-command-troubleshot-dns/
