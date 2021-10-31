# Install MariaDB on a Server
---------
# Install all the packages

## Install the Repository
```sh
curl -LsS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash
```

## Update Repositories and install MariaDB
```sh
sudo apt-get update
sudo apt-get install -y mariadb-server
```

## Set MariaDB to start on boot
```sh
sudo systemctl daemon-reload
sudo systemctl start mariadb
sudo systemctl enable mariadb
```


# Configure MariaDB

## (Optional) Allow acess from all IPs
Edit the file `/etc/mysql/mariadb.conf.d/50-server.cnf`  
Find the followig line:
```
bind-address            = 127.0.0.1
```
And change `127.0.0.1` to `0.0.0.0`

Your block should look like this:
```
bind-address            = 0.0.0.0
```
Restart MariaDB:
```sh
sudo systemctl restart mariadb
```


## Do the first time setup
By doing the first time setup you will be setting up the root account and cleaning some tables  
Do the first time setup using:
```sh
mysql_secure_installation
```

Note:  
```You'll probably want a new user other than root but im not going to put how to make a new user because it depends on the use case!```  
Done :)