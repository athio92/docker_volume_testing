# Docker-compose Volume testing

This short package is created for learning purpose. It gives examples of how to create and attach volumes using docker-compose CLI tool by defining the services and volumes in docker-compose.yml file.

The nginx server is not important - it is set-up just so `docker-compose` does not exit execution after `docker-compose up` is run, thereby giving us chance to inspect the containers and volumes being run.

## Reading
https://docs.docker.com/storage/  (for docker volume fundamentals - please understand difference between `volume` and `bind-mount`)

https://docs.docker.com/compose/reference(for docker-compose.yml  syntax guide)

## How to use this 
1. Before you start, note your docker volume conditions by running `docker volume ls`. Remember the result.
2. Go to `volume_testing` root directory
3. Build all containers with `docker-compose build`, and start containers using `docker-compose up`
4. Switch to a new terminal, and get the Container IDs of the three containers you just started using docker images test_services1, 2, and 3 by running `docker ps`
5. Run this command below to inspect and learn what is exactly the volume type created for each container. Compare with docker-compose.yml configuration to understand the syntax.

```
docker inspect [container_id] | grep -A 11 Mounts
```
6. For the container which volume type is `bind mount`, you can open a shell (`docker exec -it [container_id] sh`), cd to `/app` folder, and try to modify/create/delete files (ex: `touch testfile000.txt`). You will see that changes are synced to your laptop's `./test_folder` directory
7. Stop and remove container (`docker-compose down`) and restart again (`docker-compose up`). Then, inspect list of docker volumes (`docker volume ls`). You will see that existing named `volumes` (not `bind mount`) are remounted to a new container, while anonymous `volumes` are created anew.
