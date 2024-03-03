1. Install git
```shell
# clone repository
git clone https://github.com/mazzlookman/microservices-api-gateway api-gateway
cd api-gateway/

# install all in package.json
npm install

# copy .env.example to .env
cp .env.example .env

# edit .env file
nano .env

# set HOSTNAME=this_container_ip_addr to .env
HOSTNAME=127.0.0.1

# add start script
nano package.json

# add this on scripts scope:
"start": "node src/main.js"

# start pm2
pm2 start --name=api-gateway npm -- start

# test with curl
curl localhost:3000

# create proxy in nginx, which forward to http://localhost:3000
cd /etc/nginx/sites-available

cp default default.backup

nano default

# replace the contents of the nano with the configuration below
server {
  listen 80;
  listen [::]:80;
  
  location / {
    proxy_pass http://localhost:3000/;
  }
}

# restart nginx
/etc/init.d/nginx restart

# check configuration status OK or !OK
nginx -t

# start nginx
/etc/init.d/nginx start
```