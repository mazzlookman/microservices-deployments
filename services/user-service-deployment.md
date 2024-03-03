1. Install git
```shell
# clone repository
git clone https://github.com/mazzlookman/microservices-user-service.git user-service
cd user-service/

# install all in package.json
npm install

# copy .env.example to .env
cp .env.example .env

# edit .env file
nano .env

# value format for DATABASE_URL key:
DATABASE_URL=mysql://USER:PASSWORD@HOST:PORT/DATABASE?key=value&key=value

# log format see here: https://expressjs.com/en/resources/middleware/morgan.html
LOG_FORMAT=common

# add start script
nano package.json

# create database
mysql -uuser_name -puser_password
mysql -umazzlookman -p*Root304
create database user_service;

# prisma generate
npx prisma generate

# run migration
npx prisma migrate deploy

# seed default user
# user 1 = {email:aqib@test.com, password:123, role:admin}
# user 2 = {email:ucup@test.com, password:123, role:student}
npx prisma db seed

## set HOSTNAME=this_container_ip_addr to .env
#HOSTNAME=127.0.0.1

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
    proxy_pass http://localhost:3002/;
  }
}

# restart nginx
/etc/init.d/nginx restart

# check configuration status OK or !OK
nginx -t

# start nginx
/etc/init.d/nginx start
```