# Docker Postgres projeto

## Executando
no teminal digite `docker-compose up -d`

## Veficando execução
    docker-composer ps

## Executando comando dentro do Container do PostGreSQL
    docker-compose exec db psql -U postgres -c '\l'

### Explicando
`docker-compose exec` => o camando do docker.

`db` => nome do serviço definido dentro do [docker-compose](docker-compose.yml)

`psql -U postgres -c '\l'` => comando CLI do PostGresSQL.

## Encerrando
use o comando `docker-compose down` para que todos os containers em execução sejam paralizados, repare que os comandos tem em sua composição a palavra **compose** e não **composer**, cuidado com o r para não errar o comando.