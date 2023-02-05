## Lisää Apachea

### Getting started

+ URL kertoo osoitteen, missä jokin resurssi sijaitsee netissä
+ Clientti lähettää serverille resurssipyynnön käyttäen jotain tiettyä protokollaa (esim. http, https). Resurssipyyntö lähetetään käyttäen URL-polkua.
+ Serveri lähettää clientille vastauksen. Vastaus sisältää statuksen (esim. 200 ok, 4040 not found jne.) ja mahdollisesti bodyn. 
+ Nämä clientin ja serverin väliset liikkeet tallentuvat lokitiedostoon
+ Clientin täytyy ensin selvittää, missä serverissä pyydetty resurssi sijaitsee. Clietti selvittää serverin nimen ja sitä kautta IP-osoitteen, jonne pyyntö lähetetään
+ Useampi hostname voi käyttää samaa IP-osoitetta ja yhtä fyysistä serveriä kohden voi olla useampia IP-osoitteita (tämä onnistuu käyttämällä VirtualHostia)
+ Serverin ohjaukset kirjataan Apachen konfigurointi-tiedostoon
+ Nettisivun sisältö voidaan jakaa staattiseen ja dynaamiseen sisältöön: staattista sisältöä ovat esim. kuva, html ja css tiedostot, jotka sijaitsevat tietyssä tiedostokansiossa. Dynaaminen eli mukautuva sisältö muodostuu siinä tilanteessa, kun pyyntö tehdään. Esimerkkejä dynaamisesta sisällöstä ovat mm. käyttäjän sijainti, sää ja lämpötila sekä käytettävä järjestelmä (selain, laitetyyppi). Myös tieto siitä, kuinka moni muu käyttäjä katselee juuri samaa sivua kuin sinä, on dynaamista tietoa. 
+ Lokitiedostot ja varsinkin virheloki on ongelmanselvityksestä tärkein tietolähde

### Name-baased Virtual Host Support 



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

Annan neuvotun komennon $ sudo systemctl status apache2 ja saan virhetiedot. Poimin ilmoituksesta tämän rivin: Syntax error on line 6 of /etc/apache2/sites-enabled/newfrontpage.conf ja tämän rivin perusteella lähtisin tutkimaan newfrontpage.conf tiedostoa. Virheilmoituksessa myös sanotaan, että Apache error logs saattaa sisältää enemmän tietoa, joten tarkistan sen komennolla $ sudo tail -l /var/log/apache2/error.log. Lokitiedot eivät suoraan palauta mitään uutta tietoa, muuta kuin lisäohjeen antaa komento $ sudo /usr/sbin/apache2ctl configtest. Virheilmoituksessa kerrottiin tarkemmin, missä kohtaa tiedostoa oli virhe. 

![lokitiedot_virheilmoitus](https://user-images.githubusercontent.com/82024427/216787691-ccc9c4c6-8216-424d-8fe5-b2fa5637d2be.png)

Käyn korjaamassa virheen, ja annan uudestaan komennon käynnistää demoni, mutta saan uuden virheilmoituksen: 
mirkah@mirka-virtualbox:/etc/apache2/sites-available$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Sat 2023-02-04 21:18:18 EET; 13s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 2474 ExecStart=/usr/sbin/apachectl start (code=exited, status=1/FAILURE)
        CPU: 7ms

helmi 04 21:18:18 mirka-virtualbox systemd[1]: Starting The Apache HTTP Server...
**helmi 04 21:18:18 mirka-virtualbox apachectl[2477]: AH00526: Syntax error on line 4 of /etc/apache2/sites-enabled/newfrontpage.conf:
helmi 04 21:18:18 mirka-virtualbox apachectl[2477]: Unknown Authz provider: alla** Poimin tämän rivin virheilmoituksesta ja menen katsomaan tiedostoa newfrontpage.conf ja sen riviä 4. Sieltä löytyy kirjoitusvirhe. 

Seuraavaksi uudelleen käynnistys onnistuu. Mutta testi $ curl localhost antaa Forbidden (403). Eli jotain on vielä pielessä. Käyn katsomassa Apachen error logia (komento $ sudo tail -l /var/log/apache2/error.log) ja sieltä saan vastauksen, minkä perusteella voin jatkaa selvitystä. 

[Sat Feb 04 21:21:09.075050 2023] [authz_core:error] [pid 2505:tid 139780157146880] [client ::1:46846] AH01630: client denied by server configuration: /home/mirkah/public_sites/
[Sat Feb 04 21:21:28.263582 2023] [authz_core:error] [pid 2505:tid 139780140361472] [client 127.0.0.1:44142] AH01630: **client denied by server configuration: /home/mirkah/public_sites/** Suuntaan jälleen katseet newfrontpage.conf tiedostoon ja käyn katsomassa, mikä polku tiedostoon on annettu. Siellä on kirjoitusvirhe polussa. Korjaan kirjoitusvirheen, käynnistän demonin uudestaan ja testaan sivun komennolla $ curl localhost. Nyt sivun teksti näkyy oikein. 

![sivu_toimii_taas_ongelmien_jalkeen](https://user-images.githubusercontent.com/82024427/216788043-815d851f-35cc-439d-8781-27d973ebe757.png)

### Lähteet

https://kanava.to/dynaaminen-sisalto-ja-sen-mahdollisuudet/






