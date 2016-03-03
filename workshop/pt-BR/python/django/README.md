# PythonPraVida
O portal PythonPraVida quer uma solução para o CMS da empresa. Vamos montar um ambiente com python e django utilizando o PostgreSQL

***OBS:*** Este workshop espera que você já tenha conhecimento sobre os comandos básicos do docker e docker-compose.
Se você esta começando a estudar docker então você deve fazer primeiro o workshop [ dockerforyou ](https://github.com/rtancman/dfy/tree/master/workshop/pt-BR/dockerforyou/workshop)


## 1) Docker hub - Vamos buscar as imagens
Vamos começar buscando as imagens que vamos utilizar para este projeto no docker hub (https://hub.docker.com/).

- Postgres https://hub.docker.com/_/postgres/
O postgres vamos usar a imagem oficial na versão latest msm ou seja basta rodar o comando abaixo:
```bash
$ docker pull postgres
```

- django https://hub.docker.com/_/django/
Vamos usar a imagem do django oficial na versão latest
```bash
$ docker pull django
```

- nginx https://hub.docker.com/_/nginx/
Vamos usar a imagem oficial também na versão latest
```bash
$ docker pull nginx
```

## 2) django modo dev - manage.py runserver
Vamos começar a rodar o django no docker utilizando o manage.py runserver. Para isso vamos precisar agora utilizar a imagem do django somente. Vou utilizar o projeto eventex (https://github.com/rtancman/eventex) para validar esse container.

- Olhando o nosso container
```bash
$ docker run -it django bash
```
Este comando vai levantar o container e trazer um console bash para agente "olhar" o nosso container django.

- Eventex
Para rodar o projeto, vamos entender o que precisamos fazer para rodar a aplicação ( https://github.com/rtancman/eventex#como-desenvolver ).

- Customizando a imagem padrão do django
Agora que já entendemos como levantar o nosso projeto de teste, precisamos realizar algumas alteraçoes na nossa imagem do django. Para isso vamos criar o nosso Dockerfile.
```Dockerfile
  FROM django
```

- Agora vamos criar o nosso docker-compose.yml
```yml

django:
 image: django
 ports:
  - "8000:8000"
 volumes:
   - ./eventex-entrypoint.sh:/usr/src/entrypoint
 entrypoint: /usr/local/bin/entrypoint
```


