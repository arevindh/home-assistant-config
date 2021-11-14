## Mosquitto Config

Change to data dir 

`mkdir -p mosquitto/config`

`sudo nano mosquitto.conf`

```
#### mosquitto.conf file contents - Dont give spaces between lines ####
persistence true
persistence_location /mosquitto/data/
#
log_dest stdout
log_dest file /mosquitto/log/mosquitto.log
#
listener 1883
allow_anonymous true
password_file /mosquitto/data/mosquitto.password_file
####################################################################

```

## Adding user in mosquitto 

Login to mosquitto container

`sudo docker exec -it mosquitto /bin/sh`

Creating a password file

To create a password file, use the mosquitto_passwd utility, use the line below. You will be asked for the password. Note that -c means an existing file will be overwritten:

`mosquitto_passwd -c <password file> <username>`

To add more users to an existing password file, or to change the password for an existing user, leave out the -c argument:

`mosquitto_passwd <password file> <username>`

To remove a user from a password file:

`mosquitto_passwd -D <password file> <username>`


## Install samba for local management 

`sudo apt update`

`sudo apt install samba`

### Add new user 

Note username should be same as your login username

`sudo smbpasswd -a username`


`sudo nano /etc/samba/smb.conf`

Add

```
server min protocol = SMB3

[ha-stack]
   comment = Home assistant
   path = /path/to/data/folder
   writable = yes
   ;guest ok = yes
   ;guest only = yes
   read only = no
   create mode = 0777
   directory mode = 0777
   force user = nobody
   create mask = 0777
   directory mask = 0777
   force user = root
   force create mode = 0777
   force directory mode = 0777
   hosts allow =
   
````

Remove 

```
map to guest = bad user
```

### Restart samba

`sudo service smbd restart`
