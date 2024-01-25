config file: `/etc/httpd.conf`
```
# le delais maximum en secondes que le serveur attendra avant d'abandonner
Timeout 300
# le num de port dont le serveur ecoutera
Listen 80

# nombre maximum de clients maximums de clients simultanees que le serveur pourra serveur
MaxClients

# utilisateur sous lequel les processus apache s'executerons
User www

# repertoire racine a partir duquel le serveur servira les documents web
DocumentRoot /var/www/FES


```

- firewall
```
firewall-cmd --permanent --add-service=http
```