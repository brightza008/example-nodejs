FROM node:alpine3.10

WORKDIR /app
COPY ./app/hello-1.js .

RUN apk add redis

RUN npm install express
RUN npm install redis

RUN export port=redis_port
RUN export host=redis_host

CMD redis-server & node /app/hello-1.js


