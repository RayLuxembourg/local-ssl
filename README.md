# Local-SSL
Before you start, make sure to configure conf/app.conf to serve the proper endpoints and port or static content.

### Step 1

Clone the repo cd into it.
```shell
git clone git@github.com:RayLuxembourg/local-ssl.git

cd local-ssl
```

### Step 2
Generate your private key
```shell
mkdir ssl
```

```shell
openssl genrsa -des3 -out ssl/localhost.key 2048
```
And then generate the root certificate
```shell
openssl req -x509 -new -nodes -key ssl/localhost.key -sha256 -days 1825 -out ssl/localhost.pem
```

### Step 3 
Installing the root certificate
```
sudo security add-trusted-cert -d -r trustRoot -k "/Library/Keychains/System.keychain" ssl/localhost.pem
```

### Step 4
Run your docker-compose file

```shell
docker-compose up -d
```
This will run a dockerized nginx instance and will load the conf/app.conf file as your nginx configuration