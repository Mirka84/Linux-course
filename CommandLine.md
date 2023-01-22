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

Asensin seuraavat ohjelmat: Googler, Calcurse ja Cowsay. Etsin ohjelmia komennolla apt-cache search tui/cli, mutta vaihtoehtojahan tuli terminaaliin niin paljon, ettei niistä oikein osannut mitään valita. Samaten nimet eivät suoraan kertoneet, että mistä on kysymys, joten päädyin valittuihin sovelluksiin googlettamalla erilaisia sovelluksia, joita käytetään terminaalissa. 

## Googler

![image](https://user-images.githubusercontent.com/82024427/213912722-49da35fc-1866-4761-a4d0-878c2e8da97d.png)

Sovelluksella voi googlettaa terminaalissa, jos jostain syystä ei voisi avata Firefoxia GUIlla. Avasin löytyneen linkin klikkaamalla hiiren oikeaa näppäintä ja avaamalla selaimen uudessa ikkunassa. Firefox avautui. 

## Calcurse 

![image](https://user-images.githubusercontent.com/82024427/213913000-0d3f69ec-4381-4dd2-a985-033e8b3728b4.png)

Calcurse on kalenteriohjelma. Näin lyhyellä käytöllä koin ohjelman hieman hankalaksi. Esimerkiksi kalenteriin tapahtuman lisäys vaati paljon kokeiluja, jotta kalenteriin pääsi jotain kirjoittamaan. Ohjeet eivät mielestäni olleet kovin selkeät ja ajauduinkin kokeiluissani kummallisiin valikkoihin. Käynnistin ja suljin ohjelmaa, kun huomasin ajautuneeni johonkin ihmeelliseen paikkaan, josta en päässyt pakittamaan edelliseen näyttöön. Q-näppäintä tuli siis käytettyä. 
