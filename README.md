# DOCKER BASE CODE

## What are Containers?

"A container is a standard software unit that packages code and all the dependencies of a
application making it run reliably quickly from an environment
computational to the other. "docker.com

### What is Docker?

It is software that uses a container execution mechanism as a process.

## Why should I use Docker?
Because unlike virtual machines, Docker manages extremely quickly and lightly
run your containers without the need for a complete installation of an operating system. The docker
"lends" all resources, including the kernel so that its containers can be used.

#### What key points for Docker to work correctly
1. Namespaces - Process isolation
2. cgroups - Controls the resources of the operating system
3. File System - OFS (Overlay File System)

### Basic Commands

##### Containers

Run a container:

	$ docker run -it ubuntu / bin / bash

Check containers in use:
ps dockerCheck all containers:

	$ docker ps -a

Port sharing / display

	$ docker run -p 8080: 80 nginx

Run a container in the background (detached mode)

	$ docker run -d -p 8080: 80 nginx

Remove a container

	$ docker rm <id or container name> (-f if you want to force it)

Remove a container after exiting

	$ docker run --rm -p 8080: 80 nginx

Remove all containers (linux / mac / bash, etc.)

	$ docker rm $ (docker ps -a -q) -f

To access or execute a command on a container

	$ docker exec -it container-name <command or / bin / bash>
	
#### Images

List images

	$ docker images

Remove an image

	$ docker rmi <image name>
	
* NOTE: in case of any error, eg: Error response from daemon:
	
	$ docker rmi -f <image_id>

Remove all images

	$ docker rmi $ (docker images -q) -f

## Dockerfile

#### What is the Dockerfile

It is a declarative file that aims to build an image through another image.
The Dockerfile has all the structure and commands necessary for actions to be performed in the process of
"build", that is, in the process of building an image.

Example of a Dockerfile

	FROM golang: 1.14
	WORKDIR / go / src /
	COPY. .
	RUN GOOS = linux go build -ldflags = "- s -w"
	EXPOSE 8081
	ENTRYPOINT ["./main"]

## Generating an image

After creating the Dockerfile file, you can create your own image using the following command.

	$ docker build -t <image name>: <image version>.

1. The end point signals which directory the Dockerfile is located in.
2. If the version of the image is not informed, it will be automatically named "latest".

#### Publishing image to Docker Hub

Dockerhub is a repository where you can make your images available, publicly or privately.
For publication to be possible, you will first have to log in to your account
typing:

	$ docker login

After login, just push your image:

	$ docker push <image name>

## Docker-compose

### What is docker-compose

The docker-compose is a tool whose objective is to facilitate the process of executing docker containers from
declarative form. Each container runs as a service.
The file used for the docker-compose to run successfully is called docker-
compose.yaml.
Example:

	version: '3'
	services:
	nginx:
	image: nginx
	volumes:
	- ./nginx:/usr/share/nginx/html/
	ports:
	- 8080: 80
	redis:
	image: redis: alpine
	expose:
	- 6379

If you look at the example above, you will see that we have two services to perform.

1. The first is called nginx. It will use the nginx image as a base and share
volume. That is, the computer's local folder will be shared with the container. In this case, everything
exists in the computer's nginx folder, it will be automatically replicated at: / usr / share / nginx / html /
of the container. Port 8080 will also be redirected to port 80 on the container; This means that
when we access the computer: localhost: 8080 the docker will automatically redirect
of the request for port 80 of the container.

2. The second service is called redis and in this case it is extremely simple. He uses redis: alpine as
base image and exposes port 6379 of the container. This means that the nginx container will be able to
communicate on the local network created by the docker using port 6379.

#### Useful commands for docker-compose

To start the services declared in docker-compose.yml, simply execute:

	$ docker-compose up

When you execute this command, the services will be started, however, you will notice that your terminal will be
blocked, since the process is running. To execute in a detached way, just
inform the "-d" parameter at the end of the instruction.

	$ docker-compose up -d

To end the services, simply execute:

	$ docker-compose down

If you want to see in a more "organized" way only the containers of the services being executed, just
rotate:

	$ docker

# CÓDIGO BASE DOCKER

## O que são Containers?

"Um container é um padrão de unidade de software que empacota código e todas as dependências de uma
aplicação fazendo que a mesma seja executada rapidamente de forma confiável de um ambiente
computacional para o outro." docker.com

###  O que é o Docker?

É um software que utiliza um mecanismo de execução de containers como um processo.

## Por que devo utilizar o Docker?
Porque diferentemente de máquinas virtuais, o Docker consegue de forma extremamente rápida e leve
executar seus containers sem a necessidade da instalação completa de um sistema operacional. O docker
"empresta" todos os recursos, incluindo o Kernel para que seus containers possam ser utilizados.

#### Quais pontos chave para que o Docker funcione corretamente
1. Namespaces - Isolamento de processos
2. cgroups - Controla os recursos do sistema operacional
3. Sistema de Arquivos - OFS (Overlay File System)

### Comandos Básicos

##### Containers

Executar um container:

	$ docker run -it ubuntu /bin/bash

Verificar containers em utilização:
docker psVerificar todos os containers:

	$ docker ps -a

Compartilhamento / Exposição de portas

	$ docker run -p 8080:80 nginx

Executar um container em segundo plano (modo detached)

	$ docker run -d -p 8080:80 nginx

Remover um container

	$ docker rm <id ou nome do container> (-f se quiser forçar)

Remover um container após sair

	$ docker run --rm -p 8080:80 nginx

Remover todos os containers (linux/mac/bash,etc)

	$ docker rm $(docker ps -a -q) -f

Para acessar ou executar um comando em um container

	$ docker exec -it nome-do-container <comando ou /bin/bash>
#### Imagens

Listar imagens

	$ docker images

Remover uma imagem

	$ docker rmi <nome da imagem>
	
* OBS : caso der algum erro, ex : Error response from daemon:
	
	$ docker rmi -f <image_id> 

Remover todas as imagens

	$ docker rmi $(docker images -q) -f
	
## Dockerfile

#### O que é o Dockerfile

É um arquivo declarativo que tem o objetivo de construir uma imagem através de outra imagem.
O Dockerfile possui toda a estrutura e comandos necessários que ações sejam executadas no processo de
"build", ou seja, no processo de construção de uma imagem.

Exemplo de um Dockerfile

	FROM golang:1.14
	WORKDIR /go/src/
	COPY . .
	RUN GOOS=linux go build -ldflags="-s -w"
	EXPOSE 8081
	ENTRYPOINT ["./main"]

## Gerando build de uma imagem

Após a criação do arquivo Dockerfile, você poderá criar sua própria imagem utilizando o seguinte comando.

	$ docker build -t <nome da imagem>:<versao da imagem> .

1. O ponto final sinaliza em qual diretório encontra-se o Dockerfile.
2. Caso a versão da imagem não seja informada, ela será nomeada automaticamente como "latest".

#### Publicando imagem no Docker Hub

O Dockerhub é um repositório aonde você pode disponibilizar suas imagems, de forma pública ou privada.
Para que a publicação seja possível, você primeiramente você terá que realizar o login em sua conta
digitando:

	$ docker login

Realizado o login basta realizar o push de sua imagem:

	$ docker push <nome da imagem>

## Docker-compose

### O que é o docker-compose

O docker-compose é uma ferramenta cujo o objetivo é facilitar o processo de executar containers docker de
forma declarativa. Cada container é executado como um serviço.
O arquivo utilizado para que o docker-compose seja executado com sucesso chama-se por padrão docker-
compose.yaml.
Exemplo:

	version: '3'
	services:
	nginx:
	image: nginx
	volumes:
	- ./nginx:/usr/share/nginx/html/
	ports:
	- 8080:80
	redis:
	image: redis:alpine
	expose:
	- 6379

Se você verificar o exemplo acima, perceberá que teremos dois serviços a serem executados.

1. O primeiro chama-se nginx. Ele utilizará a imagem do nginx como base e fará um compartilhamento de
volume. Ou seja, a pasta local do computador será compartilhada com o container. Nesse caso, tudo que
existir na pasta nginx do computador, será automaticamente replicado no endereço: /usr/share/nginx/html/
do container. Também a porta 8080 será redirecionada para a porta 80 do container; isso significa que
quando acessarmos no computador: localhost:8080 automaticamente o docker fará o redirecionamento
da requisição para a porta 80 do container.

2. O segundo serviço chama-se redis e nesse caso é extremamente simples. Ele utiliza o redis:alpine como
imagem base e expõe a porta 6379 do container. Isso significa que o container do nginx poderá se
comunicar na rede local criada pelo docker utilizando a porta 6379.

#### Comandos úteis para o docker-compose

Para iniciar os serviços declarados no docker-compose.yml, basta executar:

	$ docker-compose up

Ao executar esse comando, os serviços serão inicializados, porém, você perceberá que seu terminal ficará
bloqueado, uma vez que o processo está sendo executado. Para executar de forma desatachada, basta
informar o parâmetro "-d" no final da instrução.

	$ docker-compose up -d

Para encerrar os serviços, basta executar:

	$ docker-compose down

Caso queira ver de forma mais "organizada" somente os containers dos serviços sendo executados, basta
rodar:

	$ docker-compose ps

E finalmente, caso queira acessar algum container, basta executar:

	$ docker-compose -it nome-do-container /bin/bash ou o comando a ser executado
