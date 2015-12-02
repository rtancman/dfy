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