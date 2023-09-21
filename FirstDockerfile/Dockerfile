FROM node
WORKDIR /app

#COPY package.json /app COPY package-lock.json /app 
#COPY package*.json /app

#Resumo de sintaxe, copia todos os aqruivos package para o workdir
# para que facilite a copia do node modules
COPY package*.json . 

RUN npm install

# Faz copia de tudo para o container
COPY . .

#Porta que o docker vai associar na minha maquina
#Porta da aplicação deve ser igual do docker
EXPOSE 3000

#Comandos para executar a aplicação
CMD [ "node", "app.js" ]

## docker build [diretorio do Dockerfile]