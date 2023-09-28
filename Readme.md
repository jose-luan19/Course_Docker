# Comandos docker

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
docker swarm join --token [TOKEN] [IP]:2377
```

## Get token
```console
docker swarm join-token manager
```

## Criar serviços no swarm
```console
docker service create [IMAGE]
```
### PARAMETRÔS:
 --name [ NAME ]
 --replicas [ QUANTIDADE ]
 -p [portas local : docker]
 --network [NOME DA REDE] usada para isolar certos container dentro da orquestração, e o driver de rede do swarm é o overlay

## Node sair do Swarm
```console
docker swarm leave
```

## Remover Node
```console
docker node rm [ID]
```
caso ainda eseja rodando um serviço basta usar o -f

## Inspecionar services
```console
docker service inspect [ID]
```

## Verificar container que estão num serviço
```console
docker service ps [ID]
```

## Criar swarm junto do arquivo compose
```console
docker stack deploy -c docker-compose.yaml [NAME]
```

## Escalar container já conectados ao meu orquestrador
```console
docker service scale [NAME_SERVICE]=[número]
```

## Para de receber TASK do node manager
```console
docker node update --availability drain [ID]
```

status drain para de receber
pode retornar para active que é o padrão

## Atulaizar a imagem de um serviço
```console
docker service update --image [IMAGE] [IDSERVICE]
```

## Atulaizar a rede de um serviço
```console
docker service update --network-add [REDE] [IDSERVICE]
```