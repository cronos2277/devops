# Docker

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
