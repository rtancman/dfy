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

   Esta td certo \o/ ja temos todos os nossos containers para esta aplicação.

   Agora vamos rodar o WordPress, mas para que isso seja possivel vamos precisar modificar a imagem do php:5.6-fpm e é isso que vamos fazer agora ;)

## 2) Criando a nossa img para o rodar o blog utilizando o Wordpress

Precisamos instalar algumas dependencias para rodar o Wordpress para isso vamos criar uma imagem nossa que vai se basear no php:5.6-fpm

Nossa estrutura de pastas ira ficar assim:

```bash
.
├── app
│   └── wordpress
├── docker-compose.yml
├── Dockerfile
├── entrypoint
├── nginx
│   ├── app.conf
│   └── ssl
│       ├── nginx.crt
│       └── nginx.key
└── README.md
```

1. Dockerfile

   ```Dockerfile
    FROM php:5.6-fpm
    RUN apt-get update
    RUN apt-get install -y libfreetype6-dev
    RUN apt-get install -y libjpeg62-turbo-dev
    RUN apt-get install -y libmcrypt-dev
    RUN apt-get install -y libpng12-dev

   ```
   Nosso Dockerfile vai ser baseado no php:5.6-fpm ( FROM php:5.6-fpm ) e em seguida vamos começar instalar as nossas dependencias.

2. Instalando extensões do php

   ```Dockerfile
    FROM php:5.6-fpm
    RUN apt-get update
    RUN apt-get install -y libfreetype6-dev
    RUN apt-get install -y libjpeg62-turbo-dev
    RUN apt-get install -y libmcrypt-dev
    RUN apt-get install -y libpng12-dev
    
    RUN docker-php-ext-install iconv mcrypt mysql
    RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
    RUN docker-php-ext-install gd
    RUN docker-php-ext-install zip
    RUN docker-php-ext-install pdo
    RUN docker-php-ext-install pdo_mysql
   ```
   Essa imagem do php:5.6-fpm tem um script que é o "docker-php-ext-install" para instalar as extensões do php

3. Baixando o WP

   ```Dockerfile
    FROM php:5.6-fpm
    RUN apt-get update
    RUN apt-get install -y libfreetype6-dev
    RUN apt-get install -y libjpeg62-turbo-dev
    RUN apt-get install -y libmcrypt-dev
    RUN apt-get install -y libpng12-dev
    
    RUN docker-php-ext-install iconv mcrypt mysql
    RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
    RUN docker-php-ext-install gd
    RUN docker-php-ext-install zip
    RUN docker-php-ext-install pdo
    RUN docker-php-ext-install pdo_mysql

    RUN apt-get install -y wget

    RUN wget http://wordpress.org/latest.tar.gz
    RUN tar xzvf latest.tar.gz
    RUN cp wordpress/wp-config-sample.php wordpress/wp-config.php
    RUN rm -rf latest.tar.gz

   ```
   Baixando o WordPress para esta imagem
   
4. Baixando o WP

   ```Dockerfile
    FROM php:5.6-fpm
    RUN apt-get update
    RUN apt-get install -y libfreetype6-dev
    RUN apt-get install -y libjpeg62-turbo-dev
    RUN apt-get install -y libmcrypt-dev
    RUN apt-get install -y libpng12-dev
    
    RUN docker-php-ext-install iconv mcrypt mysql
    RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
    RUN docker-php-ext-install gd
    RUN docker-php-ext-install zip
    RUN docker-php-ext-install pdo
    RUN docker-php-ext-install pdo_mysql

    RUN apt-get install -y wget

    RUN wget http://wordpress.org/latest.tar.gz
    RUN tar xzvf latest.tar.gz
    RUN cp wordpress/wp-config-sample.php wordpress/wp-config.php
    RUN rm -rf latest.tar.gz

    COPY entrypoint /usr/local/bin/
    RUN chmod +x /usr/local/bin/entrypoint

    WORKDIR /var/www/html

    EXPOSE 9000

    ENTRYPOINT ["/usr/local/bin/entrypoint"]
   ```

   ENTRYPOINT -> É parecido com o CMD porém ele vai executar após a criação do container. É uma boa prática usar entrypoint ao invés de usar o CMD

5. Vamos buildar a nossa imagem do WP e criar um container
   ```bash
    $ docker build -t php56-wordpress .
    $ docker run -d --name wp php56-wordpress
    $ docker exec -it wp ls
   ```
   Após o build e criação do container, vamos ver se o wp esta nosso container usando o comando docker exec



