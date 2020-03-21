#App Flask
FROM ubuntu
LABEL Author="Santiago Caro"
RUN apt update && apt-get install -y python-pip python-dev build-essential
COPY app.py /myapp/
COPY requirements.txt /req/
RUN pip install --no-cache-dir -r /req/requirements.txt
CMD python /myapp/app.py
EXPOSE 5000
