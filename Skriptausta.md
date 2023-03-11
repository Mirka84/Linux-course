## Skriptausta

### Uusi komento Bashilla

Aloitin tehtävien teon la klo 10. 

Ensimmäisenä tein kansion `$ mkdir skriptausta` ja siirryin kansioon `$ cd skriptausta`. Sinne tein tekstitiedoston `$ micro testataan`. Tiedostoon kirjoitin, että echo "Testataan" ja lisäsin shebangiin #! /bin/bash (tiedosto siis luetaan Bashilla). Tämän jälkeen tarkistin tiedoston oikeudet, komento `$ ls -l`. Testataan-tiedostolta puuttuu x- eli ajo-oikeudet (execute) käyttäjältä, ryhmältä ja muulta. Lisään oikeuden komennolla `$ chmod ugo+x testataan`.  Lisäyksen jälkeen komento `$ ./testataan` tulostaa terminaaliin tiedoston sisällön. 

![image](https://user-images.githubusercontent.com/82024427/224475275-43187caa-99ba-4a42-8672-8bd2bc0c3a63.png)


![image](https://user-images.githubusercontent.com/82024427/224475215-28baa83e-a79d-4bfd-a142-3c1f643463c3.png)

Nyt komento toimii ainoastaan kansiossa skriptausta, joten annan komennon `$ sudo cd testataan /usr/local/bin/`. Tämän jälkeen komennon testataan pitäisi tulostaa haluttu teksti riippumatta siitä, missä työkansiossa ollaan. Testaan siirtymällä pois skriptausta-kansiosta ja komento testataan tulostaa halutun tekstin myös toisessa kansiossa. Toimii siis! 

![image](https://user-images.githubusercontent.com/82024427/224475713-ac0518c8-330c-45a0-84cd-21d7f854fc72.png)

Ja sitten halusin testata seku vain, että saanko Lehmän sanomaan jotain pelkällä yhdellä komennolla. 

Asensin cowsayn, (komennot `$ sudo apt-get update` ja `$ sudo apt-get install cowsay`. Siirryin edellisellä tunnilla tehtyyn kansioon skriptausta ja muutin tekstin pelkäksi komennoksi: cowsay Heippa. 

![image](https://user-images.githubusercontent.com/82024427/224475907-3aff4c44-eb5e-4e75-94ad-feef0b4b089b.png)



