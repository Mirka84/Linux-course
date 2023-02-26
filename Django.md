## Tietokantasovelluksen teko 

Sunnuntai 19.2.2023 klo 12.00. Aloitin tietokantasovelluksen teon lukemalla ensin artikkelin https://terokarvinen.com/2022/django-instant-crm-tutorial/ ja seuraamalla artikkelissa olleita ohjeita. 
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

Loin toisen käyttäjän käyttöliittymällä ja annoin toiselle käyttäjälle yhtä kovat oikeudet, kuin itselläni. Käyttöliittymä oli erittäin selkeä käyttäjän lisäämiseen. 

![image](https://user-images.githubusercontent.com/82024427/220148127-3de0be61-c27f-49d8-85be-459af469c53a.png)

Kirjautuminen onnistui myös toisena käyttäjänä: 

![image](https://user-images.githubusercontent.com/82024427/220148400-725fceb0-c904-4e7f-8349-16d9cb90f017.png)

Sitten olikin tietokannan luonnin vuoro. Tein sovelluksen nimeltä Juomat, komento `$ ./manage.py startapp juomat`. Jotta sovellus näkyisi käyttöliittymällä, täytyi se käydä lisäämässä asetuksiin, komento `$ micro mirkahei/settings.py` avasi Microon dokumentin, jonne INSSTALLED_APPS-kohtaan lisäsin myös juomat. 

![lisataan_appi_asetuksiin](https://user-images.githubusercontent.com/82024427/220149272-bb3c3445-989b-4ee7-893b-27e2f076fff0.png)

Taulujen luonnin vuoro. `micro juomat/models.py` komento avasi Microon dokumentin, jonne kirjoitin luokan tiedot:

`class Drink(models.Model):
    name = models.CharField(max_length=50)
    description = models.CharField(max_length=200)`
 
 Minulla oli kirjoitusvirhe atribuutissa charfiel ja virheilmoitus näytettiin terminaalissa. 
 
 ![tehdaan_appi_ja_tauluja](https://user-images.githubusercontent.com/82024427/220151482-2ad4b273-e967-430a-bf5f-17f9621c080d.png)
 
 Jotta taulut näkyisivät käyttöliittymällä, muutokset täytyi taas päivittää komennolla `$ ./manage.py makemigrations` ja `$ ./manage.py migrate`. Ja vielä `$ micro juomat/admin.py`tiedostoon lisättiin teksti: 
 
 `from django.contrib import admin
from . import models
admin.site.register(models.Drink)`

![taulut_nakyy_adminissa](https://user-images.githubusercontent.com/82024427/220154439-aff25520-3019-401a-bc41-259b668cdfec.png)

Tietokantaan lisääminen onnistui ja lisäsin muutaman juoman. 

![lisataan_juomia](https://user-images.githubusercontent.com/82024427/220154722-698edc08-8686-4c99-a1d2-ddaa41346bd2.png)

Juomien nimet olivat hukassa, näkyi vain objekteja. Nimet sai lisättyä lisäämällä funktion samaan tekstitiedostoon, mihin oli kirjoitettu luokkakin. Dokumentti avautui komennolla `$ micro juomat/models.py` ja sinne lisättiin funktio  
def __str__(self):
        return self.name
        
Ja sisennykset olivat erittäin herkkiä! Tässä kesti aika kauan, että sain tekstit oikealle kohdalle ja että juomien nimet näkyivät. Mutta lopulta onnistui. 

![juomat_nakyy_tekstina](https://user-images.githubusercontent.com/82024427/220155413-6eb7a5e5-e605-45b4-8e87-93b164c36272.png)14.

Tehtävien teko päättyi n. klo 14.30. 

### Sunnuntai 26.2. klo 13.30

Tutkiskelin hieman many-to-one relationshippia ja luin tämän artikkelin: https://docs.djangoproject.com/en/4.1/topics/db/examples/many_to_one/. Lisäsin models.py-tiedostoon tekstiä: `$ micro juomat/models.py` komento avasi dokumentin. Bottle-luokalla oli ensin atribuutti name, mutta koska myös Drink-luokassa on name, niin muutin Bottle-luokan nimen bottlenameksi. Lisäsin bottlename = models.ForeignKey(Bottle, on_delete=models.CASCADE) atribuutiksi Drink-luokkaan. 

![foreign_key](https://user-images.githubusercontent.com/82024427/221410159-c59c3281-7adf-423d-9dba-4321923c27fa.png)

`$ ./manage.py makemigrations`-komennon jälkeen sain seuraavan vastauksen: 
It is impossible to add a non-nullable field 'bottlename' to drink without specifying a default. This is because the database needs something to populate existing rows.
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit and manually define a default value in models.py.
Select an option: 

Jatkoin tämän ohjeen mukaan: https://stackoverflow.com/questions/26185687/you-are-trying-to-add-a-non-nullable-field-new-field-to-userprofile-without-a. Keskustelun perusteella tulin siihen lopputulemaan, että ongelma johtuu siitä, kun yrittää muokata olemassa olevaa tietokantaa. Valitsin vaihtoehdon 1, jossa annetaan oletusarvo jo olemassa oleville juomille. Arvoksi annoin 1, eli pullon id:n. Sen jälkeen vielä annoin komennon `$ ./manage.py migrate` ja käynnistin serverin `$ ./manage.py runserver`. 

![paadyttiin_ratkaisuun_1](https://user-images.githubusercontent.com/82024427/221410727-2ffb47bb-7783-4428-8697-67356200e205.png)


![pullo_lisatty_juomalle](https://user-images.githubusercontent.com/82024427/221410650-d39d9f91-bd30-4f97-9b04-20dd44369c10.png)

Juomien tietokantaan oli ilmestynyt uusi rivi, Bottlename, ja siinä kaikilla oli valittu 0,75 l lasipullo. Vetovalikosta pystyin kuitenkin valitsemaan juomille muitakin pullovaihtoehtoja ja tallentamaan muutoksen. 

Lopetin tehtävän klo 14.37.



### Lähteet

https://terokarvinen.com/2022/django-instant-crm-tutorial/

https://askubuntu.com/questions/802544/is-sudo-pip-install-still-a-broken-practice

https://stackoverflow.com/questions/73586004/def-str-self-return-strself-name-in-model

https://groups.google.com/g/django-users/c/Fp-UEAYEiAE 

https://docs.djangoproject.com/en/4.1/topics/db/examples/many_to_one/

https://stackoverflow.com/questions/26185687/you-are-trying-to-add-a-non-nullable-field-new-field-to-userprofile-without-a


















