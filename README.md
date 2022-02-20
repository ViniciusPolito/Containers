# Containers

Esse repositório tem como objetivo destacar pontos principais sobre containers.

## Docker

![virt_docker](https://user-images.githubusercontent.com/41132563/154765115-020bac2d-6701-491c-b638-4f2c8c6c6020.png)

O containers do docker funcionam como processos do Windows.

### Como instalar docker no Windows? 

https://docs.docker.com/desktop/windows/install/

### Como instalar docker no Ubuntu?

https://docs.docker.com/engine/install/ubuntu/

### [Comandos](https://docs.docker.com/engine/reference/commandline/docker/)

`docker attach`	Attach local standard input, output, and error streams to a running container

`docker build`	Build an image from a Dockerfile

`docker builder`	Manage builds

`docker checkpoint`	Manage checkpoints

`docker commit`	Create a new image from a container’s changes

`docker config`	Manage Docker configs

`docker container`	Manage containers

`docker context`	Manage contexts

`docker cp`	Copy files/folders between a container and the local filesystem

`docker create`	Create a new container

`docker diff`	Inspect changes to files or directories on a container’s filesystem

`docker events`	Get real time events from the server

`docker exec`	Run a command in a running container

`docker export`	Export a container’s filesystem as a tar archive

`docker history`	Show the history of an image

`docker image`	Manage images

`docker images`	List images

`docker import`	Import the contents from a tarball to create a filesystem image

`docker info`	Display system-wide information

`docker inspect`	Return low-level information on Docker objects

`docker kill`	Kill one or more running containers

`docker load`	Load an image from a tar archive or STDIN

`docker login`	Log in to a Docker registry

`docker logout`	Log out from a Docker registry

`docker logs`	Fetch the logs of a container

`docker manifest`	Manage Docker image manifests and manifest lists

`docker network`	Manage networks

`docker node`	Manage Swarm nodes

`docker pause`	Pause all processes within one or more containers

`docker plugin`	Manage plugins

`docker port`	List port mappings or a specific mapping for the container

`docker ps`	List containers

`docker pull`	Pull an image or a repository from a registry

`docker push`	Push an image or a repository to a registry

`docker rename`	Rename a container

`docker restart`	Restart one or more containers

`docker rm`	Remove one or more containers

`docker rmi`	Remove one or more images

`docker run`	Run a command in a new container

`docker save`	Save one or more images to a tar archive (streamed to STDOUT by default)

`docker search`	Search the Docker Hub for images

`docker secret`	Manage Docker secrets

`docker service`	Manage services

`docker stack`	Manage Docker stacks

`docker start`	Start one or more stopped containers

`docker stats`	Display a live stream of container(s) resource usage statistics

`docker stop`	Stop one or more running containers

`docker swarm`	Manage Swarm

`docker system`	Manage Docker

`docker tag`	Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

`docker top`	Display the running processes of a container

`docker trust`	Manage trust on Docker images

`docker unpause`	Unpause all processes within one or more containers

`docker update`	Update configuration of one or more containers

`docker version`	Show the Docker version information

`docker volume`	Manage volumes

`docker wait`	Block until one or more containers stop, then print their exit codes

### Comandos mais utilizados

`docker ps -a` Lista containers em execução

`docker container rm $(docker container ls –aq)` Remove todos os containers

`docker container rmi $(docker container ls –aq)` Remove todas as imagens

### Como criar uma imagem?

Para criação de uma imagem, vamos utilizar o [Dockerfile](https://docs.docker.com/engine/reference/builder/#from) <br />
Os Dockerfiles são criados através de um conjunto de instruções.

`ADD`
`COPY`
`ENV`
`EXPOSE`
`FROM`
`LABEL`
`STOPSIGNAL`
`USER`
`VOLUME`
`WORKDIR`
`ONBUILD`

Existem diferentes maneiras de criar um Dockerfile. Portanto mostrar alguns exemplos.

<pre>
FROM Node:14 # Usa uma imagem base
WORKDIR /app-node # Diz o diretório padrão
COPY . . # Copia tudo da pasta onde o Dockerfile está e coloca no diretório padrão dentro da imagem
RUN npm install # Executa comando quando imagem estiver sendo criada
ENTRYPOINT npm start # Executa quando imagem estiver criada
</pre>

<pre>
FROM Node:14 
WORKDIR /app-node
ARG PORT_BUILD=6000
ENV PORT=$PORT_BUILD
EXPOSE $PORT_BUILD
COPY . . 
RUN npm install 
ENTRYPOINT npm start
</pre>

<pre>
# syntax=docker/dockerfile:1
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
</pre>

### Como persistir arquivos?

Existem 3 formas de persistir arquivos no Docker.

[volumes](https://docs.docker.com/storage/volumes/) são gerenciados pelo Docker

[bind mounts](https://docs.docker.com/storage/bind-mounts/) dependem da estrutura de pastas do host

[tmpfs](https://docs.docker.com/storage/tmpfs/) armazenam dados em memória volátil

### Docker Compose

O Docker Compose resolve o problema de executar múltiplos containers de uma só vez e de maneira coordenada, evitando executar cada comando de execução individualmente.
Ele é executado através do arquivo `docker-compose.yml`

Segue um exemplo de um arquivo Docker Compose

<pre>
version: "3.9"
services:
  mongodb:
    image: mongo:4.4.6
    container_name: meu-mongo
    networks:
      - compose-bridge

  alurabooks:
    image: aluradocker/alura-books:1.0
    container_name: alurabooks
    networks:
      - compose-bridge
    ports:
      - 3000:3000
    depends_on:
      - mongodb
    
networks:
  compose-bridge:
    driver: bridge
</pre>

## Kubernetes
