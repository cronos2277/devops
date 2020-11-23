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

### PGDATA
    db:
    image: postgres:9.6
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: 123456 
      PGDATA: /tmp            

No se faz necessário colocar o `PGDATA: /tmp` para que funcione no docker do windows, isso ocorre porque o docker usa o tmp do sistema operacional e como o sistema não tem esse diretório, logo isso ocasiona problema em ambiente windows, por isso essa propriedade é interessante.

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

### Porta
    version: '3'
    volumes:
        dados:
    services:
    db:
        image: postgres:9.6
        environment:
            POSTGRES_USER: postgres
            POSTGRES_PASSWORD: 123456
        volumes:      
          - dados:/var/lib/postgresql/data
          - ./sql:/scripts
          - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql
    frontend:
        image: nginx:1.13
        volumes:
          - ./web:/usr/share/nginx/html
        ports:
          - 80:80

### Explicando
Como pode-se perceber tem um segundo serviço agora que no caso é o front-end:

    frontend:
        image: nginx:1.13
        volumes:
            - ./web:/usr/share/nginx/html
        ports:
            - 80:80

Nesse exemplo foi especificado uma versão de maneira fixa, no caso `nginx:1.13`, foi mapeado a pasta web a pasta html do container e além disso especificado uma porta, lembrando sempre que a esquerda está a porta do hospedeiro e a direita a do container, no caso a porta **80** da maquina mapeada a porta **80** do container. Seja para mapeamento de volume, ou porta como é o caso, sempre a esquerda dos dois pontos se refere a maquina e a parte direita a parte referente ao container, no caso a porta 80 da maquina mapeada para a porta 80 do container. Além disso qualquer alteração na pasta web, caso o container rode no modo deamon, será imediatamente percebido.

## Lendo e processando arquivos externos

    version: '3'
    volumes:
        dados:
    services:
    db:
        image: postgres:9.6
        environment:
            POSTGRES_USER: postgres
            POSTGRES_PASSWORD: 123456 
            PGDATA: /tmp                 
        volumes:      
          - dados:/var/lib/postgresql/data
          - ./sql:/scripts
          - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql
    frontend:
        image: nginx:1.13
        volumes:
          - ./web:/usr/share/nginx/html
        ports:
          - 80:80
    app:
        image: python:3.6
        volumes:
          - ./app:/app
        working_dir: /app
        command: bash ./app.sh
        ports:
          - 8080:8080

A grande diferença está no `working_dir` e `command`, ambos trabalham em conjunto.

### working_dir
Aqui o diretório de trabalho, ou seja o diretório ao qual irá alimentar o container, nesse exemplo seria o código que a imagem do Python deve executar.

### command
Aqui você especifica o comando a ser executado, lembrando que ele executa um comando de uma working_dir definida, logo esse trabalha em conjunto com a working dir, no caso foi carregado a pasta app como working_dir e dentro desta pasta executado o arquivo de script.

## Proxy Reverso
    version: '3'
    volumes:
        dados:
    services:
        db:
            image: postgres:9.6
            environment:
                POSTGRES_USER: postgres
                POSTGRES_PASSWORD: 123456 
                PGDATA: /tmp                 
            volumes:      
              - dados:/var/lib/postgresql/data
              - ./sql:/scripts
              - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql
        frontend:
            image: nginx:1.13
            volumes:
              - ./web:/usr/share/nginx/html
              - ./nginx.conf:/etc/nginx/conf.d/default.conf
            ports:
            - 80:80
        app:
            image: python:3.6
            volumes:
              - ./app:/app
            working_dir: /app
            command: bash ./app.sh   

### Explicando
Repare no seguinte: foi removido essa linha ao final do arquivo:

    ports:
          - 8080:8080

e adicionado essa: `- ./nginx.conf:/etc/nginx/conf.d/default.conf`, nesse caso ao invés de expor a porta 8080 para público isso foi delegado para o nginx por meio do proxy reverso, através desse arquivo: 
#### nginx
    server {
        listen 80;
        server_name localhost;

        location / {
            root /usr/share/nginx/html;
            index index.html index.htm;
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
            root /usr/share/nginx/html;
        }

        location /api {
            proxy_pass http://app:8080/;
            proxy_http_version 1.1;
        }
    }

#### Server
    server {
            listen 80;
            server_name localhost;

Aqui é configurado a porta e o Ip ao qual o nginx vai ouvir.

#### Location /
    location / {
                root /usr/share/nginx/html;
                index index.html index.htm;
            }

Configuração de rotas, tipo aonde esta o arquivo de index, ou seja quando for digitado a **"/"** qual arquivo e em qual path deve ser carregado?

#### Error page
     error_page 500 502 503 504 /50x.html;
        location = /50x.html {
            root /usr/share/nginx/html;
        }

Em caso de erro da familia 500, qual arquivo e path o nginx deve carregar?

#### /api
    location /api {
            proxy_pass http://app:8080/;
            proxy_http_version 1.1;
        }

Aqui estamos tratando uma rota específica, a rota API no caso, ou seja o font vai mandar uma requisição para essa url e aqui será definido isso, `proxy_http_version 1.1;` aqui indicamos a versão do HTTP que estamos usando.

##### proxy_pass http://app:8080/;
A primeira coisa que precisamos saber sobre containers, é que eles possuem um IP e podemos referenciar eles pelo nome, no caso esse app desse arquivo de configuração do NGINX, será interpretado pelo docker nesse container abaixo, que pode ser visto na integra aqui: [docker-compose.yml](#proxy-reverso):

    app:
        image: python:3.6
        volumes:
              - ./app:/app
        working_dir: /app
        command: bash ./app.sh   

Toda vez que for referenciado esse app, será relacionado a esse container acima.

### Mapeando arquivos
`- ./nginx.conf:/etc/nginx/conf.d/default.conf`, lembre-se sempre de uma coisa a esquerda o arquivo do computador que hospedeiro e a direita o container, nesse caso estamos mapeando o arquivo `nginx.conf` para esse arquivo no container do nginx `/etc/nginx/conf.d/default.conf`.