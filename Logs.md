### Logit

## /var/log/syslog

## /var/log/auth.log

Auth.log sisältää tiedon onnistuneista ja epäonnistuneista sisäänkirjautumisista ja kirjautumisyrityksistä. Samaten logi sisältää tiedon muista sudo-komentoon liittyvistä toiminnoista. 

![auth_log](https://user-images.githubusercontent.com/82024427/215325975-5c3fe3c6-6b43-4e2c-a108-be155632aafb.png)

Jan 29 14:16:58 MHDebian sudo:   mirkah : TTY=pts/0 ; PWD=/home/mirkah ; USER=root ; COMMAND=/usr/bin/tail -F var/log/auth.log. Tammikuun 29 päivä klo 14.16.58 käyttäjä mirkah on antanut sudo-komennon. 
Jan 29 14:16:58 MHDebian sudo: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=1000). UID 1000 on järjestelmän luoma tunnus ensimmäiselle käyttäjälle. UID=0 on juurikäyttäjä. 
Jan 29 14:17:01 MHDebian CRON[1555]: pam_unix(cron:session): session opened for user root(uid=0) by (uid=0). Sessio avautui, mutta samalla hetkellä myös sulkeutui. 
Jan 29 14:17:01 MHDebian CRON[1555]: pam_unix(cron:session): session closed for user root.  

### Lähteet

https://www.linuxquestions.org/questions/linux-general-1/what-is-the-user-1000-a-4175510196/






