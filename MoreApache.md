## Lisää apachea

### Apachen uusi etusivu

Siirryn komennolla $ cd /etc/apache2/sites-available directoryyn, ja luon uuden tiedoston newfrontpage.conf komennolla $ micro newfrontpage.conf. Kirjotan seuraavat rivit: 
<VirtualHost *:80>
  DocumentRoot /home/mirkah/public_sites/
  <Directory /home/mirkah/public_sites/>
    require all granted
   </Directory>
</VirtualHost>. 

![luodaan_uuden_etusivun_ohjaus](https://user-images.githubusercontent.com/82024427/216786873-f18538bb-737d-42b0-85da-48875ae86105.png)

Seuraavaksi laitan newfrontpage.conf konfiguroinnit voimaan komennolla $ sudo a2ensite newfrontpage.conf ja suljen edellisen etusivun konfiguroinnin komennolla $ sudo a2dissite frontpage.conf. 
Viimeiseksi käynnistetään demoni uudestaan komennolla $ sudo systemctl restart apache2

![avataan_newfrontpage_suljetaan_frontpage](https://user-images.githubusercontent.com/82024427/216786586-16495fde-257d-460f-bdb9-d6b9e2e5f312.png)

Seuraavaksi muokkaan käyttäjänä etusivun tekstiä. /home/mirkah/ kansiossa on jo public_sites-kansio, joten sitä ei tarvitse luoda, mutta jos ei olisi, luonti onnistuisi komennolla $ mkdir public_sites. Tämä kansio sisältää jo tiedoston index.html. Avaan tiedoston tekstieditoriin $ micro index.html. Muokkaan tekstiä. 

Vanhan kotisivun teksti: 
![vanha_kotisivun_etusivu](https://user-images.githubusercontent.com/82024427/216786847-12d7344a-5372-42f3-bd6c-20a34540f761.png)

Uuden kotisivun tekstin testaus: 
![testataan_uutta_etusivua](https://user-images.githubusercontent.com/82024427/216786912-9f988e54-e0f9-4d38-bcb5-be79334349ab.png)

Testi toimii!

### Virhe asetustiedostossa

Käyn muokkaamassa newfrontpage.conf tiedoston tekstiä. Siirryn komennolla $ cd /etc/apache2/sites-available oikeaan kansioon, sitten komennolla $ micro newfrontpage.conf avaan asetustiedoston tekstieditoriin ja muokkailen tekstiä ja teen virheitä. Muokkauksen jälkeen testaan kotisivua komennolla $ curl localhost. Tässä kohtaa hämmennyn, koska en saa mitään virheilmoitusta ja kotisivun teksti tulee näkyviin. Kokeilen muutaman kerran, käyn myös kertaalleen katsomassa Apachen virhelokin, mutta sielläkään ei ole mitään ihmeellistä. Sitten huomaan, että en ole uudelleen käynnistänyt Apachea. Komento $ sudo systemctl restart apache2 tuottaakin sitten toivotun virheilmoituksen. 

![apachestatus_virheilmoitus](https://user-images.githubusercontent.com/82024427/216787206-a082100d-afad-4919-9e35-dd85eb3ba15a.png)



