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
## Atulaizar a rede de um serviço
```console
docker service update --network-add [REDE] [IDSERVICE]
```
# No Kube existe o deployment que seria o meu serviço e os pods que são como computadores que hospedam containers, o meu serviço pode ser externalizado usando o minikube e caso algum pod caia, outro pod de replica substitui seu lugar para a aplicação continuar no ar
## AO INSTALAR O 'MINIKUBE' ELE BUSCA TAMBÉM O KUBERNETS E JÁ ASSOCIA
## Iniciando minikube com docker:
```console
minikube start --driver=docker
```

## Criar deployment no Kube
```console
kubectl create deployment [NAME-DEPLOY] --image=[NOME_IMAGE] 
```

## Checando deployments 
```console
kubectl get deployment OU
kubectl describe deployment
```

## Checando pods 
```console
kubectl get pods OU
kubectl describe pods
```

## Configurações do Kube 
```console
kubectl config view
```

## Criar service no Kube
```console
kubectl expose deployment [NAME-DEPLOY] --type=[TIPO] --port=[PORTA]
```

## Expor service no minikube
```console
minikube service [NAME-DEPLOY]
```

## Checando services 
```console
kubectl get services OU
kubectl describe services/[NAME-DEPLOY]
```

## Replicar aplicação 
```console
kubectl scale deployment/[NAME-DEPLOY] --replicas=[NÚMERO]
```

## Checando replicas 
```console
kubectl get rs
```

## Atualizar imagem pelo pod manager 
```console
kubectl set image deployment/[NAME-DEPLOY] [NAME-CONTAINER]=[NEW-NAME-IMAGE]
```

## Checar alteração no deploy
```console
kubectl rollout status deployment/[NAME-DEPLOY]
```

## Desfazer alteração 
```console
kubectl rollout undo deployment/[NAME-DEPLOY]
```

## Deletar service do Kube 
```console
kubectl delete service [NAME-DEPLOY]
```

## Deletar deployment do Kube 
```console
kubectl delete deployment [NAME-DEPLOY]
```

## Criar Deployment por arquivo yaml
```console
kubectl apply -f [NAME-ARQUIVO]
```

# Usando kubernets com docker-desktop

## Instale através da interface

## E logo já poderá usar os proprios comandos do kubectl

## Para iniciar o dashboard você precisa executar o seu deploy
```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml
```

## Para acessar o dashboard você precisa se autenticar e para isso deve criar dois services
Um <a href="https://github.com/jose-luan19/Course_Docker/blob/main/dashboard-adminuser.yaml">ServiceAccount </a> com o tipo de usuario e outro <a href="https://github.com/jose-luan19/Course_Docker/blob/main/cluster-admin.yaml">ClusterRoleBinding </a>  fazendo uma ponte entre o serviço de usuario criado antes e o cluster

## Criar token para logar
```console
kubectl -n kubernetes-dashboard create token admin-user
```

## Executa o servidor e  acessa a url para visulizar o dahsboard
```console
kubectl proxy
```

## Endereço do dashboard
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

