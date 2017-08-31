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

- `smtp_sasl_auth_enable = yes`  
- `smtp_sasl_security_options = noplaintext noanonymous` skip noplaintext if it doesn't wok (even though that's not recommended)  
- `smtp_sasl_password_maps = hash:/etc/postfix/sasl_password`
  
postfix get's user/password from `/etc/postfix/sasl_password` bzw. from a database generated from that `sasl_password` file  
  
- create a user/password file: `sudo touch /etc/postfix/sasl_password`  
- and add the relevant info to it: `echo "smtp.mailprovder.com [username]:[supersecretpassword] >> /etc/postfix/sasl_password`  
- restrict access for passwordfile with `sudo chmod 600 /etc/postfix/sasl_password`  
- create the database with `sudo postmap hash:/etc/postfix/sasl_password`  
- finally restart postif with: `sudo ystemctl restart postfix.service`
