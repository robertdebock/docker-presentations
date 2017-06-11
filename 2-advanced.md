# Advanced stuff
- Variables
- Volumes
- Network
- Docker Hub
- Github and Docker Hub
- Docker Compose
- Swarm

---

# Briefly: setup

````
curl http://docker-presentor.meinit.nl:8000/keys/docker-workshop-ssh-key/docker-workshop-ssh-key
chmod 600 docker-workshop-ssh-key
ssh -i docker-workshop-ssh-key root@docker-${yourname}.meinit.nl
````

````
yum -y install docker
systemctl start docker
````

---

# Variables


````
docker run -e "variable=value" -ti alpine /bin/sh
/ # echo "${variable}"
value
/ # exit
````

----

# Use Variables to

Insert some data into a container.

````
docker run -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql
````

---

# Volumes

````
docker run -v $(pwd):/data alpine touch /data/iets.txt
docker run -v $(pwd):/data alpine ls -l /data/iets.txt
iets.txt
````

----

# Use Volumes to

Save (persit) data when the container is gone.

Think of:
- Log files
- Certificates
- Configurations

----

# Caution

Docker is not a good match for dataservices such as:
- Databases
- Fileservers

---

# Network

| Container 1 | Container 2|
|---|---|
|`docker run -ti alpine /bin/sh`|`docker run -ti alpine /bin/sh`|
|`ifconfig`|`ifconfig`|
|`ping 172.17.0.3`|`ping 172.17.0.2`|
|CTRL+C|    |
|`exit`|    |

----

# More complex

````
docker run -ti --name first-container alpine /bin/sh
````

````
docker run -ti --name second-container alpine /bin/sh
````

````
docker network create simple-network
docker network connect simple-network first-container
docker network connect simple-network second-container
````

Try `ifconfig` and `ping first-container` or `ping second-container`.

----

# How to use

To link containers like nginx -> tomcat -> mysql.

---

# Docker Compose

----

````
version: '3'

services:
  frontend:
    image: httpd
    ports:
    - "8080:80"
    volumes:
    - ./data/logs:/usr/local/apache2/logs
    - ./data/html:/usr/local/apache2/html
  database:
    image: mysql
    environment:
      -	MYSQL_ROOT_PASSWORD=my-secret-pw
````

----

# I love compose!

It gets rather complex. Even with one container.
- build details
- naming
- tcp/udp ports
- volumes
- variables
- commands
- [many more](https://docs.docker.com/compose/compose-file/).

---

# Docker Hub

````
docker build . -t robertdebock/super-vet
docker login
docker push
````

----

# Use Docker Hub

To share the effort, get feedback, give something back to the community and learn.

Don't forget to look on Docker Hub for great (and less great) examples.

---

# Auto building

It's extremely easy to automatically build images:
1. Make a GitHub or BitBucket repository with a Dockerfile in it.
2. On Docker Hub: Create -> Create Automatic Build.

---

# Swarm

````
docker swarm init --advertise-addr 1.2.3.4
````

````
docker swarm join --token $TOKEN
````

````
docker service create --replicas 3 httpd
````

----

# Why

To run containers over multiple machines.

---

# Learn

- https://training.docker.com/category/self-paced-online
- https://play.instruqt.com/competitions/docker/challenges
