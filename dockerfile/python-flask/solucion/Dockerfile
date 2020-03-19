    # Imagen base
    FROM ubuntu:latest

    # Instalar python y pip
    RUN apt-get update; apt-get install -y python-pip python-dev build-essential

    # Copiar el fichero de dependencias e instalarlas con pip
    COPY requirements.txt /usr/src/app/
    RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

    # Copiar el fichero con la aplicación web
    COPY app.py /usr/src/app/

    # Declarar el puerto que utilizarán los contenedores
    EXPOSE 5000

    # Lanzar la aplicación web con Flask
    CMD ["python", "/usr/src/app/app.py"]
