# How to use

Create Dockerfile for hello-1.js
```
FROM node:alpine3.10

WORKDIR /app
COPY ./app/hello-1.js .

RUN apk add redis

RUN npm install express
RUN npm install redis

RUN export port=redis_port
RUN export host=redis_host

CMD redis-server & node /app/hello-1.js
```

and Dockerfile for hello-2.js
```
FROM node:alpine3.10

WORKDIR /app
COPY ./app/hello-2.js .

RUN npm install express
RUN npm install redis

CMD node /app/hello-2.js
```

Create docker-compose.ym;
```
version: '3'
services:
  hello1:
    build:
      context: .
      dockerfile: ./hello1_dockerfile/Dockerfile
    ports:
     - "8001:8000"
    restart: always

  hello2:
    build:
      context: .
      dockerfile: ./hello2_dockerfile/Dockerfile
    ports:
     - "8002:8000"
restart: always
```

Command to run docker-compose 
```bash
docker-compose up -d
```

Create nginx Configuration
```
default.conf
```

# Using with Jenkins 


create job jenkins pipeline with https://github.com/brightza008/example-nodejs.git




# example-nodejs
Just simple nodejs application

## Installation ##
npm install express

npm install redis

## hello-1 ##

In case of hello-1 , it need to have redis server to keep session & timestamp

export port=redis_port

export host=redis_host

node app/hello-1.js 

## hello-2 ##

node app/hello-2.js
