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












