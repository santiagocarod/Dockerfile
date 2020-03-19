# IDE web Icecoder

![Icecoder logo](https://icecoder.net/images/icecoder.png)

[Icecoder](https://icecoder.net) es un entorno integrado de desarrollo (IDE) accesible a través de la web mediante un navegador. Según su web oficial:

> ICEcoder is a browser based code editor which provides a modern approach to building websites by allowing you to code directly within the web browser. This, in turn, means you only need one program (your browser), plus can test on actual web servers and after development, maintain the website easily, all of which make for speedy and smart development. Because it is web based you also can do this from any internet enabled computer with a modern browser and because it's built with common web languages, customise it to your liking.

## Objetivo

El objetivo de este problema es crear una imagen Docker con el entorno integrado de desarrollo **Icecoder**.

Por lo tanto, el objetivo del problema pasa por diseñar el fichero [Dockerfile](https://docs.docker.com/engine/reference/builder/) necesario para que **Icecoder** se pueda desplegar en un contenedor Docker.

Para construir el Dockerfile debes basarte en los requisitos e instrucciones de instalación que puedes encontrar en su [manual](https://icecoder.net/manual) y se resumen en:

### Requisitos

* Servidor web Apache o similar (Nginx)

* PHP 7.0 como mínimo

### Instalación

1. Descargar el ZIP desde la web oficial (recuerda que `ADD` permitía pasar una URL como parámetro).

2. Descomprimir el fichero en una ruta accesible por el servidor web.

3. Dar permisos de escritura a las carpetas `data`, `lib`, `plugins` y `tmp`.

4. Acceder al servidor desde el navegador para establecer la contraseña.
