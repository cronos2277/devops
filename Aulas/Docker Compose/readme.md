# Docker Composer
## Exemplo básico
### Exemplo básico de um docker-compose.yml
    version: '3'
    services:
        db:
            image: postgres:latest
            environment:
                POSTGRES_USER: postgres
                POSTGRES_PASSWORD: 123456

### Começando a explicação        
Sempre em toda e qualquer situação o arquivo deve se chamar `docker-compose.yml` do contrário não funcionará, uma vez que você esteja no diretório desse arquivo, você pode dar o comando `docker compose up` para subir, no caso recomenda-se rodar no modo **deamon**, caso queira que o container rode em background, usando a flag **-d**: `docker compose up -d`. Você pode parar a execução usando o comando `docker compose down`, lembre que é **compose** e não **composer**. Outro detalhe, identação importa, ou seja os tabs indicam o escopo do bloco, assim como funciona no Python, isso é um padrão do YAML.

#### version
Aqui especificamos a versão do compose, no caso do exeplo é usado a versão 3: `version: '3'` esse atributo é obrigatório e informa como o docker deve interpretar esse arquivo e a versão, apesar de ser um número deve ser informado usando o padrão estabelecido para Strings.

#### services
Aqui especificamos os seviços que irão funcionar, cuidado com a identação, todos os serviços especificados devem estar dentro dessa marcação.

#### db
Aqui estamos especificando um servico de banco de dados com o DB. No caso o nome do serviço é `db` e no interior de sua identação estamos especificando o que é esse serviço.

##### image: postgres:latest
Aqui estamos especificando uma imagem para o serviço `db`, no caso o banco de dados PostGreSQL na ultima versão, você poderia especificar uma versão fixa se fosse o caso, como por exemplo: `image: postgres:9.6`, nesse caso é carregada uma imagem com a versão 9.6 desse banco de dados.

##### environment:
Aqui estamos configurando o postgres, repare que essa marcação está no mesmo escopo que o **image** porém ele contem subatributos. Aqui é configurado o usuário para essa imagem `POSTGRES_USER`, aqui a senha `POSTGRES_PASSWORD`, se for necessário configurar outras coisas segue o link [documentação](https://hub.docker.com/_/postgres), lembrando que a configuração de usuário e senha se tornou obrigatório recentemente, quando for usar o Postgres para isso.

## Exemplo com Volumes
    version: '3'
    volumes:
        dados:
    services:
        db:
            image: postgres:latest
            environment:
                POSTGRES_USER: postgres
                POSTGRES_PASSWORD: 123456
            volumes:      
                - dados:/var/lib/postgresql/data
                - ./sql:/scripts
                - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql

### volumes:
Aqui é definido um volume, para criar um volume primeiro você precisa definir um e isso é feito aqui:

    volumes:
        dados:

Uma vez definido um volume, você pode usa-lo dentro de seu serviço, como abaixo:

    volumes:      
        - dados:/var/lib/postgresql/data
        - ./sql:/scripts
        - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql

`- dados:/var/lib/postgresql/data` => mapeando dados a esse diretório do serviço **db**.

`- ./sql:/scripts` => mapeando a pasta sql do hospeiro a pasta scripts do serviço.

`- ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql` => uma convenção do PostGreSQL para que o script execute assim que o serviço for inicializado, no caso isso é específico do PostGres e nesse caso estamos solicitando que ele execute o script **init.sql** dentro da pasta **sql**, assim que o serviço subir.

#### Mapeamento de volumes
No caso o mapeamento é sempre feito da seguinte forma `path_host`:`path_serviço`, sempre com o host na esquerda e o serviço a direita, no caso tudo que estiver no diretório de host será copiado para o diretório mapeado com o serviço, por exemplo: `- ./sql:/scripts`, ou seja tudo que estiver dentro da pasta **sql** será copiado para a pasta **scripts** do serviço, quando o mesmo for iniciado.