# PythonPraVida
### O portal PythonPraVida quer uma solução para o CMS da empresa. Vamos montar um ambiente com python e django utilizando o PostgreSQL


### 1) Docker hub - Vamos buscar as imagens
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