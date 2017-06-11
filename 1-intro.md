# Docker

---

# What is it?

----

# Terminology

- Container
- Image
- Volume

----

# Use cases

- Packaging, including environment.
- Runtime environment.
- Everything as code.

----

# Examples

## CD/CI

When building artifacts, like RPMS, containers give a predictable environment.

## Microservices

When your environment is broken in to -many- parts.

----

# It's not

- A new concept
- The same a virtual machine
- Very mature, features are added constantly

---

# Lets try!

https://www.katacoda.com/robertdebock

---

# Debugging

When things run differently than expected, you have these options:

````
container=$(docker ps -alq)

docker logs ${container}
docker exec -ti ${container} /bin/sh
docker inspect ${container}
````

---

# Conclusion

- What is it?
- Building an image
- Running an image

---

# Learn

- https://training.docker.com/category/self-paced-online
- https://play.instruqt.com/competitions/docker/challenges
- http://training.play-with-docker.com

---

# Next

- Variables
- Volumes
- Network
- Docker Hub
- Github and Docker Hub
- Docker Compose
- Swarm/Kubernetes
