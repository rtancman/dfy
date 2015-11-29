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


## 2) Vamos rodar os comandos mais usandos
**OBS: Vamos entender melhor assim que criarmos o primeiro container de teste**

#### Trabalhando com imagens
```bash
Vai listar as imagens que você tem disponível em sua maquina.

$ docker images
```

```bash
Vai baixar uma imagem no docker hub. 

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

#### Vamos começar a rodar docker a VERAAAAA!!!!