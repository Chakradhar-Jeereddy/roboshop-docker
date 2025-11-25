# Containerization has two parts
1) Build image
2) Run image/container

for i in mongodb mysql catalogue user cart shipping payment frontend; do
docker build -t $i:v1; cd ..; done

- Instread of using the loops, we can use docker compose.

Docker compose
---------------
As services are dependent on each other.
Docker Compose - It is simple yaml used to up or down the services at a time. Allows define dependencies, create network and volumes and so on.