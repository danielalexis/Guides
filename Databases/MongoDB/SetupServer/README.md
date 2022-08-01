# Install MongoDB on a Server
---------
# Install all the packages

## Add the Repository Key
```sh
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
```

## Add the Repository
```sh
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

## Update Repositories and install MongoDB
```sh
sudo apt-get update
sudo apt-get install -y mongodb-org
```

## Set MongoDB to start on boot
```sh
sudo systemctl daemon-reload
sudo systemctl start mongod
sudo systemctl enable mongod
```


# Configure MongoDB

## (Optional) Allow acess from all IPs
Edit the file `/etc/mongod.conf`  
Find the followig block:
```
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1
```
And change `bindIp` to `0.0.0.0`

Your block should look like this:
```
# network interfaces
net:
  port: 27017
  bindIp: 0.0.0.0
```
Restart MongoDB to apply the new IP
```sh
sudo systemctl restart mongod
```

## Add a new admin/root user
Go into the Mongo Shell using:
```sh
mongosh
```
Use the admin database:
```sh
use admin
```
Add a new user:
```js
db.createUser({user:"admin", pwd:"password", roles:[{role:"root", db:"admin"}]})
```

Done :)
