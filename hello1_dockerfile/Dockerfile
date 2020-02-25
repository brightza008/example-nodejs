FROM node:alpine3.10

WORKDIR /app
COPY ./app/ .

RUN npm install express
RUN npm install redis

RUN export port=redis_port
RUN export host=redis_host

CMD node /app/hello-1.js


