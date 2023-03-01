# Ambiente de desenvolvimento

## Build da imagem
Depois de clonado este repositório é necessário fazer o build desta imagem:
```bash
$ docker build -f Dockerfile -t local/php-8.1:0.0.1 --build-arg user=yourUserName --build-arg uid=1000 .
```
> Este comando irá fazer o build localmente passando os argumentos requeridos pela imagem.
> - user = Nome do seu usuário;
> - uid = Identificador deste usuário.
> Estes argumentos serão usados na criação do nosso usuário dentro do container para
> evitar problemas com permissões.

## Docker compose
Agora já podemos servir nosso projeto.

1. Dentro do diretório do projeto crie um arquivo estritamente chamado `docker-compose.yml`;
```docker
version: '3.9'

services:
  app:
    image: local/php-8.1:0.0.1
    hostname: nome-para-o-seu-hostname
    container_name: nome-para-o-seu-container
    restart: always
    volumes:
      - ./:/var/www/html
    security_opt:
      - no-new-privileges:true
    ports:
      - "8000:80"
    logging:
      driver: json-file
      options:
        max-size: "100M"
        max-file: "5"
```
> Aqui estamos usando a imagem buildada para criar um container fazendo um volume
> da nossa aplicação para dentro deste container.

2. Agora basta subir o container com o docker compose:
```bash
$ docker compose up -d
```