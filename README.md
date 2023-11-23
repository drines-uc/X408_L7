# X408_L7

Get dockers test app

```
git clone https://github.com/docker/getting-started-app.git
```


## Demo 1: Basic Docker Image/Container

Lets get a dockerfile..

```
cp demo1/Dockerfile getting-started-app
```

Build an image

```
cd getting-started-app
docker build -t getting-started .
```

or

```
docker build -t getting-started getting-started-app
```

What did we make??
```
docker image ls --all
```

make an container
```
docker run -dp 127.0.0.1:3000:3000 --name=gs23 getting-started
```



## Demo 2: How to make changes to a containerized application

make a change in src/static/js/app.js

## Demo 3: Persistent Storage

Lets understand how files in containers work

```
docker run -d --name=rand1 ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
docker container ls
docker exec <containerid> cat /data.txt
```

Lets bring up another container with the same image...

```
docker run -it ubuntu ls /
```

Lets create a volume

```
docker volume ls
docker volume create todo-db
docker container ls
```

Create a container that use a the volume

```
docker run -dp 127.0.0.1:3000:3000 --name=persistgs --mount type=volume,src=todo-db,target=/etc/todos getting-started
```

Does it persist???

```
docker rm -f <continerid>
docker run -dp 127.0.0.1:3000:3000 --name=persistgs --mount type=volume,src=todo-db,target=/etc/todos getting-started
 ```

Should also metion inspecting a volume

```
docker volume inspect todo-db
```


## Demo 4: Bind Mounts

I want to use docker for development....
You can... try a bind mount

```
docker run -it --mount type=bind,src="$(pwd)",target=/src ubuntu bash
```


## Demo 5: Multi-stage Docker files & scratch builds

```
 docker build -t sc2 demo5/
 ls demo5/
 docker build -t sc2 demo5/
 docker run -dp 127.0.0.1:8080:8080 --name=scratch22 sc2
```




####AFTER INSTALLING DOCKER####
# grep /etc/group - e "docker"
# sudo usermod -aG docker $USER
# newgrp docker
#--- might need sudo groupadd docker
#######################################

################### USEFUL CMDS ################################
# List all the containers
docker container ls --all
# Start containers
docker start <container name>
# Stop container
docker stop <container name>
# Delete conntainer
docker rm <container name>
# Jump into a running container
docker exec -it <container name> <cmd>
docker exec -it t2 /bin/sh
# Specify CMD from the cmdline
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
docker run -dp 127.0.0.1:3000:3000 --name=t2 getting_started watch "echo 'this is a test'"
# Manage images
docker image ls --all
# Look at logs of running/failed containers
docker logs <name>


## USEFUL LINKS
https://docs.docker.com/engine/reference/commandline/build/








