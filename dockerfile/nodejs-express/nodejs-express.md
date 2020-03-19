# Aplicación web con nodejs y Express

![nodejs Logo](https://nodejs.org/static/images/logo.svg)

[Express](https://expressjs.com/) es un framework de aplicaciones web mínimo y flexible de Node.js, que proporciona un sólido conjunto de características para aplicaciones web y móviles.

## Objetivo

El objetivo de este problema es crear una imagen Docker de una aplicación web desarrollada con *Express*. Como la implementación queda fuera del ámbito de la asignatura, utilizaremos un ejemplo muy sencillo de aplicación web.

Por lo tanto, el objetivo del problema pasa por diseñar el fichero [Dockerfile](https://docs.docker.com/engine/reference/builder/) necesario para que la aplicación de ejemplo se pueda desplegar en un contenedor Docker.

## Tecnología necesaria para ejecutar Express

Si consultamos la [documentación](https://expressjs.com/en/starter/installing.html) sobre la instalación de *Express*, vemos que el primer requisito es tener [nodejs](https://nodejs.org/es/) instalado. Si bien podríamos partir de una imagen base como *Linux Alpine* e instalar *nodejs* mediante `apt-get`, vamos a no reinventar la rueda y utilizar como base la [imagen oficial de Docker](https://hub.docker.com/_/node) que *nodejs* pone a nuestra disposición.

Según leemos en la documentación, esta imagen de Docker contiene pre-instalado todo lo necesario para lanzar aplicaciones.

El primer paso es crear el fichero `package.json` que define la aplicación web y sus dependencias. El objetivo de este ejercicio no es aprender a implementar, por lo que este fichero ya se proporciona:

```json
{
    "name": "docker_web_app",
    "version": "1.0.0",
    "description": "Node.js on Docker",
    "author": "First Last <first.last@example.com>",
    "main": "server.js",
    "scripts": {
      "start": "node server.js"
    },
    "dependencies": {
      "express": "^4.16.1"
    }
}
```

Para que se instalen las dependencias, hay que utilizar el siguiente comando:

```bash
npm install
```

Para definir lo que hace la aplicación web, se crea un fichero `server.js` con la lógica de la aplicación. Es en este fichero donde se importa y utiliza *Express* para definir el comportamiento de la aplicación:

```javascript
'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

Se observa en el código que el **puerto** que se va a usar es el `8080`.

Por último, la instrucción que hay que ejecutar para lanzar nuestra aplicación sería la siguiente:

```bash
node server.js
```

**OJO:** En el caso de aplicaciones *nodejs* es recomendable definir un fichero [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file) para incluir algunas rutas y ficheros a excluir cuando se ejecuta la instrucción `COPY` o `ADD`. Este fichero es similar a un `.gitignore`. En nuestro caso, es recomendable añadir los siguientes patrones al fichero para evitar que se copien cachés locales de paquetes:

```text
node_modules
npm-debug.log
```

## Tareas

1. Crea un fichero `Dockerfile` para distribuir nuestra sencilla aplicación web como imagen de contenedor Docker.

2. Construye la imagen con `docker build -t mi-app-express .` y comprueba que el proceso termina sin errores. Presta atención a cómo se van añadiendo las capas *overlayfs* a la imagen.

3. Lanza un contenedor con la imagen que acabas de construir y comprueba que funciona abriendo la siguiente URL en tu navegador: [localhost:8080](http://localhost:8080). Recuerda mapear el puerto 8080 cuando ejecutes `docker run mi-app-express`.

Si necesitas una ayuda, puedes consultar el esquema con comentarios del fichero Dockerfile:

## Tareas extra

1. Hemos visto que se crea una capa en la imagen cada vez que se ejecuta una instrucción `COPY`, `ADD` o `RUN` en un `Dockerfile`. ¿Se te ocurre alguna forma de reducir el número de capas que se añaden a nuestra imagen?

2. Nuestra imagen de Docker tiene una peculiaridad: cada vez que modifiquemos la aplicación web tendremos que reconstruir la imagen para que los archivos se copien. Una posible alternativa sería utilizar volúmenes, de forma que el directorio de trabajo de nuestra imagen se pudiese montar como un volumen al directorio de trabajo de nuestra máquina host. ¿Se te ocurre cómo hacerlo?
