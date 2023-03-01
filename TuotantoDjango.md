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








