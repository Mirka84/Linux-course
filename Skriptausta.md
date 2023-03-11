## Skriptausta

### a) Uusi komento Bashilla

Aloitin tehtävien teon la klo 10. 

Ensimmäisenä tein kansion `$ mkdir skriptausta` ja siirryin kansioon `$ cd skriptausta`. Sinne tein tekstitiedoston `$ micro testataan`. Tiedostoon kirjoitin, että echo "Testataan" ja lisäsin shebangiin #! /bin/bash (tiedosto siis luetaan Bashilla). Tämän jälkeen tarkistin tiedoston oikeudet, komento `$ ls -l`. Testataan-tiedostolta puuttuu x- eli ajo-oikeudet (execute) käyttäjältä, ryhmältä ja muulta. Lisään oikeuden komennolla `$ chmod ugo+x testataan`.  Lisäyksen jälkeen komento `$ ./testataan` tulostaa terminaaliin tiedoston sisällön. 

![image](https://user-images.githubusercontent.com/82024427/224475275-43187caa-99ba-4a42-8672-8bd2bc0c3a63.png)


![image](https://user-images.githubusercontent.com/82024427/224475215-28baa83e-a79d-4bfd-a142-3c1f643463c3.png)

Nyt komento toimii ainoastaan kansiossa skriptausta, joten annan komennon `$ sudo cd testataan /usr/local/bin/`. Tämän jälkeen komennon testataan pitäisi tulostaa haluttu teksti riippumatta siitä, missä työkansiossa ollaan. Testaan siirtymällä pois skriptausta-kansiosta ja komento testataan tulostaa halutun tekstin myös toisessa kansiossa. Toimii siis! 

![image](https://user-images.githubusercontent.com/82024427/224475713-ac0518c8-330c-45a0-84cd-21d7f854fc72.png)

Ja sitten halusin testata seku vain, että saanko Lehmän sanomaan jotain pelkällä yhdellä komennolla. 

Asensin cowsayn, (komennot `$ sudo apt-get update` ja `$ sudo apt-get install cowsay`. Siirryin edellisellä tunnilla tehtyyn kansioon skriptausta ja muutin tekstin pelkäksi komennoksi: cowsay Heippa. 

![image](https://user-images.githubusercontent.com/82024427/224475907-3aff4c44-eb5e-4e75-94ad-feef0b4b089b.png)

Skriptausta-tiedostolla oli jo annettuna x-oikeudet, sekä oikeudet oli annettu kaikille käyttäjille. Sitten testaan, ensin skiptausta-kansiossa komennolla skriptausta, ja toimii! Siirryn vielä pois kansiosta ja testaan uudelleen skriptausta-komentoa, ja lehmä sanoo Heippa. Toimii siis! 

![image](https://user-images.githubusercontent.com/82024427/224476077-2e850d0b-4f56-4d00-9578-82c006a36b00.png)

### b) Uusi komento Pythonilla

Loin skriptausta-kansioon uuden tiedoston `$ micro pythonilla`. Sinne kirjoitin shebangiin #! /bin/python3 (jotta luetaan tiedostoa python3:lla) ja tekstiin print("Terveppä terve!"). Oikeudet tarkistin komennolla `$ ls -l`. Pythonilla-tiedostosta puuttui taas x-oikeus, joten sen lisäsin komennolla `$ chmod ugo+x pythonilla`. 

![image](https://user-images.githubusercontent.com/82024427/224476843-4eadbb3b-6aa6-4380-8617-04a79c349a5e.png)

![image](https://user-images.githubusercontent.com/82024427/224476875-7e8254f9-553f-496b-906f-8683ef4e0a6c.png)

Ja vielä korotin komennon toimimaan muissakin työhakemistoissa komennolla `$ sudo cp pythonilla /usr/local/bin/`. Sitten testailut skriptailua-kansiossa, omassa mirkah-työhakemistossa ja vielä home-työhakemistossa. Kaikkialla tulostaa halutun tekstin. 

![image](https://user-images.githubusercontent.com/82024427/224477194-969e1a68-218f-45fa-83ab-22a758296d8e.png)

### c) Uusi komento, joka tekee jotain monelle tiedostolle

Loin skriptausta-kansioon tiedoston looppaus. Apuja hain for-loopin käyttöön täältä: https://www.digitalocean.com/community/tutorials/workflow-loop-through-files-in-a-directory ja täältä https://www.cyberciti.biz/faq/bash-for-loop/. 

Looppaus-tiedostoon kirjoitin ensin

`#! /bin/bash
for FILE in skriptausta; 
do echo $FILE; 
done`

Tarkoitus oli, että tämä komento listaisi kaikki kansiossa olevat tiedostot..Testasin lohoppaus-komentoa, ei toiminut, joten lisäsin jälleen x-oikeuden `$ chmod ugo+x looppaus`. Tämän jälkeen ./looppaus tulosti terminaaliin skriptausta, mikä ei ollut tarkoitus. Avasin tiedoston `$ micro looppaus` ja muutin skriptausta tilalle mirkah. Tämä muutos ei tuottanut haluttua lopputulemaa. Lopulta vaihdoin * -merkin tilalle. Ja komento alkoi toimia. 

![image](https://user-images.githubusercontent.com/82024427/224479041-4709e8dd-8cff-4109-859d-f034439c2dd7.png)

Korotin komennon käytettäväksi missä vaan: `$ sudo cp looppau /usr/local/bin/` ja testasin etc- ja mirkah-työhakemistoissa. Komento looppaus listasi hakemistoissa olevat tiedostot. 

![image](https://user-images.githubusercontent.com/82024427/224479097-8121a458-3b42-4585-8401-ce78ccbeed28.png)

![image](https://user-images.githubusercontent.com/82024427/224479177-b8958693-d9a9-4bf7-bef9-beb67e6595b0.png)

Testasin myös komennon yhdistämistä grep-komentoon. Komento `$ looppaus | grep 'public'`toimi myös:

![image](https://user-images.githubusercontent.com/82024427/224479207-a7b61aba-d785-481d-b657-a6be1e0a4bc9.png)


### Lähteet

https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

https://terokarvinen.com/2007/shell-scripting-4/

https://www.digitalocean.com/community/tutorials/workflow-loop-through-files-in-a-directory

https://www.cyberciti.biz/faq/bash-for-loop/



