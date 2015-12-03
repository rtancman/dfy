# Projeto 2: Blog para empresa "Queremos um Blog maneiro"

Vamos montar um ambiente com docker utilizando NGINX, PHP 6 + PHPFPM e MariaDB. Resultado: No final teremos o WP rodando para empresa.

## 1) Selecionando os containers no docker hub ;)

1. Buscando a imagem do Debian SO base que vamos utilizar nos nossos containers.
   
   Acessando o docker hub encontramos a seguinte imagem https://hub.docker.com/_/debian/

   Agora vamos baixar para nossa maquina essa imagem ;)

   ```bash
   $ docker pull debian
   ```

2. Nginx...

   No docker hub temos https://hub.docker.com/_/nginx/

   Vamos baixar \o/

   ```bash
   $ docker pull nginx
   ```

3. MariaDB...

   No docker hub temos https://hub.docker.com/_/mariadb/

   Vamos baixar \o/
   
   ```bash
   $ docker pull mariadb
   ```

4. E por fim o php6 + fpm ...

   No docker hub temos https://hub.docker.com/_/php/

   Vamos baixar \o/
   
   ```bash
   $ docker pull php:5.6-fpm
   ```

## 2) Vamos montar o nosso docker-compose

1. Iniciando o arquivo yml com a nossa imagem do nginx

   ```yml
   
   meunginx:
     image: nginx
     ports:
      - "80:80"

   ```

   ports: E utilizado para mapear a porta da maquina host com o container q vai rodar. Ou seja, tudo que bater na porta 80 do seu pc vai direcionar para o container recem gerado no docker.

2. Adicionando o mariadb 

   ```yml
    meunginx:
      image: nginx
      links:
        - meumariadb
      ports:
        - "80:80"
    meumariadb:
      image: mariadb
      environment:
        - MYSQL_ROOT_PASSWORD=1234
   ```

   environment: E utilizado para setar variaveis de ambiente (env vars) no container ;) 

3. Vamos fazer um teste e rodar o que ja temos e verificar se os containers estao rodando 

   ```bash
   $ docker-compose up -d
   ```

   ```bash
   $ docker ps
   ```

   Tudo certo! Vamos continuar...

4. php6-fpm 

   ```yml
    meunginx:
      image: nginx
      links:
        - meumariadb
      ports:
        - "80:80"
    meumariadb:
      image: mariadb
      environment:
        - MYSQL_ROOT_PASSWORD=1234
    meuphp6fpm:
      image: php:5.6-fpm
      ports:
        - "9000:9000"
   ```

5. Vamos testar mais uma vez e verificar se os containers estao rodando 

   ```bash
   $ docker-compose up -d
   ```

   ```bash
   $ docker ps
   ```

   Esta td certo \o/ Vamos baixar o WordPress


## 2) Rodando o WordPress
