# vesrion  0.0.2
FROM alpine:latest
LABEL maintainer="Tahmim Ahmed Shibli <shibli05 at gmail>"

RUN apk --update add openjdk8

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

# install elasticsearch
RUN addgroup -g 1000 -S elasticsearch && adduser -u 1000 -D -S -G elasticsearch elasticsearch

RUN wget -O elasticsearch.zip https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/2.4.6/elasticsearch-2.4.6.zip \
    && unzip elasticsearch.zip \
    && rm -f elasticsearch.zip \
    && mv elasticsearch* elasticsearch \
    && mv elasticsearch /usr/share/elasticsearch


WORKDIR /usr/share/elasticsearch


RUN set -ex && for path in data logs plugins config config/scripts; do \
        mkdir -p "$path"; \
        chown -R elasticsearch:elasticsearch "$path"; \
    done

VOLUME /usr/share/elasticsearch/data

# change user
USER elasticsearch

COPY logging.yml /usr/share/elasticsearch/config/
COPY elasticsearch.yml /usr/share/elasticsearch/config/

ENV PATH=/usr/share/elasticsearch/bin:$PATH

CMD ["elasticsearch"]
EXPOSE 9200 9300

# run the docker: 
# cd /mnt/devlnx/es/es-docker; docker run --restart unless-stopped -d --name es-alpine-server -p 9200:9200 -p 9300:9300 --mount type=bind,src="$(pwd)/data",target=/usr/share/elasticsearch/data alpine-es
