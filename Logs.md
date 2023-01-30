## Artikkeli 

Artikkelitarjontaa oli runsaasti, joten oli hieman valinnanvaikeutta. Artikkeliksi valikoitui https://dev.to/cosimo/five-tips-to-be-a-more-effective-command-line-user-44e2, Five tips to be a more effective command-line user. 

+ Artikkeli oli tarkoitettu enemmän jo kokeneemmalle komentokehotteen käyttäjälle
+ Hyödyllisiä vinkkejä: CNTR + R, komentohistoria
+ Aliakset: usein käytettyjä pidempiä komentoja voi opettaa shellille, esim. kirjoittajan yksi esimerkki cdb = cd ..
+ Hakemistosta toiseen siirtymistä voi nopeuttaa configuroimalla .bashrc tiedostoon lyhyemmät komennot '
+ Samaten tiettyjen ohjelmien ajamisen voi automatisoida, kun siirrytään johonkin tiedostoon, esim. jonkun projektin kansioon. Shelli käynnistää tällöin automaattisesti ne ohjelmat, mitä projektissa tarvitaan. Tämä muutoskin tehdään .bashrc tiedostoon.   
+ Tehtävien suorittamista saa nopeutettua ja automatisoitua helposti, mutta tämä vaatii paljon harjoittelua ja taitojen ylläpitoa. 

## Logit

### /var/log/syslog

Syslog näyttää yleiset viestit ja tietoa koko järjestelmästä. Kaikki mitä tehdään järjestelmässä, tallentuu syslogiin.

![syslog_](https://user-images.githubusercontent.com/82024427/215330998-fdd1c20a-79b3-4860-bc2d-493ae4acdef9.png)

+ Jan 29 15:42:42 MHDebian kernel: [ 5292.980707] [UFW BLOCK] IN=enp0s3 OUT= MAC=08:00:27:e1:04:3b:52:54:00:12:35:02:08:00 SRC=178.250.2.146 DST=10.0.2.15 LEN=40 TOS=0x00 PREC=0x00 TTL=255 ID=19199 PROTO=TCP SPT=443 DPT=53712 WINDOW=0 RES=0x00 ACK RST URGP=0. **Rivi kertoo kernelistä (ytimestä) tietoa.** 
+ Jan 29 15:42:58 MHDebian rtkit-daemon[1084]: Supervising 8 threads of 4 processes of 1 users. **Deamon seuraa käyttäjätietoja, salasanoja ja käyttäjätunnuksia.**


### /var/log/auth.log

Auth.log sisältää tiedon onnistuneista ja epäonnistuneista sisäänkirjautumisista ja kirjautumisyrityksistä. Samaten logi sisältää tiedon muista sudo-komentoon liittyvistä toiminnoista. 

![auth_log](https://user-images.githubusercontent.com/82024427/215325975-5c3fe3c6-6b43-4e2c-a108-be155632aafb.png)

+ Jan 29 14:16:58 MHDebian sudo:   mirkah : TTY=pts/0 ; PWD=/home/mirkah ; USER=root ; COMMAND=/usr/bin/tail -F var/log/auth.log. **Tammikuun 29 päivä klo 14.16.58 käyttäjä mirkah on antanut sudo-komennon. Käskynantohetkellä ollaan oltu /home/mirkah -hakemistossa.** 
+ Jan 29 14:16:58 MHDebian sudo: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=1000). **UID 1000 on järjestelmän luoma tunnus ensimmäiselle käyttäjälle. UID=0 on juurikäyttäjä.** 
+ Jan 29 14:17:01 MHDebian CRON[1555]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0). **Sessio avautui, mutta samalla hetkellä myös sulkeutui.**
+ Jan 29 14:17:01 MHDebian CRON[1555]: pam_unix(cron:session): session closed for user root. 

### /var/log/apache2/access.log

Apache access.log kerää tietoa kaikista Apache-serverin tekemistä pyynnöistä. 

![apache2_log](https://user-images.githubusercontent.com/82024427/215332230-879e494d-5324-4959-991b-5ddd6e11daf2.png)

+ 127.0.0.1 - - [28/Jan/2023:21:10:55 +0200] "GET / HTTP/1.1" 200 3380 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0 **Tammikuun 28. 2023 klo 21.10.55 on käynnistetty Firefox selain.**
+ 127.0.0.1 - - [29/Jan/2023:14:29:30 +0200] "GET / HTTP/1.1" 200 3380 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0" **Tammikuun 29. 2023 klo 14.29.30 on taas käynnistetty Firefox.**

### /var/log/apache2/error.log

Apache2 error.logiin tallentuu tiedot virheiimoituksista ja kummallisuuksista. Lokitiedot ovat tallentuneet siitä lähtien, kun Apache2 on asennettu laitteelle. 

![apache2_error](https://user-images.githubusercontent.com/82024427/215332927-dd664442-3b3f-46a4-b485-cf445f13aeda.png)

+ [Sun Jan 29 14:14:38.063468 2023] [mpm_event:notice] [pid 669:tid 140366684515648] AH00489: Apache/2.4.54 (Debian) configured -- resuming normal operations **Sunnuntaina 29.1.2023 klo 14.14.38 ei virheitä, toimii normaalisti.**
+ [Sun Jan 29 14:14:38.064097 2023] [core:notice] [pid 669:tid 140366684515648] AH00094: Command line: '/usr/sbin/apache2'


### Jälki lokiin auth.log, väärä salasana sudo-komentoon sekä väärillä tiedoilla kirjautuminen

#### Väärä salasana 

+ Jan 29 15:08:20 MHDebian sudo: pam_unix(sudo:auth): authentication failure; logname= uid=1000 euid=0 tty=/dev/pts/0 ruser=mirkah rhost=  user=mirkah. Tammikuun 29. klo 15.08.20 autentikointi on epäonnistunut (syötetty väärä salasana sudo-komennossa). 
+ Jan 29 15:08:31 MHDebian sudo:   mirkah : TTY=pts/0 ; PWD=/var/log ; USER=root ; COMMAND=/usr/bin/tail -F syslog. Tammikuun 29. klo 15.08.31 annettu sudo-komento, komentohetkellä oltu /var/log-hakemistossa. Käyttäjänä pääkäyttäjä. 
+ Jan 29 15:08:31 MHDebian sudo: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=1000). Tunnisteet kirjoitettu oikein ja sessio avattu. 

#### Väärä kirjautuminen

+ **Jan 29 15:21:07 MHDebian lightdm: gkr-pam: stashed password to try later in open session.** Kirjautuessa syötetty väärä salasana. 
+ Jan 29 15:21:07 MHDebian lightdm: pam_unix(lightdm-greeter:session): session closed for user lightdm. 
+ Jan 29 15:21:07 MHDebian systemd-logind[479]: Removed session c2.
+ **Jan 29 15:21:08 MHDebian lightdm: pam_unix(lightdm:session): session opened for user mirkah(uid=1000) by (uid=0)** Järjestelmä avattu käyttäjälle mirkah. 
+ Jan 29 15:21:08 MHDebian systemd-logind[479]: New session 8 of user mirkah.


### Lähteet

https://www.linuxquestions.org/questions/linux-general-1/what-is-the-user-1000-a-4175510196/

https://stackify.com/apache-error-log-explained/

https://www.plesk.com/blog/featured/linux-logs-explained/#:~:text=Linux%20logs%20give%20you%20a%20visual%20history%20of,where%20best%20to%20put%20the%20log%20of%20events.

https://dev.to/cosimo/five-tips-to-be-a-more-effective-command-line-user-44e2






