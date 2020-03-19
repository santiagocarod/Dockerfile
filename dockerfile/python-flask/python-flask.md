# Aplicación web con Python y Flask

![Flask Logo](https://upload.wikimedia.org/wikipedia/commons/3/3c/Flask_logo.svg)

[Flask](https://palletsprojects.com/p/flask/) es un framework ligero de aplicaciones web que cumple la especificación *WSGI*. El framework está basado en Python.

## Objetivo

El objetivo de este problema es crear una imagen Docker de una aplicación web desarrollada con *Flask*. Como la implementación queda fuera del ámbito de la asignatura, utilizaremos un ejemplo muy sencillo de aplicación web.

Por lo tanto, el objetivo del problema pasa por diseñar el fichero [Dockerfile](https://docs.docker.com/engine/reference/builder/) necesario para que la aplicación de ejemplo se pueda desplegar en un contenedor Docker.

## Tecnología necesaria para ejecutar Flask

Si consultamos la [documentación](https://flask.palletsprojects.com/en/1.1.x/installation/) sobre la instalación de Flask, nos encontramos con:

> We recommend using the latest version of Python 3. Flask supports Python 3.5 and newer, Python 2.7, and PyPy.

Por lo tanto, necesitaremos instalar Python y algunas librerías adicionales, como por ejemplo la herramienta `pip` para instalar paquetes Python. En una máquina con Ubuntu, bastaría con lanzar la siguiente instrucción:

```bash
apt-get install -y python-pip python-dev build-essential
```

En Python es común utilizar el fichero `requirements.txt` para especificar en él las dependencias que tiene nuestro proyecto. Como nuestra aplicación web es extremadamente simple, la única dependencia que tiene el proyecto es, precisamente, la librería [Flask](https://palletsprojects.com/p/flask/):

```text
Flask==1.0
```

Para que `pip` instale automáticamente las dependencias de un proyecto, hay que ejecutar el siguiente comando:

```bash
pip install --no-cache-dir -r <ruta/a/requirements.txt>
```

En el fichero `app.py` se define la aplicación web. Como ya hemos dicho, es extremadamente simple. Su única funcionalidad es mostrar un mensaje:

```python
import socket
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return "¡Hola! Flask se está ejecutando en {}".format(socket.gethostname())


if __name__ == '__main__':
    # Es necesario especificar el parámetro host para que el servidor pueda recibir peticiones desde fuera del contenedor
    app.run(host='0.0.0.0')
```

Un detalle importante es que el **puerto por defecto** para los servidores Flask es el `5000`.

Por último, la instrucción que hay que ejecutar para lanzar nuestra aplicación sería la siguiente:

```bash
python </ruta/a/app.py>
```

## Tareas

1. Crea un fichero `Dockerfile` para distribuir nuestra sencilla aplicación web como imagen de contenedor Docker.

2. Construye la imagen con `docker build -t mi-app-flask .` y comprueba que el proceso termina sin errores. Presta atención a cómo se van añadiendo las capas *overlayfs* a la imagen.

3. Lanza un contenedor con la imagen que acabas de construir y comprueba que funciona abriendo la siguiente URL en tu navegador: [localhost:5000](http://localhost:5000). Recuerda mapear el puerto 5000 cuando ejecutes `docker run mi-app-flask`.

Si necesitas una ayuda, puedes consultar el esquema con comentarios del fichero Dockerfile:

<details>
  <summary>Plantilla Dockerfile</summary>

  ```text
    # Imagen base
    FROM

    # Instalar python y pip
    RUN

    # Copiar el fichero de dependencias e instalarlas con pip
    COPY
    RUN

    # Copiar el fichero con la aplicación web
    COPY

    # Declarar el puerto que utilizarán los contenedores
    EXPOSE

    # Lanzar la aplicación web con Flask
    CMD [, ]
  ```
  
</details>

## Tareas extra

1. Hemos visto que se crea una capa en la imagen cada vez que se ejecuta una instrucción `COPY`, `ADD` o `RUN` en un `Dockerfile`. ¿Se te ocurre alguna forma de reducir el número de capas que se añaden a nuestra imagen?

2. Nuestra imagen de Docker tiene una peculiaridad: cada vez que modifiquemos la aplicación web tendremos que reconstruir la imagen para que los archivos se copien. Una posible alternativa sería utilizar volúmenes, de forma que el directorio de trabajo de nuestra imagen se pudiese montar como un volumen al directorio de trabajo de nuestra máquina host. ¿Se te ocurre cómo hacerlo?
