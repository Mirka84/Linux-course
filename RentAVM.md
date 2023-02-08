## Tiivistelmä tekstistä 

### Oman virtuaalipalvelimen vuokraus 

Oman virtuaalipalvelimen vuokrausprosessi aloitettiin 7.2. pidetyllä luennolla. Yritin saada vuokrattua palvelimen Linodelta, mutta sieltä ei koskaan tullut vahvistussähköpostia. 
Päädyin siis luomaan tilin DigitalOceaniin ja sieltä palvelimen vuokraus onnistuikin hyvin. 

Palvelimen vuokraus alkoi alueen valinnalla ja Frankfurt oli valmiiksi valittuna. Seuraavaksi valittiin image: 

![image](https://user-images.githubusercontent.com/82024427/217592390-913ee5e3-3ed2-40bc-86fc-aefd32a0b27a.png)

Ja viimeisenä CPU. Valitsin ohjeen (ja toki myös hinnan) mukaan halvimman vaihtoehdon. 1 GB muistia. 

![image](https://user-images.githubusercontent.com/82024427/217593049-9fcbbf9c-d6c6-49a3-80d9-84c66e3e928b.png)

Autentikointimenetelmäksi valitsin ssh-avaimen. Lokaalissa terminaalissa annoin komennon $ ssh-key ja myös $ ssh-keygen, mutta sain virheilmoituksen ssh-keygen command not found. Tämän virheilmoituksen perusteella googlettelin, mikä voisi olla vikana. Ratkaisu löytyi tältä sivulta: https://www.thegeekdiary.com/ssh-keygen-command-not-found/. Asensin OpenSSH paketin komennolla 

`$ sudo apt-get install openssh-client` 

Valintojen jälkeen painettiin painiketta Create Droplet ja hetken kuluttua palvelimeni oli valmis. 

Alkutoimenpiteinä otin yhteyttä vuokrapalvelimeen lokaalista terminaalista: 

### Lähteet: 

https://www.thegeekdiary.com/ssh-keygen-command-not-found/

https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/






