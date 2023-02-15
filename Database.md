## Esimerkki softa

## Asenna postgresql

Olin asentanut postgresql jo tunnilla, joten aloitin luomalla uuden käyttäjän `$ sudo createuser testimirka`. Vaihdoin käyttäjää komennolla `$ su testimirka`
ja yritin käyttäjänä testimirka luoda käyttäjälle tietokannan komennolla `$ sudo -u postgres createdb testimirka`, mutta sain ilmoituksen, että testimirka ei kuulu sudoryhmään. 
Vaihdoin käyttäjän sudo-käyttäjäksi ja loin sudo-käyttäjänä testimirkalle databasen ja loin postgre-käyttäjän testimirka komennolla `$ sudo postgres createuser testimirka`. 
Vaihdoin taas käyttäjän testimirkakaksi komennolla `$ su testimirka` ja annoin komennon `$ psql`. 

![kayttajalle_testimirka_tietokannan_luonti](https://user-images.githubusercontent.com/82024427/219151619-3aadf663-2a60-486c-afcb-3d49e1c0c80b.png)

Seuraavaksi loin taulun hobbies, komento `CREATE TABLE hobbies (id SERIAL PRIMARY KEY, name VARCHAR (100));`. Id on primary key, joka generoidaan automaattisesti, ja harrastuksen
nimi, siihen voi käyttää merkkejä 100 kpl. 

![create_table_testimirka](https://user-images.githubusercontent.com/82024427/219152923-2064e1a3-4583-4067-9d78-d4c2f83608f3.png)

Seuraavaksi lisäsin tietokantaan harrastuksia. Komennolla `INSERT INTO hobbies (name) VALUES 'harrastuksen nimi';` lisäsin tauluun kolme eri harrastusta (create). Komennolla `SELECT * FROM hobbies;` 
näen taulun sisällön (read). 

![lisaa_taulukkoon_harrastuksia_nayta](https://user-images.githubusercontent.com/82024427/219154052-b156a99b-68ec-4fba-85c3-fdaf4cd75cf7.png)

Taulussa olevien tietojen päivitys tapahtuu komennolla `UPDATE hobbies SET='uusi päivitettävä tieto WHERE name='jokin taulussa oleva harrastus';` (update).

![update_taulukko](https://user-images.githubusercontent.com/82024427/219156587-f8f210d4-b32a-4188-b4ba-34cd1bbc72b7.png)

Viimeisenä vielä taulusta poisto. Poistaminen tapahtuu komennolla `DELETE FROM hobbies WHERE name='jokin tietokannassa olevista harrastuksista';` (delete).

![delete_hobbies](https://user-images.githubusercontent.com/82024427/219157028-61f47dc9-ece3-430d-bd03-50fe237a3589.png)

Komennolla `SELECT * FROM hobbies;` voi aina tarkistaa, että onhan taulun tiedot päivittyneet. 

### Lähteet: 

https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/









