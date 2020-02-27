# Requirement
+ Allow firewall port 80
```bash
$ firewall-cmd --zone=public --add-port=80/tcp --permanent
```
+ Allow jenkins user for run docker command 
```bash
$ usermod -aG root jenkins
```

# Using with Jenkins 


Create jenkins pipeline job with source code: https://github.com/brightza008/example-nodejs.git



# Source Code on github
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

Create docker-compose.yml
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

Jenkinsfile
```
pipeline {
    agent any
    environment { 
        PATH = "$PATH:/usr/local/bin" //define docker-compose for jenkins user 
    }
    stages {
        stage('clear existing dontainer') {
        	steps {
                sh'''
                  docker-compose stop
                '''
            }
        } //End stage
        stage('deploy docker container') {
        	steps {
                sh'''
                  docker-compose up -d
                '''
            }
        } //End stage
    }//End stages
}//End pipeline
```

Edit nginx Configuration in `/etc/nginx/conf.d/default.conf` and reload config
```
server {
    listen       80;
    server_name  localhost;
    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
    
   location /hello1 {
            proxy_pass         http://0.0.0.0:8001;
        }

   location /hello2 {
            proxy_pass         http://0.0.0.0:8002;
        }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

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
