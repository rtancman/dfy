# Projeto 1: Treinamento de docker + docker-compose
Vamos construir uma ambiente com docker e evoluir em seguida utilizando o docker-compose

# 1) Instalando o docker em sua maquina ;)
Para começar toda nossa jornada precisamos instalar o docker e o docker-compose na sua maquina. Para isso vamos seguir os seguintes passos:

- Meu SO é Fedora22, Debian ou Debian likes
-- Baixar o projeto dotfiles https://github.com/rtancman/dotfiles/tree/docker
-- Em seguida abrir o terminal, navegar ate o diretorio do projeto dotfiles e rodar o comando abaixo
```Shell Script
$ sudo su -
$ bash main.sh -u SEU_USUARIO_LOCAL

```
*OBS: Substituir este valor SEU_USUARIO_LOCAL para o seu usuário*

- Meu SO é WIN, OSX ou outra distro

-- OSX e Win vamos usar o Docker Toolbox ( https://www.docker.com/docker-toolbox ):
--- OSX -> https://docs.docker.com/mac/step_one/
--- WIN -> https://docs.docker.com/windows/step_one/

-- Outra Distro
--- https://docs.docker.com/engine/installation/ubuntulinux/
