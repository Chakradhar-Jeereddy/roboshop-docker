## Volumes
- By default containers are ephermeral, if you remove containers, 
  data also will be deleted. For data persistance we need to use volumes.

***Types of volumes ->***
1) Named volumes -> Docker can create and manage volumes, these volumes
                    needs to be created using docker commands, before mounting it in containers.
2) Un named volumes -> If you create directories/volumes manually, we need
                       to manage them.

***Application types ->*** 
1) Sateless applications - These containers contains code only, the code is
                           stored in git (No need of volumes).
2) Statefull applications - Mongodb, redis, mysql,
                            rabbitmq are databases and need to persist data.
                            In the dockerhub images search for -v and use that to app the volume.

***Commands ->***
docker volume ls
docker volume create nginx
docker volume inspect nginx (/var/lib/docker/volumes/mongodb/_data)
docker volume rm nginx
docker run -d -p 80:80 -v nginx:/usr/share/nginx/html nginx
***Test***
docker exec -it nginx bash; echo "hello" > hello.html
cat /var/lib/docker/html/nginx
***Importatn:*** Data remains even after container restart. 
- Usage: docker volume COMMAND
create -> create a volume
Inspect -> Display detailed information on one or more volumes
ls      -> List volumes
rm     -> Remove one or more volumes





  