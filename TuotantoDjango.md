## Tuotantoasennus

Aloitin tehtävän teon lukemalla artikkelin https://terokarvinen.com/2022/deploy-django/. Kello oli 18.00 ja päivä 28.2.

Tein asennuksen vuokrakoneelleni. Ensin otin yhteyden vuokrakoneelleni, komento `$ ssh mirka@ip-osoitteeni` ja syötin salasanan. Päivitin paketit, `$ sudo apt-get update`
ja asensin tekstieditorin micron, `$ sudo apt-get -y install micro bash-completion`. 

Olin jo aikaisemmassa tehtävässä asentanut virtuaalikoneelleni apachen ja alkuteksti oli vaihdettu. 

![image](https://user-images.githubusercontent.com/82024427/222212146-9312adfc-893f-42f3-aef3-7ebb22baff8b.png)

Seuraavaksi loin käyttäjänä sisältöä: `$ mkdir -p publicwsgi/mirka/static/`,  `$ echo "Let's see if this works!"|tee publicwsgi/mirka/static/index.html`. Sitten tein muutokset conffi-tiedostoon: `$ sudoedit /etc/apache2/sites-available/mirka.conf`ja sinne oikeat ohjaukset. Muutoksen jälkeen aktivoitiin oikea conffitiedost: `$ a2ensite mirka.conf` ja defaultticonffitiedosto "suljettiin", `$ a2dissite 000-default.conf`. 

![image](https://user-images.githubusercontent.com/82024427/222214716-b04ffb4f-75f0-448d-9ab7-a794484e6177.png)

![image](https://user-images.githubusercontent.com/82024427/222214089-dff6c0ed-9127-454b-bace-4759d8b49186.png)

Testasin muutoksen: `$ /sbin/apache2ctl configtest` ja sain herjan, minkä sai ohittaa, ja ilmoituksen, että Syntax OK. Apachen uudelleen käynnistys, `$ sudo systemctl restart apache2` ja testi, `$ curl http://localhost/static/`. 

![image](https://user-images.githubusercontent.com/82024427/222215914-3ea6390c-9b81-4ea8-be06-94586a50f4f2.png)

Kaikki siis vaikuttaa olevan ok! Eteenpäin. 

Asensin virtuaalikehitysympäristön, `sudo apt-get -y install virtualenv`, siirryin kansioon `$ cd publicwsgi/` ja`$ virtualenv -p python3 --system-site-packages env` komennolla asennettiin pythonin paketteja, mutta näitä paketteja on myös mahdollista käyttää kehitysympäristön ulkopuolella. Aktivoin ympäristön, `$ source env/bin/activate`. Aktivointi onnistui ja nimen eteen ilmestyi sulkuihin env. 

![image](https://user-images.githubusercontent.com/82024427/222216983-ef9f9999-9820-4f48-891e-5c1cacb160c4.png)

Sitten kysytään, mikä pip: `$ which pip`. Kirjoitetaan tesktitiedostoon, mitä halutaan asentaa. `$ micro requirements.txt
` tiedostoon kirjoitin django (ja tarkistin useasti, että menihän oikein). Sitten jälleen se pelottava komento: `$ pip install -r requirements.txt`. 

![image](https://user-images.githubusercontent.com/82024427/222217392-780daefa-7258-4806-be11-0b44bc238b55.png)

Testasin, että onnistuiko asennus, `$ django-admin --version` ja vastauksena palautui versio 4.17. Loin uuden projektin `$ django-admin startproject mirkahei`. 

![image](https://user-images.githubusercontent.com/82024427/222218299-73820c93-95f9-486e-9092-be0ab8b59304.png)

Seuraavana oli polkujen määrittely conffitiedostoon. Avasin tiedoston editoriin `$ sudoedit /etc/apache2/sites-available/mirka.conf` ja kopioin artikkelista ohjeen mukaan tekstit ja muutin polkujen tiedot. (Edit 21.30, kopioinnin vaaroista varoitettiin, ja kompastuin siihen.. :)). 

![ohjaustiedot_confitiedostoon](https://user-images.githubusercontent.com/82024427/222219281-d740362f-c796-4b57-9667-e9811ebaaf0e.png)

Sitten etenin ohjeen mukaan: `$ sudo apt-get -y install libapache2-mod-wsgi-py3` ja testaus `$ /sbin/apache2ctl configtest`. Syntax Ok, käynnistetään apache uudestaan, `$ sudo systemctl restart apache2` ja `$ curl -s localhost|grep title`. Mutta otsikko!!!! Forbidden? 

![image](https://user-images.githubusercontent.com/82024427/222220446-3c6a110b-18a5-4fb5-a080-10b3a72a4ea4.png)

Palasin ohjeet läpi, ja tässä vaiheessa en keksinyt, että mistä tuo forbidden voi johtua. Jatkoin eteenpäin artikkelin mukaan. Ajattelin, että tehdään asennukset ja tutkitaan sitten. Siirryin projektin kansioon, `$ cd mirkahei/` ja avasin asetustiedoston, `$ micro mirkahei/settings.py`. Sinne muutettiin DEBUG=False ja lisättiin sallitut HOSTit. Muutoksen jälkeen taas käynnistettiin demoni uudestaan `$ sudo systemctl restart apache2` ja tarkistataan, mitä palautuu. `$ curl -s localhost|grep title`, ohjeen mukaan piti palautua not found, mutta jälleen palautuu forbidden. 

![image](https://user-images.githubusercontent.com/82024427/222221696-f8527c4f-131c-49e3-b0ab-b8486164ff45.png)

![image](https://user-images.githubusercontent.com/82024427/222221555-212a820c-03ef-4951-ac7e-837085a93fe8.png)

Nyt tutkin apachen error logeja. `$ sudo tail -F /var/log/apache2/error.log` ja sieltähän paljastui, että polkuun oli jäänyt kopioituna artikkelista teroco! Siirryin confitiedostoon `$ sudoedit /etc/apache2/sites-available/mirka.conf` ja korjasin polut. 

![image](https://user-images.githubusercontent.com/82024427/222228052-27d559ea-4f11-4667-82e5-5efb1c92b8ec.png)

Korjaus ei kuitenkaan edelleenkään auttanut. Käynnistin myös demonin uudestaan. Kello kävi, joten jatkoin vielä eteenpäin artikkelin ohjeiden mukaisesti. Siirryin projektikansioon, avasin asetustiedoston `$ micro mirkahei/settings.py` ja muokkasin sinne ohjeen mukaan
import os
STATIC_ROOT = os.path.join(BASE_DIR, 'static/'). 

![image](https://user-images.githubusercontent.com/82024427/222229939-6e4c9a0b-c9f9-49c2-a400-03456b05042e.png)

![image](https://user-images.githubusercontent.com/82024427/222230598-d4186364-f2a8-4b74-bc87-449ee9b12433.png)

Viimeisin virheilmoitus, kello 22.09, joten tähän lopetin. Django antoi edelleen forbiddeniä. 

![image](https://user-images.githubusercontent.com/82024427/222231451-dc419fe3-68f6-4cb0-b831-561c11f32c7a.png)

### Ongelman selvittelyn jatkaminen.. 

Selvittely jatkuu torstaina työpäivän jälkeen, joten katsotaan, mikä tilanne perjantaina. :) 

### Lähteet

https://terokarvinen.com/2022/deploy-django/






