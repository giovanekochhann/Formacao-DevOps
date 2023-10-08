# Formacao-DevOps Alura

Formação em DevOps

## 1 - Virtualização e provisionamento
O que é IaC
Terraform
Ansible
AWS 

## 2 - Dominar conteinerização
Instalação do docker sempre deve ser feita seguindo o script do site oficial, nao usar wget nem snap, usar apt-get and repositorio especifico.

Docker
hub.docker.com
$docker run hello-world
procura se existe local, senão baixa do dockerhub, roda o conteiner mostrando no terminal Hello from Docker!

Para criar grupo e não precisar chamar sudo p comando docker toda vez que for executar
$ sudo groupadd docker
$ sudo usermod -aG docker $USER

$ docker run -d -p 8080:80 dockersamples/static-site
-d mantem processo do conteiner rodando sem travar o terminal
-p mapeia portas especificas de uso do conteiner para a maquina local
-P mapeia as portas automaticamente geralmente determina portas altas para redirecionamento
este conteiner mostra um HTML rodando pelo servidor NGINX

comandos abaixo devem ser seguido do id_conteiner para identificar de qual conteiner estamos falando.
$ docker run -it ubuntu bash --> abre versao interativa de terminal com imagem do ubuntu
$ docker exec --> executa comando em cima de conteiner que ja esta rodando
$ docker pull --> baixa imagem de conteiner do dockerhub
$ docker build --> monta imagem de conteiner
$ docker start --> Iniciar conteiner que esteja montado porem parado
$ docker stop --> para a execução de um conteiner
$ docker rm --> remove conteiner --force permite parar e remover em um unico comando
$ docker port --> mostra como o mapeamento esta sendo feito
$ docker (un)pause --> comandos que pausam e retomam a pausa quando desejado
$ docker images ls --> lista conteiners baixados
$ docker inspect id --> detalhamento interno do conteiner
$ docker history id --> mostra camadas de um conteiner

Docker reutiliza camadas entre imagens.
Uma vez que exista uma imagem ela é fechada, imutável.
Um conteiner quando roda ele é read only. O que gravamos nele é apenas uma camada adicional que o docker adiciona mas a imagem original não é alterada.
Rodar diversos conteineres iguais é criar apenas uma camada de read/write para cada, o que torna o uso de conteiner muito performático

Dockerfile --> build --> imagem --> run --> conteiner

Documentação com as tags para montagem do Dockerfile
https://docs.docker.com/engine/reference/builder/

FROM node:14
WORKDIR /app-node
ARG PORT_BUILD=6000     cria variavel de ambiente permitindo personalizar a porta pelo docker file inserindo a informação no codigo da aplicação no momento do build
ENV PORT=$PORT_BUILD    permite o mesmo mapeamento do args em execucao alem do build
EXPOSE $PORT_BUILD      mostra que a aplicação esta exposta na porta 3000
COPY . . 
RUN npm install
ENTRYPOINT npm start
$ docker build -t  ./app-node:1.0

Se deseja parar todos os containeres em execução:
$ docker stop $(docker container ls -q)

PUSH da imagem para o DOCKER HUB
Autenticar usuario docker hub via terminal:
$ docker login -u [nome do usuario]
#Password: *******

cria uma copia da build, trocando o nome do repositorio para que haja match entre o nome de usuario do docker hub
$ docker tag danialartine/app-node:1.0 aluradocker/app-node:1.0 ----> aluradocker = usuario docker hub
$ docker push aluradocker/app-node:1.0
DOCKER HUB É UM GITHUB PARA CONTEINERES
O versionamento apenas atualiza as camadas do conteiner atualizadas de uma versao para outra.

### Persistencia de dados nos containeres:
- Bind Mounts: 
utilização de diretorio local da maquina host linkado com diretorio de dentro do container
$ docker run -it -v /home/gk/volume-docker:/app ubuntu bash
$ docker run -it --mount type=bind,source=/home/gk/volume-docker,target=/app ubuntu bash

- Volume (gerenciado pelo docker - nao fica dependente do sistema de arquivos, docker ajuda a gerenciar)
$ docker volume create meu-volume
$ docker run -it -v meu-volume:/app ubuntu bash
$ docker run -it --mount source=meu-novo-volume,target=/app ubuntu bash (cria o volume caso nao exista)

- Memory (tmpfs - so funciona no linux - dados sensiveis nao escritos na camada RW - ex. senha)
$ docker run -it --tmpfs=/app ubuntu bash
$ docker run -it --mount type=tmpfs,destination=/app ubuntu bash

### Comunicação atraves de redes

## 3 - Integração e entrega continua

## 4 - Monitoramento
