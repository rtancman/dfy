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

OSX e Win vamos usar o Docker Toolbox ( https://www.docker.com/docker-toolbox ):

- OSX -> https://docs.docker.com/mac/step_one/

- WIN -> https://docs.docker.com/windows/step_one/

   Após instalar o docker toolbox precisamos iniciar a instalacao da vm com docker
   
   Você pode usar o kitematic beta ou o docker kickstart mais informações de instalação aqui https://docs.docker.com/v1.8/installation/windows/

   Depois de criar a vm com docker basta acessar o cmd e rodar

   ```dosbatch   
   
   C:\Users\mary> docker-machine ls

   C:\Users\mary> docker-machine env --shell cmd my-default
   
   C:\Users\mary> FOR /f "tokens=*" %i IN ('docker-machine env --shell cmd default') DO %i
   ```
   my-default -> é o nome da vm recem criada no virtual box

   docker-machine -> ferramenta para acesso remoto ao docker que esta rodando em outra maquina

- Outra Distro

   https://docs.docker.com/engine/installation/ubuntulinux/