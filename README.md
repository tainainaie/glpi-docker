# glpi-docker
Repositório contém o passo a passo da instalação do GLPI utilizando Docker Compose.

# GLPI no Docker com Docker Compose
Guia para instalar o GLPI com Docker

## Instalando o Docker

#### 1º Atualizar lista de pacotes

O sudo apt update com privilégios de administrador é o primeiro comando que você precisa executar em qualquer sistema Linux após uma nova instalação.

~~~
sudo apt update
~~~

#### 2º Instalando pré-requisitos

Instalar os pacotes de pré-requisitos para permitir o apt o uso de pacotes seguros https.

~~~
sudo apt install apt-transport-https ca-certificates curl software-properties-common
~~~

#### 3º Adicionar chaves

Adiocionar a chave para garantir a validade de pacotes vindos do docker.

~~~
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
~~~

#### 4º Adicionar repositórios:

Adicionar o repositório do docker as fontes do ubuntu.

~~~
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
~~~

#### 5º atualizar lista de pacotes

Atualizar a lista de pacotes novamente.

~~~
sudo apt update
~~~

#### 6º Instalando o docker

Instalar o docker

~~~
sudo apt install docker-ce
~~~

#### 7º Docker em execução

Verificar se o docker está em execução.

~~~
sudo systemctl status docker
~~~

O sistema retornará a seguinte mensagem:
> Active: active(running)

#### 8º Versão

Para verificar a versão do docker execute o comando abaixo:

~~~
docker --version
~~~

#### 9º Habilitar o super admin no docker

Por padão o comando docker só pode ser executando pelo usuário usando o comando sudo e para evitar a repetição desse comando e da senha utilize:

~~~
sudo usermod -aG docker ${USER}
~~~

Para aplicar a associação do usuário ao grupo docker sem precisar sair do sistema basta digitar:

~~~
su - ${USER}
~~~

Instalação e configuração do docker concluída, próximo passo instalar o docker compose.

## Instalar o Docker Compose

### 1º Criar um diretório

Criar um diretório para o docker compose dentro do docker (diretório oculto por padrão).

~~~
mkdir -p ~/.docker/cli-plugins/
~~~

### 2º Baixar o docker compose

Baixe docker compose a partir do github.

~~~
curl -SL https://github.com/docker/compose/releases/download/v2.11.2/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
~~~

### 3º Liberar permissões

Após baixar o docker compose é necessário dar as devidas permissões para que o docker compose se torne executável.

~~~
chmod +x ~/.docker/cli-plugins/docker-compose
~~~
### 4º Verificação

Verique se o docker compose foi instalado de fato

~~~
docker compose --version
~~~

Pronto! Docker compose também finalizado.

## Instalar o GLPI

Para implantar com docker compose, você usa os arquivos docker-compose.yml e mariadb.env

Para criar o arquivo digite:
~~~
nano docker-compose.yml
~~~

### mariadb.env

~~~
MARIADB_ROOT_PASSWORD=diouxx
MARIADB_DATABASE=glpidb
MARIADB_USER=glpi_user
MARIADB_PASSWORD=glpi
~~~

### docker-compose.yml

~~~
version: "3.2"

services:
#MariaDB Container
  mariadb:
    image: mariadb:10.7
    container_name: mariadb
    hostname: mariadb
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    env_file:
      - ./mariadb.env
    restart: always

#GLPI Container
  glpi:
    image: diouxx/glpi
    container_name : glpi
    hostname: glpi
    ports:
      - "80:80"
    volumes:
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
      - /var/www/html/glpi/:/var/www/html/glpi
    environment:
      - TIMEZONE=Europe/Brussels
    restart: always
~~~




