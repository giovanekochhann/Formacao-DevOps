# Formacao-DevOps Alura

Formação em DevOps

1 - Virtualização e provisionamento
O que é IaC
Terraform
Ansible
AWS 

2 - Dominar conteinerização
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
COPY . . 
RUN npm install
ENTRYPOINT npm start
$ docker build -t  ./app-node:1.0


3 - Integração e entrega continua

4 - Monitoramento
