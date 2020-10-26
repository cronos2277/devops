# Docker
## Resumo dos comandos

### docker image COMMAND
  `build`    **=>**   Constrói uma imagem apartir de um Dockerfile

  `history`  **=>**   Mostra o histórico de uma imagem

  `import`   **=>**   Importa o conteúdo de um tarball para criar uma imagem do sistema de arquivos

  `inspect`  **=>**   Exibaeinformações detalhadas sobre uma ou mais imagens

  `load`     **=>**   Carrega uma imagem de um arquivo tar ou STDIN

  `ls`       **=>**   Lista imagens

  `prune`    **=>**   Remove imagens não usadas

  `pull`     **=>**   Receba a imagem ou repositório de um registro

  `push`     **=>**   Envie uma imagem ou repositório para um registro

  `rm`       **=>**   Remove um ou mais imagens

  `save`     **=>**   Salve uma ou mais imagens em um arquivo tar (transmitido para STDOUT por padrão)

  `tag`      **=>**   Crie uma tag TARGET_IMAGE que se refira a SOURCE_IMAGE

### docker container COMMAND
  `attach`    **=>**  Anexe entrada, saída e fluxos de erro padrão locais a um contêiner em execução

  `commit`    **=>**  Crie uma nova imagem a partir das alterações de um contêiner

  `cp     `   **=>**  Copie arquivos / pastas entre um contêiner e o sistema de arquivos local

  `create `   **=>**  Crie um novo contêiner

  `diff   `   **=>**  Inspecione alterações em arquivos ou diretórios no sistema de arquivos de um contêiner

  `exec   `   **=>**  Execute um comando em um contêiner em execução

  `export `   **=>**  Exporte o sistema de arquivos de um contêiner como um arquivo tar

  `inspect`   **=>**  Exiba informações detalhadas sobre um ou mais contêineres

  `kill   `   **=>**  Mate um ou mais contêineres em execução

  `logs   `   **=>**  Busque os registros de um contêiner

  `ls     `   **=>**  liste containers

  `pause  `   **=>**  Pause todos os processos em um ou mais contêineres

  `port   `   **=>**  Listar mapeamentos de portas ou um mapeamento específico para o contêiner

  `prune  `   **=>**  Remova todos os contêineres parados

  `rename `   **=>**  Renomear um contêiner

  `restart`   **=>**  Reinicie um ou mais contêineres

  `rm     `   **=>**  Remova um ou mais recipientes

  `run    `   **=>**  Execute um comando em um novo contêiner

  `start  `   **=>**  Inicie um ou mais contêineres parados

  `stats  `   **=>**  Exiba uma transmissão ao vivo de estatísticas de uso de recursos de contêineres

  `stop   `   **=>**  Pare um ou mais contêineres em execução

  `top    `   **=>**  Exiba os processos em execução de um contêiner

  `unpause`   **=>**  Retome todos os processos em um ou mais contêineres

  `update `   **=>**  Atualize configuração de um ou mais contêineres

  `wait   `   **=>** Bloqueie até que um ou mais contêineres parem e imprima seus códigos de saída

### docker volume COMMAND
  
  `create `   **=>**  Crie um volume
  
  `inspect`   **=>**  Exiba informações detalhadas em um ou mais volumes
  
  `ls     `   **=>**  liste de volumes
  
  `prune  `   **=>**  Remova todos os volumes locais não utilizados
  
  `rm     `   **=>**  Remova um ou mais volumes


### docker COMMAND
#### Sintaxe Antiga
  `attach `   **=>**  Anexe entrada, saída e fluxos de erro padrão locais a um contêiner em execução

  `build  `   **=>**  Construa uma imagem de um Dockerfile

  `commit `   **=>**  Crie uma nova imagem a partir das alterações de um contêiner

  `cp     `   **=>**  Copie arquivos / pastas entre um contêiner e o sistema de arquivos local

  `create `   **=>**  Crie um novo contêiner

  `diff   `   **=>**  Inspecione alterações em arquivos ou diretórios no sistema de arquivos de um contêiner

  `events `   **=>**  Obtenha eventos em tempo real do servidor

  `exec   `   **=>**  Execute um comando em um contêiner em execução

  `export `   **=>**  Exporte o sistema de arquivos de um contêiner como um arquivo tar

  `history`   **=>**  Mostra a história de uma imagem

  `images `   **=>**  Listar imagens

  `import `   **=>**  Importe o conteúdo de um tarball para criar uma imagem do sistema de arquivos

  `info   `   **=>**  Exibir informações de todo o sistema

  `inspect`   **=>**  Retorne informações de baixo nível sobre objetos Docker

  `kill   `   **=>**  Mate um ou mais contêineres em execução

  `load   `   **=>**  Carregar uma imagem de um arquivo tar ou STDIN

  `login  `   **=>**  Faça login em um registro do Docker

  `logout `   **=>**  Saia de um registro do Docker

  `logs   `   **=>**  Busque os registros de um contêiner

  `pause  `   **=>**  Pause todos os processos em um ou mais contêineres

  `port   `   **=>**  Listar mapeamentos de portas ou um mapeamento específico para o contêiner

  `ps     `   **=>**  Contêineres de lista

  `pull   `   **=>**  Puxe uma imagem ou repositório de um registro

  `push   `   **=>**  Envie uma imagem ou repositório para um registro

  `rename `   **=>**  Renomear um contêiner

  `restart`   **=>**  Reinicie um ou mais contêineres

  `rm     `   **=>**  Remova um ou mais containers

  `rmi    `   **=>**  Remova uma ou mais imagens

  `run    `   **=>**  Execute um comando em um novo contêiner

  `save   `   **=>**  Salve uma ou mais imagens em um arquivo tar (transmitido para STDOUT por padrão)

  `search `   **=>**  Pesquise imagens no Docker Hub

  `start  `   **=>**  Inicie um ou mais contêineres parados

  `stats  `   **=>**  Exibir uma transmissão ao vivo de estatísticas de uso de recursos de contêineres

  `stop   `   **=>**  Pare um ou mais contêineres em execução

  `tag    `   **=>**  Crie uma tag TARGET_IMAGE que se refira a SOURCE_IMAGE

  `top    `   **=>**  Exibir os processos em execução de um contêiner

  `unpause`   **=>**  Retome todos os processos em um ou mais contêineres

  `update `   **=>**  Atualizar configuração de um ou mais contêineres

  `version`   **=>**  Mostra as informações da versão do Docker

  `wait   `   **=>**  Bloqueie até que um ou mais contêineres parem e imprima seus códigos de saída


## Explicando os principais comandos
Todos os comandos do docker tem o `docker` no começo e o que vem depois é justamente esse comando deve estar na frente de qualquer comando.
### docker inspect [image]
Retorna um JSON contendo as configurações da imagem `[image]`

### docker image
Todo comando que tem `image` ele é usado para a interação com imagens, ou seja as imagens são as receitas, ou as classes se fosse relacionarmos com orientação a objetos e com base nessa receita criamos o nosso container.

#### docker image build [path]
Esse comando permite que você crie uma imagem customizável com base no arquivo docker, aonde está o [**path**] você deve informar o diretoório do arquivo dock, que contém a receita para a criação de uma imagem customizável, ou você pode usar o ponto para indicar o diretório corrente, segue um exemplo desse arquivo: [Dockerfile](Dockerfile)

##### docker image build -t [nome_da_imagem]
Informando o parametro `-t` você pode criar uma tag, ou seja um nome para que você possa usar para chamar essa imagem customizada, como por exemplo: `docker container run [nome_da_imagem]`

### docker container
Todo o container se comparado com a programação orientado a objetos seria um objeto instanciado e os comandos envolvendo o `container` refere-se a forma com que esse "objeto" seria instanciado

#### docker container start [nome]
Com esse comando você inicia um container [**nome**], pode ser a tag criada com `-t` ou o hash. Pode ser uma ou mais imagem separados por um espaço.

#### docker container stop [nome]
Esse comando para a execução de um container, pode ser a tag criada com `-t` ou o hash. Pode ser uma ou mais imagem separados por um espaço.

#### docker container restart [nome]
Reinicia determinado container com a tag `[nome]`.

#### docker container run [nome]
Esse comando procura a imagem localmente e se não tiver, faz download, após isso executa a imagem subindo assim um container.

##### docker container [run] -p[tcp porta hospedeiro]:[tcp porta container] [imagem]
Essa tag `-p` ele permite mapear uma do container com uma porta TCP do hospedeiro, por exemplo `-p 8080:80` o primeiro argumento antes dos `:` você deve informar a porta do hospedeiro a ser mapeada e o segundo parametro a porta interna do container, ou seja quando o hospedeiro recebe processo na **8080**, ela redireciona a porta **80** do container, exemplo de uso `docker container run -p 8080:80 nginx`, nesse exemplo estamos mapeando uma imagem do nginx na com a porta **80** do hospedeiro.

##### docker container run -v [path-host] [imagem]
Com essa flag você consegue mapear um volume interno, no caso tudo o que você coloca no diretório ao qual está sendo executado, será copiado para esse diretório informado aqui [**path-host**]

##### docker container run -d [imagem]
Essa flag aciona o modo demon e faz com que o container fique escutando em segundo plano.

##### docker container run --name[nome] [imagem]
Com a flag `--name` você define uma tag(nome) em tempo de execução.

##### docker container exec [tag] [comando-linux]
Um exemplo desse comando: `docker container exec upbeat_mayer uname -or` , no caso esse comando exec, ele executa um comando dentro do sistema operacional linux embarcado do container, precisa ser dado esse comando em um container que esteja rodando, se não não funciona. `[tag]` aui você informa o nome do container que você quer executar o comando, `[comando-linux]` o comando em si, no caso qualquer comando que poderia ser usado no terminal linux.

### docker ps
Mostra todas as maquinas ativas por padrão, se usado com a flag `-a` mostra todas as imagens que estão salvas.

### docker rm
Esse comando serve para excluir uma imagem ou container, se for usar o comando sem especificar se é container ou imagem, se faz necessário usar o hash para isso, pode ser uma ou mais imagem separados por um espaço.
