FROM node:alpine3.10

WORKDIR /app
COPY ./app/ .

RUN npm install express
RUN npm install redis

CMD node /app/hello-2.js


