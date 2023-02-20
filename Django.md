## Tietokantasovelluksen teko 

Aloitin tietokantasovelluksen teon lukemalla ensin artikkelin https://terokarvinen.com/2022/django-instant-crm-tutorial/ ja seuraamalla artikkelissa olleita ohjeita. 
Ensimmäisenä asennettiin kehitysympäristö. Päivitin paketit komennolla `$ sudo apt-get update` ja sen jälkeen `$ sudo apt-get install -y virtualenv`. 

![asennettaan_virtualenv](https://user-images.githubusercontent.com/82024427/220134820-6f4b4a8b-c5a4-4353-9736-294270649496.png)

Tunnilla tehdyn mallin mukaan seuraavaksi tein Django-kansion komennolla `mkdir django` ja siirryin kansioon `cd django`. Komennolla `$ virtualenv --system-site-packages -p python3 env/` 
luotiin env-kansio ja sinne asentui Python-paketit. Paketit ladattiin päivitetyistä paketeista, mutta ne haluttiin asentaa kehitysympäristön sisään. Virtuaaliympäristö käynnistettiin
komennolla `$ source env/bin/activate` ja sen onnistumisen myötä koneen nimen eteen ilmestyi (env). 

![django_kansio_ja_python_paketti](https://user-images.githubusercontent.com/82024427/220138447-debaddde-160a-48ce-b407-050aa0fe48a4.png)

Nyt sitten hivenen jännitti ja monta kertaa katsoin, että koneen nimen edessä todellakin lukee (env) ja että varmasti ollaan kehitysympäristössä. Kuten tunnilla painotettiin, pipillä ei saa asentaa
mihinkään muualle kuin kehitysympäristöön eikä missään nimessä käyttää sudo-komentoa asennuksessa. Muisti hieman pätki, mikä oli se syy, miksi näin ei saanut tehdä, joten google taas käyttöön ja tietoa löytyi: 
https://askubuntu.com/questions/802544/is-sudo-pip-install-still-a-broken-practice. 

Seuraavaksi kysyin, `$ which pip`, vastaus oli ohjeen mukainen (tämän ohjeen: https://terokarvinen.com/2022/django-instant-crm-tutorial/) ja siirryin seuraavaan vaiheeseen, kirjoittamaan 
tekstitiedostoon asennettavan ohjelman nimen. Micro on jo asennettuna, joten komennolla `micro requirements.txt` aukaisi tekstitiedoston, sinne kirjoitin django (ja tarkistin oikeinkirjoituksen monta kertaa).
Ja sitten oli vuorossa se jännittävä komento, `$ pip install -r requirements.txt`. 

![djangon_asennus](https://user-images.githubusercontent.com/82024427/220142660-ad19cc09-764d-4558-b138-19edb5088d97.png)

Aloitin uuden projektin komennolla `$ django-admin startproject mirkahei`, siirryin projektin kansioon `cd mirkahei` komennolla ja käynnistin serverin `./manage.py runserver # NOT FOR PROD`. Serveri käynnistyi ja terminaalissa kerrottiin serverin osoite, http://127.0.0.1:8000/. 

![django_asennettu_terminaali](https://user-images.githubusercontent.com/82024427/220144758-9d67514a-cc0d-4968-b2e8-e33f15d56aea.png)

![django_asennettu](https://user-images.githubusercontent.com/82024427/220144807-5270e99b-b24f-4921-bc48-608c83e70efe.png)

Ohjeen mukaan (https://terokarvinen.com/2022/django-instant-rm-tutorial/) seuraavana vuorossa oli adminin käyttöliittymä ja käyttäjän luonti. Ensimmäisena päivitettiin muutokset `$ ./manage.py makemigrations` ja `$ ./manage.py migrate` komennoilla. Artikkelissa ohjeistettiin asentamaan salasananluonti-ohjelma ja sen tein. Komento oli `$ sudo apt-get install pwgen` ja salasanan luontiin `$ pwgen -s 20 1`. Toki ennen käskyn antoa en tiennyt, mitä tuo komento teki. (Ja ei hätää, terminaalissa näkyvä salasana on vaihdettu jo ainakin kahdesti sovelluksessa.) Komennolla `$ ./manage.py createsuperuser` loin ensimmäisen käyttäjän. Käynnistin serverin uudelleen (`./manage.py runserver`) ja terminaali kertoi jälleen osoitteen osoitteen http://127.0.0.1:8000/. Lisäsin tuohon perään adminin, ja pääsin pääkäyttäjän kirjautumissivulle. Kirjautuminen luomillani tunniksilla onnistui. 

![admin_sivu_terminaali](https://user-images.githubusercontent.com/82024427/220147494-ab079e74-8147-4d3e-b679-38fce327b6f3.png)

![admin_sivu_nakyy](https://user-images.githubusercontent.com/82024427/220147575-e18f3295-575e-4a10-9ff2-75d89e4c27fd.png)

Kirjautuminen myös onnistui: 

![image](https://user-images.githubusercontent.com/82024427/220147808-60357832-014e-441f-8581-d29fe5c11702.png)














