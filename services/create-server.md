#### 1. Create Ubuntu Linux Container
```shell
docker run -d -it -p 2802:80 --name service-name mazzlookman/ubuntu-server
```

#### 2. Connect to Ubuntu container command line
```shell
docker exec -it --user root service-name /bin/bash
```