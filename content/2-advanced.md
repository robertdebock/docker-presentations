# Advanced stuff
- Variables
- Volumes
- Network
- Docker Hub
- Github and Docker Hub
- Docker Compose

---

Open a webbrowser to:

https://katacoda.com/robertdebock

Open "Sweat & Tears with Docker"

---

# Use Variables to

Insert some data into a container.

````
docker run -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql
````

---

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

Containers can communicate with each other.

Containers can also be isolated to a specific network.

Some containers have no network at all.

----

# Exposing ports

Dockerfiles contain an EXPOSE parameter:

````
FROM httpd

EXPOSE 80 443
````

----

# Publishing ports

When running an image, you can "publish" ports. This opens TCP or UDP ports to a container.

````
docker run -p 8080:80 nginx
````

````
docker run -P nginx
````

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

Even one container can become quite complex.
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

# Learn

- https://training.docker.com/category/self-paced-online
- https://play.instruqt.com/competitions/docker/challenges
