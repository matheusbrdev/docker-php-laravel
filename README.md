# Ambiente PHP com Docker

## Como usar

1. Clone este projeto;

2. Faça o build da imagem no seu local:

```bash
$ sudo docker image build -f nomeDoDockerfileQueDesejaBuildar -t php-indiana-dev:versão(8.1 ou 7.3) --build-arg user=seuNomeDeUsuarioNoWsl --build-arg uid=1000 .
```

> - user = Nome do seu usuário no wsl;
> - uid = Grupo do usuário.

## Usando em um projeto:

1. Crie um container em cima da imagem buildada:

```bash
$ sudo docker container run -d --name nome-do-container -v "$(pwd)/nome-da-pasta-do-projeto":/var/www/html -p porta-de-acesso-a-aplicacao:80 nome-dado-a-imagem-buildada-acima
```

> - -v = Criando volume dos aquivos da pasta alvo para dentro do container;
> - -p = mapeamento de portas para o host e container.

## Execução de comandos dentro do container:

```bash
$ sudo docker exec nome-do-container seuComandoAqui
```

2. Caso queira manter uma sessão ativa do terminal do seu container basta digitar:

```bash
$ sudo docker exec -ti nome-do-container env TERM=xterm-256color bash -l
```
