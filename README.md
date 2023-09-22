# glpi-docker
Repositório contém o passo a passo da instalação do GLPI utilizando Docker Compose.

# GLPI com Docker Compose
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

Pronto! Agora já é possível usar o docker para criar containers.

