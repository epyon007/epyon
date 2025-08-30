Fazer o download da imagem do ubuntu no docker na versão latest:

```
docker pull ubuntu
```

Listar imagems docker disponíveis localmente:

```
docker image ls
docker images
```

Fazer o download da imagem do Node no docker na versão latest:
```
docker pull node
```

Fazer o download da imagem do node no docker na versão 14.21.1-alpine:
```
docker pull node:14.21.1-alpine
```

Fazer o download da imagem do mysql no docker na versão latest
```
docker pull mysql
```

Apaga uma imagem baixada localmente no caso do exemplo 
```
docker rmi node:14.21.1-alpine
```
Lista os containers do Docker que estão em execução no momento
```
docker ps
docker container ls
```
Executa o comando docker com a flag help para mostrar outros parâmetros
```
docker run --help
```

Executa um container docker utilizando a imagem ubuntu e usando o parametro de detach para não ficar com o terminal preso
```
docker run -d ubuntu
```

Lista os containers que foram executados mas já foram encerrados.
```
docker ps -a
docker ls -a
```

Executa o container da imagem ubuntu no docker a flag it serve para interagir dentro do container, mas para isso é necessário que um processo esteja atrelado a ele para que ele nao deixe de ser executado - abrindo o container no terminal
```
docker run -it ubuntu
```

Lista todos os containers com o status de encerrados
```
docker container ls -f status=exited
```

Faz a mesma coisa que o comando anterior, no entanto lista apenas os IDs dos containers
```
docker container ls -f status=exited -q
```

O subcomando lista apenas os ids dos containers que estão com o status "exited" e o comando principal utiliza a saída do subcomando para removê-los do sistema
```
docker rm $(docker container ls -f status=exited -q)
```

Executa o container utilizando a flag de detach e atribui ao container um nome, bem como está específicando a sua imagem
```
docker run -d --name zth-epyon ubuntu
```

Executa o container adicionando a flag --rm que já removerá o container do sistema automaticamente caso ele seja encerrado
```
docker run -d --rm --name zth-epyon ubuntu
```


Deleta o container com o ID correspondente
```
docker rm 3b24abb010641cc8b40d4405e8227f9f34221461df7b1968f0fdce64aa011a6b
```

Executa o container utilizando a flag de interativa e atribui ao container um nome, bem como está específicando a imagem node
```
docker run -it --rm --name zth-node node bash
```

Executa o container utilizando a flag de interativa e atribui ao container um nome, bem como está específicando a imagem node e adicionando um processo bash para manter o container rodando

Além disso, é realizado também o mapeamento do volume para o container (utilizando a pasta atual e mapeando o caminho /usr/src/app como volume e work directory)

```
docker run -it --rm --name zth-node -v "$PWD":/usr/src/app -w "/usr/src/app" node bash
```

Executa o container utilizando os mesmos parametros do comando anterior, mas adicionalmente executa um comando no bash do container
```
docker run -it --rm --name zth-node -v "$PWD":/usr/src/app -w "/usr/src/app" node bash -c "node index"
docker run -it --rm --name zth-node -v "$PWD":/usr/src/app -w "/usr/src/app" node bash -c "echo 'Hello World'"
```

Pacote utilizado para criação do arquivo packages.json para mapear dependencias da nossa aplicação nodejs

```
apt install npm
npm init
```

Adiciona a dependência "express" no arquivo package.json
```
npm i -P express
npm install nvm
```

Executa o container setando um nome, volume, workdir, processo que mantem o container up e executa comandos no terminal do container
```
docker run -it --rm --name zth-docker -v "$PWD:/usr/src/app" -w "/usr/src/app" node bash -c "npm install && node index"
```

Interrompe abruptamente um container que esta em execucao
```
docker kill zth-docker
```


Executa o container da aplicacao com os parametros a seguir:

- Modo interativo (-it)
- Remover a imagem apos encerramento do container (--rm)
- Nomeia o container como **zth-docker** (--name)
- Utiliza o volume "$PWD" local para a pasta */usr/src/app* ($PWD:/usr/src/app)
- Mapeia a porta 3000 localmente e no container (-p 3000:3000)
- Define o *workdir /usr/src/app* (-w)
- Utiliza a imagem *node* na versao latest
- Inclui o processo bash para manter o container em execucao
- Executa os comandos **npm install && node index** utilizando a flag (-c)

```
docker run -it --rm --name zth-docker -v "$PWD:/usr/src/app" -w "/usr/src/app" -p "3000:3000" node bash -c "npm install && node index"
```

---
Executa o container do database (MySQL) com os parametros a seguir:

- Modo nao interativo (-d)
- Remover a imagem apos encerramento do container (--rm)
- Nomeia o container como **zth-mysql** (--name)
- Define a variavel de ambiente *MYSQL_ROOT_PASSWORD* com o valor **segredo** o volume "$PWD" local para a pasta */usr/src/app* ($PWD:/usr/src/app)
- Utiliza a imagem *mysql* na versao latest

```
docker run -d --rm --name zth-mysql -e MYSQL_ROOT_PASSWORD=segredo mysql
```




