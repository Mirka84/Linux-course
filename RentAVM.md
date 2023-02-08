## Tiivistelmä tekstistä 

Teksti First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS oli erinomaisen yksityiskohtainen ohjeistus siihen, miten aloitetaan oman yksityisen virtuaalikoneen käyttö. 

Ohjeistuksessa oli selkeästi kerrottu, miten saadaan yhtyes tuohon virtuaalikoneeseen ja kuinka tuota virtuaalikonetta voidaan käyttää omasta lokaalista terminaalista. Lähes kaikki artikkelin vaiheet tulevat läpikäytyä omissa tehtävissä. 

Artikkelissa kerrotut stepit olivat yksinkertaisia ja selkeitä. Aloittelijakin pärjää niillä. Stepit oli hienosti jaettu: 
- yhteyden ottaminen
- palomuurin asentaminen
- käyttäjän luonti 
- rootin sulkeminen
- sovellusten päivittäminen ja upgreidaus
- käyttäjän oma valintaisen serverin asennus. 

### Oman virtuaalipalvelimen vuokraus 

Oman virtuaalipalvelimen vuokrausprosessi aloitettiin 7.2. pidetyllä luennolla. Yritin saada vuokrattua palvelimen Linodelta, mutta sieltä ei koskaan tullut vahvistussähköpostia. 
Päädyin siis luomaan tilin DigitalOceaniin ja sieltä palvelimen vuokraus onnistuikin hyvin. 

Palvelimen vuokraus alkoi alueen valinnalla ja Frankfurt oli valmiiksi valittuna. Seuraavaksi valittiin image: 

![image](https://user-images.githubusercontent.com/82024427/217592390-913ee5e3-3ed2-40bc-86fc-aefd32a0b27a.png)

Ja viimeisenä CPU. Valitsin ohjeen (ja toki myös hinnan) mukaan halvimman vaihtoehdon. 1 GB muistia. 

![image](https://user-images.githubusercontent.com/82024427/217593049-9fcbbf9c-d6c6-49a3-80d9-84c66e3e928b.png)

Autentikointimenetelmäksi valitsin ssh-avaimen. Lokaalissa terminaalissa annoin komennon `$ ssh-key` ja myös `$ ssh-keygen`, mutta sain virheilmoituksen ssh-keygen command not found. Tämän virheilmoituksen perusteella googlettelin, mikä voisi olla vikana. Ratkaisu löytyi tältä sivulta: https://www.thegeekdiary.com/ssh-keygen-command-not-found/. Asensin OpenSSH paketin komennolla `$ sudo apt-get install openssh-client`. Asennuksen jälkeen tein komennon `ssh-keygen`, siirryin .ssh-kansioon komennolla `cd .ssh`, tarkistin kansion sisällä olevat tidosto `ls` komennolla ja avasin julkisen avaimen tiedoston `micro id_rsa.pub` ja kopioin julkisen avaimen ja liitin DigitalOceanin sivuille. 

Valintojen jälkeen painettiin painiketta Create Droplet ja hetken kuluttua palvelimeni oli valmis. 

Alkutoimenpiteinä otin yhteyttä vuokrapalvelimeen lokaalista terminaalista: `ssh root@167.71......` ja yhteyden muodostaminen onnistui. 
Seurasin Tero Karvisen ohjeita https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Ensimmäisen yhteyden muodostaminen tapahtui heti luennon jälkeen, enkä huomannut ottaa tilanteesta kuvaa, mutta muistelen, että tässä käytettiin myös ssh-avainta, enkä antanut salasanaa. 

Seuraavana vuorossa oli palomuurin asennus `$ sudo apt-get install ufw`, aukon tekeminen palomuuriin `$ sudo ufw allow 22/tcp` ja palomuurin päälleasettaminen `$ sudo ufw enable`. Nämä komennot menivät läpi hienosti. 

![kuva_vuokrakoneen_kayttajasta](https://user-images.githubusercontent.com/82024427/217602169-fc6bf39f-e4ff-4561-9c12-67d0a5414778.png)

Loin kaksi käyttäjää, mirkan ja jalmarin. Käyttäjien luonnit tein komennolla `$ sudo adduser mirka`, annoin salasanat ja koko nimen, muita tietoja en käyttäjille täyttänyt. Tässä kohtaa vähän jännitti, koska mielestäni näppäilin jotain salasanan annossa väärin. Terminaali kuitenkin ilmoitti, että salasana ja sen uudelleen kirjoitus olivat onnistuneet. Korotin mirkalle sudo-oikeudet, `$ sudo adduser mirka sudo`. Ja mielestäni rootilta ei pyydetty salasanaa missään sudo-komennossa. 

Sitten oli vuorossa käyttäjien testaus. Tässä ilmenikin sitten haastetta. Avasin uuden terminaalin, ja yritin testata käyttäjät. Annoin komennon `ssh mirka@167.71....`, eli käyttäjä + @ + koneen IP-osoite. Sain virheilmoituksen Permission denied (publickey). 

![uuden_kayttajan_testaus_toisessa_terminaalissa_esto](https://user-images.githubusercontent.com/82024427/217608297-f7e71527-0dd8-4b9c-b7bd-3b3bd09c806f.png)

Googlettelin tuota virheilmoitusta, ja kokeilin sivun https://askubuntu.com/questions/311558/ssh-permission-denied-publickey ohjetta antaa komento 
`ssh-copy-id -i ~/.ssh/id_res.pub -p 22 mirka@167.71....`, mutta tämä  ei auttanut. Sitten päädyin antamaan sillä terminaalilla, missä yhteys vuokrakoneeseen oli, komennon `su - mirka`, ja käyttäjähän vaihtui mirkaksi. Samalla komenolla yritin kääntää taas käyttäjän takaisin rootiksi. Tässä pyydettiin salasanaa, ja oletan, että se oli rootin salasana. Ja sellaista en mielestäni antanut. Joten tästä syystä jatkoin sitten käyttäjänä mirka. Korotin käyttäjän jalmarikin sudoksi  siitä syystä, että halusin varmistaa käyttäjälle mirka annetun salasanan toimivuuden. 

![jalmari_lisatty_sudoksi](https://user-images.githubusercontent.com/82024427/217606171-d260cb46-af08-447d-9025-5d0115108c81.png)

Käyttäjä mirka sulki rootin komennolla `$ sudo usermod --lock root`, päivitti paketit `$ sudo apt-get update` ja `$ sudo apt-get upgrade`. Tämän jälkeen vuorossa on serverin asennus. Ensin kuitenkin tein palomuuriin jälleen aukon `$ sudo ufw allow 80/tcp` ja asensin Apache2, `$ sudo apt-get install apache2`. Testasin `$ curl localhost` ja sain vastaukseksi Apachen aloitussivun tekstin. Muokkasin tuota aloitussivun tekstiä, komento `$ echo Moi vaan | sudo tee /var/www/index.html` ja testasin `$ curl localhost`. Tämä palautti Moi vaan. 

![terminaali_kuva_localhostin_tekstista](https://user-images.githubusercontent.com/82024427/217608028-ca77dde3-005e-4a8b-8497-3cb65dae7975.png)

![kuva_Vuokrakoneen_localhostista](https://user-images.githubusercontent.com/82024427/217608069-9eecc6bd-9f5c-4482-b63b-2e1e59ff9f08.png)

### Merkkejä tunkeutumisyrityksistä 




### Lähteet: 

https://www.thegeekdiary.com/ssh-keygen-command-not-found/

https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/

https://askubuntu.com/questions/311558/ssh-permission-denied-publickey






