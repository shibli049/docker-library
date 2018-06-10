FROM node:carbon

VOLUME  ["/app"]
WORKDIR /app

RUN apt-get update

RUN npm install -g @angular/cli@latest

COPY entry.sh /usr/bin/

EXPOSE 4200

ENTRYPOINT ["/bin/bash", "-c", "/usr/bin/entry.sh"]

# docker build -t angular-app .
# docker run — rm -v $PWD:/app -p 4300:4200 angular-app