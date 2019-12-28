FROM node:6-alpine
MAINTAINER mohan garapati

ENV NODE_VERSION 8.17.0

#RUN addgroup -g 1000 node \
#    && adduser -u 1000 -G node -s /bin/sh -D node 

RUN apk add --update tini

RUN apk add --update nodejs

RUN mkdir -p /usr/src/app && chown -R node:node /usr/src/app

WORKDIR /usr/src/app  


COPY package.json ./

USER node

RUN npm install

USER root 

RUN npm cache clean --force

COPY --chown=node:node . /usr/src/app

EXPOSE 3000

CMD /sbin/tini -- node ./bin/www

#CMD [ "node", "app.js" ]

