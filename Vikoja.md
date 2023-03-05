## Vikojen selvittelyä

### Edellinen projekti ensin toimimaan

Aloitin tämän tehtävän teon lauantaina 4.3. noin klo 14.00 ja ensimmäinen tavoite oli tehdä toimiva projekti. Tällä kertaa en ottanut ssh-yhteyttä vuokrakoneeseeni, 
vaan päätin toistaa edellisen kerran tehtävän, eli siirtää projektin tuotantoon, asentamallani virtuaalikoneella. 

Seurasin tämän artikkelin, https://terokarvinen.com/2022/deploy-django/, ohjetta, ja toistettuani kaikki stepit, kaikki toimi (tätä operaatiota en dokumentoinut, koska
etenin täysin ohjeiden mukaisesti ja kaikki meni kuten artikkelissa sanottiin). 

![image](https://user-images.githubusercontent.com/82024427/222953321-3d877ab4-837d-441f-9aeb-0869dcd2ebad.png)

![image](https://user-images.githubusercontent.com/82024427/222953343-95a45b93-da2b-443a-aa9c-84808c642542.png)

### Virheitä, su 5.3. klo 12.10

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

Googletin tämän virheen: AH01276: Cannot serve directory /home/mirkah/publicwsgi/testiprojekti2/static/: No matching DirectoryIndex (index.html,index.cgi,index.pl,index.php,index.xhtml,index.htm) found, and server-generated directory index forbidden by Options directive. Tämän keskustelupalstan https://forums.cpanel.net/threads/cannot-serve-directory-home-public_html-no-matching-directoryindex-index-html-index-php-found-and-server-genera.687813/ mukaan polun /testiprojekti2/static/ sisällä ei olisi index-tiedostoa. Eikä siellä toki olekaan. Error logissa kerrotaan, että selain muodoistaisi 403, forbiddenin, mutta vastauksena näytetään kuitenkin 404. 

Tein myös kirjoitusvirheen ALLOWED_Hosts, localhos. 

Käyttöliittymä palauttaa jälleen 404, bad requestin. 

![image](https://user-images.githubusercontent.com/82024427/222957173-76f9eb54-def8-43e6-8c52-ada6fec54a39.png)

Ja Apachen error.log:

![image](https://user-images.githubusercontent.com/82024427/222957223-c2683176-419c-4641-b36d-34b177aeb9d0.png)

Tässä tapauksessa error.login ilmoitus on itselleni vaikea. Siinä kerrotaan, että virhe on apache2.conf-tiedoston rivillä 80, mutta tuohon tiedostoon en ole koskenut. 

#### Poistetaan Apachen WSGI-moduuli

Komennolla `$ sudo apt-get purge libapache2-mod-wsgi-py3` poistan Apachen wsgi-moduulin. 

Käyttöliittymä palauttaa tämän jälkeen Unable to connect. Eli nyt ei enää olla yhdistettynä Apache-serveriin. 

![image](https://user-images.githubusercontent.com/82024427/222957988-bf49f04f-968b-4c3c-8bac-6177bea804e2.png)

Moduulin poiston jälkeen yritin käynnistää demonin uudestaan, komento `$ sudo systemctl restart apache2`, mutta käynnistys ei onnistunut ja terminaali antoi ohjeen kokeilla kahta muuta komentoa, `$ sudo systemctl status apache2` ja `$ sudo journalctl -xe`. Annan nämä komennot. Näilä selviää, että demonin käynnistys ei ole onnistunut ja syy löytyisi testiprojekti2.conf-tiedostosta.  

![image](https://user-images.githubusercontent.com/82024427/222958399-21d41502-5457-495d-a4b7-3957a0c17276.png)

Apachen error.log on sitten hankalampi: 

![image](https://user-images.githubusercontent.com/82024427/222958595-802ed2a9-1530-4dab-9c84-cea24ad6a3a0.png)

#### Muita tutkimuksia

Dokumentit, mitä muokattu, löytyvät komennolla `$ find -printf '%T+%p\n' | sort`. 

![image](https://user-images.githubusercontent.com/82024427/222962117-47dddf7a-3b41-4168-8a6a-a1d4b2330991.png)

Hieman toki ihmetyttää, että miksi tuossa listassa ei näy testiprojekti2.conf tiedostoa, koska sitä on muokattu tänään tätä tehtävää tehdessä. 



### Lähteet 

https://terokarvinen.com/2022/deploy-django/

https://forums.cpanel.net/threads/cannot-serve-directory-home-public_html-no-matching-directoryindex-index-html-index-php-found-and-server-genera.687813/











