# Projeto 1: Treinamento de docker + docker-compose

Vamos construir uma ambiente com docker e evoluir em seguida utilizando o docker-compose

## 1) Instalando o docker em sua maquina ;)

Para começar toda nossa jornada precisamos instalar o docker e o docker-compose na sua maquina. Para isso vamos seguir os seguintes passos:

#### Meu SO é Fedora22, Debian ou Debian likes
- Baixar o projeto dotfiles https://github.com/rtancman/dotfiles/tree/docker
- Em seguida abrir o terminal, navegar ate o diretorio do projeto dotfiles e rodar o comando abaixo

```bash
$ sudo su -
$ bash main.sh -u SEU_USUARIO_LOCAL
```

**OBS: Substituir este valor SEU_USUARIO_LOCAL para o seu usuário**

#### Meu SO é WIN, OSX ou outra distro

- OSX e Win vamos usar o Docker Toolbox ( https://www.docker.com/docker-toolbox ):

OSX -> https://docs.docker.com/mac/step_one/

WIN -> https://docs.docker.com/windows/step_one/

- Outra Distro

https://docs.docker.com/engine/installation/ubuntulinux/


## 2) Vamos rodar os comandos mais usados
**OBS: Vamos entender melhor assim que criarmos o primeiro container de teste**

#### Trabalhando com imagens
- Vai listar as imagens que você tem disponível em sua maquina.
```bash
$ docker images
```
- Vai baixar uma imagem no docker hub.
```bash
$ docker pull IMAGE
```
**docker hub** é o "github" do docker, é um repositorio de imagens para o docker. Lá você pode encontrar ou disponibilizar imagens para o mundo ;)


#### Trabalhando com containers

- ps: Vai listar os containers que estão rodando.
```bash
$ docker ps
```

- ps -a: Vai listar todos os containers os estão rodando e os que estão parados.
```bash
$ docker ps -a
```

- ps -a | grep Exit: Vai listar todos os containers que estão parados.
```bash
$ docker ps -a | grep Exit
```

- run: Vai criar um container com base em uma imagem.
```bash
$ docker run IMAGEM
```

- stop: Vai parar o container. 
```bash
$ docker stop CONTAINER ID ou NAME
```

- start: Vai reiniciar um container que foi parado.
```bash
$ docker start CONTAINER ID ou NAME
```

- pause: Vai pausar um container.
```bash
$ docker pause CONTAINER ID ou NAME
```

- unpause: Vai continuar com a execucao de um container que foi pausado.
```bash
$ docker unpause CONTAINER ID ou NAME
```

- kill: Vai matar um container.
```bash
$ docker kill CONTAINER ID ou NAME
```

- rm: Vai remover um container.
```bash
$ docker rm CONTAINER ID ou NAME
```

**Dica de um comando que é bem utilizado**
- Vai matar e remover todos os containers que estao rodando.
```bash
$ docker kill $(docker ps -a -q ) && docker rm $(docker ps -a -q )
```

## 3) Vamos começar a rodar docker a VERAAAAA!!!!
1. Primeiro vamos baixar a imagem do Debian SO base que vamos utilizar nos nossos containers.
   ```bash
   $ docker pull debian
   ```
   **OBS:** Isso não é magia, lembra que agente falou do docker hub? Então essa imagem do Debian esta hospedada lá. Basta acessar https://hub.docker.com/ e buscar ;)

2. Após baixar as imagem, vamos verificar se ela esta disponível para criar o nosso primeiro container
    ```bash
    $ docker images
    ```

3. Agora vamos criar o nosso primeiro container
   ```bash
   $ docker run --name="meuprimeirocontainer" debian
   ```
   **OBS:** Este comando vai criar o container mais ele vai parar porque não existe nenhum serviço rodando. É ae que começa a cair a ficha, "o docker é um framework para criar SaaS" 

4. Agora vamos criar um novo container
   ```bash
   $ docker run -d --name="meumemcached" memcached
   ```
   **OBS:** Caso você não tenha essa imagem o comando **docker run** ira baixar como o comando **docker pull** 

   Com -d vamos rodar esse container em background.

5. Agora vamos ver se o nosso container esta rodando normalmente
   ```bash
   $ docker ps
   ```

6. Agora vamos rodar comandos
   ```bash
   $ docker exec -it meumemcached ls

   $ docker exec -it meumemcached bash
   ```

7. Agora vamos descobrir o ip do nosso container
   ```bash
   docker inspect --format '{{ .NetworkSettings.IPAddress }}' meumemcached
   ```

8. Agora que temos um container rodando podemos fazer os testes rodando os comandos pause, unpause, stop e start
   ```bash
   $ docker pause meumemcached
   $ docker unpause meumemcached
   $ docker stop meumemcached
   $ docker start meumemcached
   ```

9. Vamos matar e remover este container recem criado 
   ```bash
   $ docker kill meumemcached
   $ docker rm meumemcached
   ```

## 4) Vamos fazer este exemplo agora utilizando o docker-compose
O docker-compose ( https://github.com/docker/compose ) é uma ferramenta para facilitar os comandos do docker.

É muito utilizada e facilita o gerenciamento de multi containers.

Nela utilizamos um arquivo yml vai descrever como levantar um container. 

Foi baseada no projeto fig ( http://www.fig.sh/ ) 

Artigo ( http://blog.docker.com/2015/02/orchestrating-docker-with-machine-swarm-and-compose/ ) fala um pouco sobre as ferramentas que temos no docker e explica de onde veio o docker-compose 

1. Vamos montar o yml para o nosso container memcached:
   ```yml
   meumemcached:
     image:  memcached
   ```
   Vamos salvar em um arquivo chamado docker-compose.yml

2. Agora vamos rodar o docker-compose:
   ```bash
   $ docker-compose up -d
   ```

3. Vamos verificar se o container de memcached esta rodando:
   ```bash
   $ docker ps
   ```

4. Vamos matar esse container utilizando o docker-compose:
   ```bash
   $ docker-compose kill
   ```

5. Vamos remover esse container utilizando o docker-compose:
   ```bash
   $ docker-compose rm
   ```

6. Vamos agora criar outro arquivo com mais um servico utilizando o docker-compose:
   ```yml
   meumemcached:
     image: memcached
   meuredis:
     image: redis
   ```
   Vamos salvar em um arquivo chamado docker-compose-com-redis.yml

7. Agora vamos rodar o docker-compose novamente com o parametro -f:
   ```bash
   $ docker-compose -f docker-compose-com-redis.yml up -d
   ```
   Neste caso se você não tiver a imagem do redis ele também ira baixar.

   O parametro **-f** é utilizado para dizer ao docker-compose que o yml a ser rodado não segue o nome docker-compose.yml

   Por este motivo precisamos sempre passar o nome do novo arquivo no caso docker-compose-com-redis.yml

## 5) Dockerfile http://docs.docker.com/engine/reference/builder/

Vamos criar um Dockerfile que vai ser baseado no debian rodando o flask 

1. Vamos criar o nosso
   ```Dockerfile
   FROM debian
   ```
   FROM representa em qual container vamos nos basear para continuar construindo a nossa imagem.

2. Instalando o python
   ```Dockerfile
   FROM debian
   RUN apt-get update
   RUN apt-get install python2.7 python-pip -y
   ```
   RUN vai executar o qualquer comando para construir a nossa imagem com as nossas dependencias, nesse caso vai instalar o python

3. Instalando o pip e o flask
   ```Dockerfile
   FROM debian
   RUN apt-get update
   RUN apt-get install python2.7 python-pip -y
   RUN mkdir app
   RUN pip install gunicorn
   RUN pip install flask
   ADD app.py /app/
   WORKDIR /app/
   ```
   ADD vai adicionar algum arquivo ou diretorio na imagem
   WORKDIR vai apontar o diretorio padrao a ser chamado quando vc for criar um container

4. Rodando o flask
   ```Dockerfile
   FROM debian
   RUN apt-get update
   RUN apt-get install python2.7 python-pip -y
   RUN mkdir app
   RUN pip install gunicorn
   RUN pip install flask
   ADD app.py /app/
   WORKDIR /app/
   EXPOSE 8000
   CMD ["python2.7","app.py"]
   ```
   EXPOSE vai expor a porta 8000 do container

   CMD vai executar um comando assim que o container for criado


5. Vamos buildar uma nova imagem e criar o nosso container
   ```bash
   $ docker build -t minhaprimeiraimagem .
   $ docker run -p 5000:5000 -d --name meunovocontainer minhaprimeiraimagem
   $ docker ps
   ```
   -p -> vai apontar a porta 8000 do host para 800 do container
   --name -> da o nome ao container

6. Vamos mapear um volume agora
   ```bash
   $ docker rm -f meunovocontainer
   $ docker run -p 5000:5000 -v `pwd`/app.py:/app/app.py -d --name meunovocontainer minhaprimeiraimagem
   $ docker ps
   ```
   -v -> vai mapear o seu app.py da maquina host com o que esta no container /app/app.py

## 6) Uhulll terminamos o projeto 1
Se você chegou até aqui primeiramente...

#### PARABÉNS!!!!

Já podemos dizer que você tem o poder do Docker em suas mãos!

Vamos continuar? Toca para o projeto 2!
[Clique aqui para ver o Projeto 2](https://github.com/rtancman/dfy/tree/master/workshop/dockerforyou/workshop/projeto2)
