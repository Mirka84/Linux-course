## Vikojen selvittelyä

### Edellinen projekti ensin toimimaan

Aloitin tämän tehtävän teon lauantaina 4.3. noin klo 14.00 ja ensimmäinen tavoite oli tehdä toimiva projekti. Tällä kertaa en ottanut ssh-yhteyttä vuokrakoneeseeni, 
vaan päätin toistaa edellisen kerran tehtävän, eli siirtää projektin tuotantoon, asentamallani virtuaalikoneella. 

Seurasin tämän artikkelin, https://terokarvinen.com/2022/deploy-django/, ohjetta, ja toistettuani kaikki stepit, kaikki toimi (tätä operaatiota en dokumentoinut, koska
etenin täysin ohjeiden mukaisesti ja kaikki meni kuten artikkelissa sanottiin). 

![image](https://user-images.githubusercontent.com/82024427/222953321-3d877ab4-837d-441f-9aeb-0869dcd2ebad.png)

![image](https://user-images.githubusercontent.com/82024427/222953343-95a45b93-da2b-443a-aa9c-84808c642542.png)

### Virheitä

#### Kirjoitusvirhe testiprojekti2.conf-tiedostossa

TDIR polussa on kirjoitusvirhe. Siellä pitäisi olla käyttäjä mirkah, mutta nyt lukee vain mirka. 

![image](https://user-images.githubusercontent.com/82024427/222955526-1a34e592-3175-4184-9625-64da58741bf9.png)

Käyttöliittymä palauttaa 403, forbidden. 

![image](https://user-images.githubusercontent.com/82024427/222956346-a2557ae3-4fac-4c55-a565-edcec4400b6e.png)

Apachen error.log näyttää seuraavat tiedot (komento `sudo tail -F /var/log/apache2/error.log`): 

![image](https://user-images.githubusercontent.com/82024427/222956472-06c04d11-6e19-4839-bd35-ee2a7ac27910.png)

Loki näyttää, että virhe olisi eri polun takana, eli WSGI-polun takana. Tuosta osaisi lähteä etsimään virhettä confi-tiedostosta, mutta ensimmäisenä etsisin virhettä eri polusta. 

#### Settings.pysta puuttuu ALLOWED_hostista localhost

Selain näyttää 404, bad request, kun päivitän selaimen localhost/admin. 

![image](https://user-images.githubusercontent.com/82024427/222956141-194de948-5f4f-4979-a2e7-0482db0e6d53.png)

Lokitiedot: 

![image](https://user-images.githubusercontent.com/82024427/222956749-62e17dca-ee5c-4967-980f-ef206323bd7d.png)

Tein myös kirjoitusvirheen ALLOWED_Hosts, localhos. 

Käyttöliittymä palauttaa 404, bad requestin. 

![image](https://user-images.githubusercontent.com/82024427/222957173-76f9eb54-def8-43e6-8c52-ada6fec54a39.png)

Ja Apachen error.log 

![image](https://user-images.githubusercontent.com/82024427/222957223-c2683176-419c-4641-b36d-34b177aeb9d0.png)

Error login merkinnät valitettavasti ovat melko hankalatulkintaisia. 











