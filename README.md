Role Name
=========

Opinionated SSH secure configuration. Mostly more strict than both 
``geerlingguy.security`` and default debian implementation.

Various SSH secure updates based on reading this article: 
https://stribika.github.io/2015/01/04/secure-secure-shell.html

What it does: 

1. Regenerates SSH host keys locally and updates them on server

   This is done for two reasons: 
   
   1. We really want to only have secure host keys, and re-generating them is 
      easier than checking their length and then re-generating them. 
   2. This role will be run before VM has good entropy pool, so keys might not 
      be very strong. Your computer probably has better entropy pool (note 
      that this is non ideal solution as, well, if your computer is compromised
      server is also compromised --- however if your machine is compromised 
      this is game over for the most part nevertheless.)
2. Sets more secure cryptography protocols in ssh config;  
3. Installs fail2ban;
   

Requirements
------------

1. You need ``ssh-keygen`` installed locally. 

Role Variables
--------------


SSH Key exchange algorithms: 
     
    secure_ssh_key_exchange_algorithms: curve25519-sha256@libssh.org,diffie-hellman-group-exchange-sha256

SSH symmetric encryption ciphers: 
    
    secure_ssh_ciphers: chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

SSH MAC algorithms:     
    
    secure_ssh_macs: hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,umac-128@openssh.com

SSH port to use: 
    
    secure_ssh_port: 22
    
Sane defaults for SSH server    
    
    secure_ssh_permit_root_login: no
    secure_ssh_password_auth: no
    
Set this to only allow logins from specified groups:      
        
    secure_ssh_user_groups: []
    
Set this to only allow logins from specified users (and/or groups):     
    
    secure_ssh_users: []
    
[1]: https://security.stackexchange.com/q/79043/7873    

Dependencies
------------

None

License
-------

BSD

Author Information
------------------

Jacek Bzdak jacek@askesis.pl
