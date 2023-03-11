## Skriptausta

### Uusi komento Bashilla

Aloitin tehtävien teon la klo 10. 

Ensimmäisenä tein kansion `$ mkdir skriptausta` ja siirryin kansioon `$ cd skriptausta`. Sinne tein tekstitiedoston `$ micro testataan`. Tiedostoon kirjoitin, että echo "Testataan" ja lisäsin shebangiin #! /bin/bash (tiedosto siis luetaan Bashilla). Tämän jälkeen tarkistin tiedoston oikeudet, komento `$ ls -l`. Testataan-tiedostolta puuttuu x- eli ajo-oikeudet (execute) käyttäjältä, ryhmältä ja muulta. Lisään oikeuden komennolla `$ chmod ugo+x testataan`.  Lisäyksen jälkeen komento `$ ./testataan` tulostaa terminaaliin tiedoston sisällön. 

![image](https://user-images.githubusercontent.com/82024427/224475275-43187caa-99ba-4a42-8672-8bd2bc0c3a63.png)


![image](https://user-images.githubusercontent.com/82024427/224475215-28baa83e-a79d-4bfd-a142-3c1f643463c3.png)

Nyt komento toimii ainoastaan kansiossa skriptausta, joten annan komennon `$ sudo cd testataan /usr/local/bin/`. Tämän jälkeen komennon testataan pitäisi tulostaa haluttu teksti riippumatta siitä, missä työkansiossa ollaan. 

![image](https://user-images.githubusercontent.com/82024427/224475615-5538fdae-3eba-4785-896b-a3cbf972e401.png)


