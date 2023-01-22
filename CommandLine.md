## Linuxin komentokehotteet

Artikkeli https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited listaa hyvin päivittäisessä työskentelyssä tarvittavat 
Linuxin komentokehotteet. Artikkelissa kerrotaan, kuinka tarkistat, missä kansiossa olet työskentelemässä, kuinka tarkistat kansioiden sisällöt, liikut näiden välillä, liikuttelet kansioita/asiakirjoja toisaalle ja kopioit kansioiden sisältöjä. Käskyt eivät aivan vielä ole muistissa, mutta toivottavasti painuvat muistin syövereihin, kun tulee enemmän käytettyä Linuxia. 

## Micron asennus

Asensin micro-tekstinkäsittelyohjelman käskyllä sudo apt-get -y install micro. 

Micro tuntui heti selkeältä käyttää. Loin testidokkarin $ micro Test.txt. Micro tuntui helpommalta, kuin Nano tekstinkäsittelyohjelma. Kun tallensi, ruutuun ilmestyi teksti, että tallennettu. Nanossa tämä jäi epäselväksi. Dokkarin siirto työpöydältä uuteen luotuun kansioon oli kätevää. Mv Test.txt TESTING siirtyi TESTING kansioon. 

## Rauta

Asensin lshw ohjelman sudo apt-get -y install lshw -short -sanitize. 

![image](https://user-images.githubusercontent.com/82024427/213912573-168a8248-35bd-4092-8439-2f9507339000.png)

## Ohjelmien asennus 

Asensin seuraavat ohjelmat: Googler, Calcurse ja Cowsay. Etsin ohjelmia komennolla apt-cache search tui/cli, mutta vaihtoehtojahan tuli terminaaliin niin paljon, ettei niistä oikein osannut mitään valita. Samaten nimet eivät suoraan kertoneet, että mistä on kysymys, joten päädyin valittuihin sovelluksiin googlettamalla erilaisia sovelluksia, joita käytetään terminaalissa. Asensin ohjelmat yksitellen, mutta google kertoi, että komennolla sudo apt-get install program1 program2 program3 voi asentaa useamman ohjelman kerrallaan. 

## Googler

![image](https://user-images.githubusercontent.com/82024427/213912722-49da35fc-1866-4761-a4d0-878c2e8da97d.png)

Sovelluksella voi googlettaa terminaalissa, jos jostain syystä ei voisi avata Firefoxia GUIlla. Avasin löytyneen linkin klikkaamalla hiiren oikeaa näppäintä ja avaamalla selaimen uudessa ikkunassa. Firefox avautui. 

## Calcurse 

![image](https://user-images.githubusercontent.com/82024427/213913000-0d3f69ec-4381-4dd2-a985-033e8b3728b4.png)

Calcurse on kalenteriohjelma. Näin lyhyellä käytöllä koin ohjelman hieman hankalaksi. Esimerkiksi kalenteriin tapahtuman lisäys vaati paljon kokeiluja, jotta kalenteriin pääsi jotain kirjoittamaan. Ohjeet eivät mielestäni olleet kovin selkeät ja ajauduinkin kokeiluissani kummallisiin valikkoihin. Käynnistin ja suljin ohjelmaa, kun huomasin ajautuneeni johonkin ihmeelliseen paikkaan, josta en päässyt pakittamaan edelliseen näyttöön. Q-näppäintä tuli siis käytettyä.

## Cowsay

Kolmantena ohjelmana asensin Cowsay. Ohjelma ei taida tehdä sen kummempaa, kuin että tulostaa lehmän kuvan ja sille halutun puhekuplan. Onhan se kivan näköinen. 

![image](https://user-images.githubusercontent.com/82024427/213913113-d5486492-a630-4df9-afe8-f412761b3651.png)

## Tärkeät kansiot

/ on juurihakemisto, joka näyttää kaikki koneelle asennetut kansiot. Linuxissa ei ole eri asemia (esim. C, H), vaan kaikki kansiot sijaitsevat juurikansiossa. 

![juurihakemisto](https://user-images.githubusercontent.com/82024427/213914700-88da2ea7-59d9-487f-9bd3-dfaaafc5e3cd.png)

/home/ sisältää käyttäjien omat kansiot. Tässä virtuaalikoneessa on vain yksi käyttäjä, joten kansio sisältää mirkah-kansion. 

Komennolla cd /home/mirkah päästään käyttäjän mirkah-kansioon. LS komento näyttää, mitä mirkah-kansiossa on. 

Kansio /etc/ sisältää laitteen asetukset. 

Kansio /media/ sisältää liikuteltavia mediatiedostoja, kuten CD-rom. 

Kansio /var/log sisältää lokeihin liittyviä kansioita.

## Lähteet

https://askubuntu.com/questions/516850/is-there-any-way-to-install-multiple-software-at-a-single-command-via-terminal

https://github.com/agarrharr/awesome-cli-apps

https://www.makeuseof.com/fun-linux-command-line-programs/

https://www.wikihow.com/Run-a-Program-from-the-Command-Line-on-Linux





