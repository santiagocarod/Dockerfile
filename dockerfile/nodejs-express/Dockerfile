FROM node
COPY package.json /myapp/
RUN cd /myapp/ && npm install
COPY server.js /myapp/
EXPOSE 8080
CMD cd /myapp/ && node server.js