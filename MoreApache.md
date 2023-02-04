## Lisää apachea

### Apachen uusi etusivu

Siirryn komennolla $ cd /etc/apache2/sites-available directoryyn, ja luon uuden tiedoston newfrontpage.conf komennolla $ micro newfrontpage.conf. Kirjotan seuraavat rivit: 
<VirtualHost *:80>
  DocumentRoot /home/mirkah/public_sites/
  <Directory /home/mirkah/public_sites/>
    require all granted
   </Directory>
</VirtualHost>. 

Seuraavaksi laitan newfrontpage.conf konfiguroinnit voimaan komennolla $ sudo a2ensite newfrontpage.conf ja suljen edellisen etusivun konfiguroinnin komennolla $ sudo a2dissite frontpage.conf. 
Viimeiseksi käynnistetään demoni uudestaan komennolla $ sudo systemctl restart apache2

![avataan_newfrontpage_suljetaan_frontpage](https://user-images.githubusercontent.com/82024427/216786586-16495fde-257d-460f-bdb9-d6b9e2e5f312.png)
