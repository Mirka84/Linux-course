## Hello World kolmella kielellä

Aloitin tehtävän teon ke 8.3. klo 17.15. 

Ensimmäisenä loin koti-tiedostooni kansion, helloworld, `$ mkdir helloworld` ja siirryin tuohon kansioon `$ cd helloworld`. Kansiossa loin tiedoston 
helloworld.py, `$ micro helloworld.py`. 

### Hello World Pythonilla

Pythonin paketit on jo asennettu edellisten tehtävien aikana. Helloworld.py-tiedostoon kirjoitin print("Hello World!"). 

![image](https://user-images.githubusercontent.com/82024427/223753496-28462dbd-5c15-4ea5-abd0-56612e9aaed5.png)

Komennolla `$ cat helloworld.py` tarkistin, mitä tuli kirjoitettua ja komento `$ python3 helloworld.py` tulosti tiedoston tekstin, Hello World!

![image](https://user-images.githubusercontent.com/82024427/223753897-7efcb65f-3740-42ff-8c56-231727b551aa.png)

### Hello World Bashilla

Nyt ei muisti pelannut, onko Bash jo asennettu, joten ensin päivitin paketit `$ sudo apt-get update` ja sen jälkeen asennus `$ sudo apt-get -y install bash`. Paketit on kuitenkin jo asennettu ja käytössä on uusin versio. 

Siirryin pakettien päivittämisen jälkeen takaisin helloworld-kansioon ja sinne loin uuden tiedoston, `$ micro helloworld.sh`. 

![image](https://user-images.githubusercontent.com/82024427/223756417-b8f296b6-6c19-4b1c-b5b8-b686afadb941.png)

Catilla taas tarkistin tekstin, `$ cat helloworld.sh` ja sieltä tulostui kirjoittamani teksi. Komento `$ bash helloworld.sh` tulosti oikein Hello World! 

![image](https://user-images.githubusercontent.com/82024427/223756691-0fd1980a-b28a-4161-9469-3a564a4ea1c2.png)

### Hello World Javalla 

Java-paketteja ei ole asennettu, joten asensin ne ensin. Apuja asennukseen etsin täältä: https://phoenixnap.com/kb/how-to-install-java-ubuntu. `$ sudo apt install default-jdk` asennettiin ensin Java Development Kit. Sen jälkeen päivitettiin ohjeen mukaisesti repository `$ sudo apt update`-komennolla ja viimeiseksi asennettiin Javan kirjastot `$ sudo apt install default-jre`. Kokonaisuudessaan asennuksen kaikissa vaiheissa meni useampi minuutti.

Asennuksen jälkeen loin tiedoston helloworld-kansioon, `$ micro HelloWorld.java`. Tiedoston nimi on siksi isolla, koska nimen pitää täsmätä tiedoon kirjoitettavaan luokan nimeen, ja luokat kirjoitetaan isolla. Tiedostoon jäi muutama kirjoitusvirhe, joita en havainnut, vaikka tarkistin tekstin myös komennolla `$ cat HelloWorld.java`. Komento `$ javac HelloWorld.java` puolestaan paljasti virheet hyvin. Olin kirjoittanut isolla public Class, ja virhe näytettiin hyvin. 

![image](https://user-images.githubusercontent.com/82024427/223765659-ad59d406-160e-4376-9402-06171bb9cf2c.png)

Korjasin virheen ja tarkistin uudelleen, ja edelleen näytti yhtä virhettä luokassa. No, luokan nimi oli kirjoitettu myös väärin, HelloWold. Uusi korjaus ja sen jälkeen virheet oli korjattu. Komento `$ java HelloWorld` tulosti halutun tekstin. 

![image](https://user-images.githubusercontent.com/82024427/223766523-627cf2dd-8c86-46d3-bcff-685fce327bb4.png)

Lopetin tehtävän teon klo 18.10. 

### Lähteet

https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

https://phoenixnap.com/kb/how-to-install-java-ubuntu

