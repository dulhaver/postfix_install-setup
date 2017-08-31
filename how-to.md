## Installation

1. `sudo apt update`
2. `sudo apt install mailutils`  
2.1 `General Type:` **Satellite System**   
2.2 `System Mailname:` **[server_hostname]** (which is the default entry)  
2.3 `SMTP Relay host:` **smtp.[mymailprovider].com**  

## Setup

1.. `sudo dpkg-reconfigure postfix`  
1.1 skip previous settings (or change of you made a mistake)  
1.2 `Root and postmaster mail recipient:` put the emailaddress you want to receive those system message with
1.3 `SMTP relay host:` **smtp.localhost** (the default, not sure whether that'll work  
1.4 `Force synchronus updates on mail que?:` **Yes**  
1.5 `Local Networks:` **127.0.0.0/8**  
1.6 `Mailbox size limit:` **0** (the default)  
1.7 `Local address extension character:` **+** (the default)  
1.8 `Internet protocoll:` **All** (default)  

### Authentifizierung am Smarthost

Wenn der SMTP-Server auf dem Smarthost zum Versenden der Mail ein Passwort verlangt, muss die eben erstellte Konfiguration /etc/postfix/main.cf allerdings noch einmal editiert [3] und diese Zeilen eingefügt werden:

smtp_sasl_auth_enable = yes
# noplaintext weglassen, wenn Passwörter im Klartext übertragen werden müssen:
# (nicht empfohlen, nur wenn's anders nicht funktioniert)
smtp_sasl_security_options = noplaintext noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_password

- Wie in der Konfigurationsdatei ersichtlich, holt Postfix die Zugangsdaten aus der Datei /etc/postfix/sasl_password bzw. aus einer Datenbank, die aus der sasl_password generiert wird. Die Datei sollte man vorzugsweise mit folgendem Befehl erstellen, da sonst ein Umwandeln in eine Datenbank nicht immer möglich ist. Dazu muss man ein Terminalfenster öffnen [2] und den folgenden Befehl eingeben:

- create a user/password file  
    `sudo touch /etc/postfix/sasl_password` and restrict access  
    `smtp.mailanbieter.de username:ganzgeheimespasswort`

- restrict access for passwordfile with `sudo chmod 600 /etc/postfix/sasl_password`

Jetzt muss noch die Datenbank erzeugt werden:

`sudo postmap hash:/etc/postfix/sasl_password`

Danach muss man postfix neu starten:

`sudo ystemctl restart postfix.service`
