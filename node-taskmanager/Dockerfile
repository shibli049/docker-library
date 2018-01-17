# vesrion  0.0.2
FROM node:wheezy

LABEL maintainer="Tahmim Ahmed Shibli <shibli05 at gmail>"


RUN mkdir -p /usr/src/app/

WORKDIR /usr/src/app/


RUN git clone https://github.com/shibli049/TaskManager.git


WORKDIR /usr/src/app/TaskManager

RUN npm install 

EXPOSE 3000

CMD [ "git", "pull", "origin", "master" ]

CMD [ "npm", "start" ]