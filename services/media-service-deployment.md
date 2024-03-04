1. Install git
```shell
# clone repository
git clone https://github.com/mazzlookman/microservices-media-service.git media-service
cd media-service/

# install all in package.json
npm install

# copy .env.example to .env
cp .env.example .env

# edit .env file
nano .env

# set HOSTNAME=this_container_ip_addr to .env
HOSTNAME=127.0.0.1

# value format for DATABASE_URL key:
DATABASE_URL=mysql://USER:PASSWORD@HOST:PORT/DATABASE?key=value&key=value

# log format see here: https://expressjs.com/en/resources/middleware/morgan.html
LOG_FORMAT=common

# create database
service mysql start
mysql -uuser_name -puser_password
mysql -umazzlookman -p*Root304
create database user_service;

# prisma generate
npx prisma generate

# run migration
npx prisma migrate deploy


# start pm2
pm2 start --name=api-gateway npm -- start

# test with curl
curl localhost:3002/users

# create proxy in nginx, which forward to http://localhost:3000
cd /etc/nginx/sites-available

cp default default.backup

nano default

# replace the contents of the nano with the configuration below
server {
  listen 80;
  listen [::]:80;
  
  location / {
    proxy_pass http://localhost:3001/;
  }
}

# check configuration status OK or !OK
nginx -t

# restart nginx
/etc/init.d/nginx restart

# start nginx
/etc/init.d/nginx start
```