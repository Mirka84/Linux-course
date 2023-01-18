# Linuxin asennus

Tehtävän suorittaminen Linuxin asennus alkoi klo 17.45. Aivan ensimmäisenä menin kurssin sivuille ja etsin sieltä ohjeet asennuksen aloittamiseen. 
Hostilla on OS käyttöjärjestelmä. 

## Virtuaalikone

Minulla oli jo koneelle asennettu Oracle VM VirtualBox, joten pääsin aloittamaan suoraan uuden virtuaalikoneen asennuksen. Asennus eteni hyvin ohjeiden mukaan. Annoin virtuaalikoneelle nimen, Debian, laitoin muistia 4000 MB, valitsin virtaalisen kovalevyn ja kovalevylle muistia suositellun 8 GB (tässä poikettiin ohjeesta ja mentiinkin sitten mönkään, siitä kohta lisää). 

![image](https://user-images.githubusercontent.com/82024427/213259569-9d1ca8fe-b637-43b2-a402-98f1eb67b09b.png)

Virtuaalikone ilmestyikin VirtualBoxiin. Tämän jälkeen latasin Debian iso imagen. Lataus alkoi klo 17.57 ja kesti 18.14 asti. 

![image](https://user-images.githubusercontent.com/82024427/213261166-2fc2fa94-7f06-4fc0-a85a-f4a9bf48fba2.png)

Kun lataus oli valmis, etenin ohjeiden mukaisesti asentamaan Debiania virtuaalikoneelle. Valitsin oikean virtuaalikoneen, sieltä asetuksista storagen, tyhjän levyn ja etsin ladatun Debianin tiedoston. Yhteenveto virtuaalikoneen tiedoista näkyi VirtaulBoxissa. Aloitin boottauksen. 

## Boottaus

Oikean virtuaalikoneen tuplaklikkauksen jälkeen näytölle ilmestyi ohjeen mukainen ruutu. Ohjeessa kerrottiin, että defaulttina oleva live-boottaus lähtisi pyörimään automaattisesti iman valintaa, mutta niin se ei itselläni tehnyt. Tässä kohtaa vaadittiin enterin painamista. Boottaus eteni hyvin mutta hitaasti. Näytöllä oli pelkkä musta ruutu, mutta onneksi alakulmassa pyöri koko ajan pieni levykkeen kuva. Tästä pystyi päättelemään, että jotain tapahtuu  koko ajan. Puuttaus alkoi klo 18.19 ja kesti 18.29 asti. Sen jälkeen sininen työpöytä ilmestyi ruudulle. 

## Testaus ja Linuxin asennus

Seuraavaksi testain ohjeen mukaan, toimiiko netti. Sovelluksista valitsin Web browserin, kävin googlettamassa itseni, valitsin yhden linkeistä, hyväksyin Googlen evästeet ja sen jälkeen suljin sivun ja nettiselaimen. Hiiri, näppis ja selain toimi. Klo 18.34 aloitin Debianin asennuksen ja klokkasin Install Debian ikonia työpöydällä. Lupasin palata kohtaan, missä mentiin virtuaalikoneen alustamisessa pieleen. Tässä siis palataan. Heti Install Debian ikonin klikkauksen jälkeen sain ruudulle ilmoituksen, että kovalevyllä on liian vähän tilaa ja asennusta asennusta ei voida jatkaa. Asennukseen tarvitaan 10 GiB kovalevylle tilaa. Ei muuta kuin siis uuden virtuaalikoneen pystytyksen kimppuun. Uusi kone sai nimekseen MHDebian 20 GB:n kovalevyllä (kuten ohjeessakin oli). Uuden virtuaalikoneen alustus eteni samalla tavalla kuin ensimmäisen, ehkä vähän nopeammin. 

## Onnistunut asennus 

Virtuaalikoneen luomisen, boottauksen ja uudelleen testaamisen jälkeen pääsin asentamaan oikeasti käyttöjärjestelmää. Asennus alkoi klo 18.56 ja eteni samalla tavalla, kuin ohjeen näytönkuvissa oli. Asennus päättyi klo 19.10, jolloin tuli ilmoitus, että All done ja Restart. Uudelleen käynnistyksen jälkeen ei tullut mustaa ruutua, vaan pääsin suoraan kirjautumissivulle ja kirjautumaan. Nettiselailu onnistui hyvin. Käyttöjärjestelmän sovellusten teksti oli muuttunut suomeksi. Yläpalkin valikot, Machine ja Device, olivat edelleen englanniksi, mutta Applications oli muuttunut Sovelluksiksi. Avasin Terminalin ja annoin ohjeen mukaiset komennot. Näissä ei ollut ongelmaa. Kieli oli välillä suomea ja välillä englantia. Ohjeen mukaiset asennukset päättyivät klo 19.50. 
