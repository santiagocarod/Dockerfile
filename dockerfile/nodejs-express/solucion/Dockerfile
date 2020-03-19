FROM node:13-alpine3.10

# Directorio de trabajo para la aplicacion
WORKDIR /usr/src/app

# Instalacion de dependencias
COPY package*.json ./

RUN npm install

# Copia de los ficheros que definen la aplicacion web
COPY . .

# Puerto a usar
EXPOSE 8080

# Comando para lanzar nodejs
CMD [ "node", "server.js" ]