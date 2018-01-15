# vesrion  0.0.2
FROM ubuntu:16.04

LABEL maintainer="Tahmim Ahmed Shibli <shibli05 at gmail>"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
&& apt-get install -y --no-install-recommends software-properties-common \
&& add-apt-repository -y ppa:webupd8team/java \
&& apt-get update\
&& (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) \
&& apt-get install --no-install-recommends -y oracle-java8-installer \
&& rm -rf /var/cache/oracle-jdk8-installer \
&& echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-8-oracle/jre/lib/security/java.security \
&& apt-get clean && rm -rf /var/lib/apt/lists/* \
&& apt-get -y autoclean \
&& apt-get -y autoremove

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# install elasticsearch
RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000
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
# cd /mnt/devlnx/es/es-docker && docker run --restart unless-stopped -d --name es-server -p 9200:9200 -p 9300:9300 --mount type=bind,src="$(pwd)/data",target=/usr/share/elasticsearch/data es-image



