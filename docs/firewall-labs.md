sudo ufw default deny incoming

sudo ufw allow 4000/tcp

sudo ufw enable

sudo ufw status verbose

(be sure to update your rules accordingly)

Skipping adding existing rule

Skipping adding existing rule (v6)

Firewall is active and enabled on system startup

Status: active

Logging: on (low)

Default: deny (incoming), allow (outgoing), disabled (routed)

New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
4000/tcp                   ALLOW IN    Anywhere                  
4001/tcp                   ALLOW IN    Anywhere                  
4002/tcp                   ALLOW IN    Anywhere                  
4000                       ALLOW IN    24.118.224.126            
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
4000/tcp (v6)              ALLOW IN    Anywhere (v6)             
4001/tcp (v6)              ALLOW IN    Anywhere (v6)             
4002/tcp (v6)              ALLOW IN    Anywhere (v6)  
