### Installation

1. `sudo apt update`
2. `sudo apt install mailutils`  
2.1 `General Type:` **Satellite System**   
2.2 `System Mailname:` **[server_hostname]** (which is the default entry)  
2.3 `SMTP Relay host:` **smtp.[mymailprovider].com**  

### Setup

1.. `sudo dpkg-reconfigure postfix`  
1.1 skip previous settings (or change of you made a mistake)  
1.2 `Root and postmaster mail recipient:` put the emailaddress you want to receive those system message with
1.3 `SMTP relay host:` **smtp.localhost** (the default, not sure whether that'll work  
1.4 `Force synchronus updates on mail que?:` **Yes**  
1.5 `Local Networks:` **127.0.0.0/8**  
1.6 `Mailbox size limit:` **0** (the default)  
1.7 `Local address extension character:` **+** (the default)  
1.8 `Internet protocoll:` **All** (default)  



