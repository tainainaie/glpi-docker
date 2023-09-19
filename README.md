# glpi-docker
Repositório contém o passo a passo da instalação do GLPI utilizando Docker Compose.

# GLPI com Docker Compose
Guia para instalar o GLPI com Docker

## Instalando o Docker

~~~
curl -fsSL https://get.docker.com | sh 
~~~


## Instalando do docker-compose

~~~
curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

~~~

## Criando diretório para presistencia de dados e baixando o repositório

~~~
mkdir opt

cd /opt 

git clone https://github.com/FALATI/glpi_docker.git

cd glpi_docker 

mkdir -p ./var/www/html/glpi \
         ./var/lib/mysql

chown 472:472 ./var/lib/mysql \
              ./var/lib/mysql 
~~~

## Executando os containers
~~~
docker-compose up -d
~~~~

Para acesar o GLPI acesse http://<seu_ip>

## Configurando GLPI
~~~
host: mysql
usuario: glpi
senha: glpi
~~~

## GLPI

~~~
usuario: glpi
senha: glpi
~~~
