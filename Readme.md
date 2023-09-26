#Comandos docker

## Cria e executa um container a partir de uma imagem
```console
docker run
```
### PARAMETRÔS:
-it (iterativo - usa o terminal como novo)
-d (detached - backgrount)
-p 80:80 (porta em que estará na maquina, com porta do container)
--name(nomear container)
nome da imagem

v- nome_volume:diretorio (criar volume) * diretorio precisar ser compativel com WORKDIR
OBS.*: 
usar a maquina como volume com bind mount
-v diretorio que eu quero salvar:diretorio que é salvo no docker
e ele ainda servirá para atualizar todo o projeto caso passe
diretorio_projeto:WORKDIR_do_Dockerfile


--rm (apagar o container após execução)
[nome_imagem]



## Criar imagens a partir do Dockerfile
```console
docker build
```

###PARAMETRÔS
-t [name](name:tagVersion)
Endereço do Dockerfile

## Verificar containers
```console
docker ps -a
```

## Verificar imagens
```console
docker images
```


## Verificar volumes
```console
docker volumes ls
```

## Verificar networks
```console
docker network ls
```

## Criar network
```console
docker network create [nome]
```
(driver default: bridge)

### PARAMETRÔS
-d [driver]

OBS.* no network host geralmente é preciso criar no código
Ex.: após criar a image e network 
docker run -d -p [3306]:3306 --name container_mysql_flask  --network flasknetwork -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysqlbridge

na conexão entre container nem é preciso externalizar portas

## Conectar container a uma network
```console
docker network connect [nome_network] [container(name OR id)]
```

## Desconectar container a uma network
```console
docker network disconnect [nome_network] [container(name OR id)]
```

### Criação de variaveis de ambiente:
-e nome_variavel=valor
quando for rodar o docker run pelo terminal

## Criar varios container com compose
```console
docker compose up
```

### PARAMETRÔS:
-d (detached - backgrount)

## Verificar containers do compose rodando
```console
docker compose ps
```

## Iniciar docker swarm
```console
docker swarm init
```

## join docker swarm
```console
docker swarm join --token SWMTKN-1-27wjwr1gfjqeg6bjldzb39nm3cdb9u60i6giqsy0cu6790tl8b-8b1nblqv85s6y11xgln3myhv8 [IP]:2377
```

## Get token
```console
docker swarm join-token manager
```
