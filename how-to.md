### Installation

1. `sudo apt update`
2. `sudo apt install mailutils`  
2.1 `General Type:` **Satellite System**   
2.2 `System Mailname:` **[server_hostname]** (which is the default entry)  
2.3 `SMTP Relay host:` **smtp.[mymailprovider].com**  
3. `sudo dpkg-reconfigure postfix`  
3.1 skip previous settings (or change of you made a mistake)  
3.2 `Root and postmaster mail recipient:` put the emailaddress you want to receive those system message with
3.3 `SMTP relay host:` **smtp.localhost** (the default, not sure whether that'll work  
3.4 `Force synchronus updates on mail que?:` **Yes** 

### Setup
