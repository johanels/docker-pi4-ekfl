FROM arm64v8/amazoncorretto:11

ARG bootstrap.memory_lock
ARG network.host
ARG http.port
ARG xpack.ml.enabled
ARG discovery.seed_hosts
ARG xpack.ml.enabled

RUN yum install -y gzip shadow-utils tar && \
    groupadd -g 1000 elasticsearch && \
    adduser -u 1000 -g 1000 elasticsearch

WORKDIR /home/elasticsearch

USER elasticsearch:root

RUN curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-no-jdk-linux-x86_64.tar.gz && \
    tar zxvf elasticsearch-7.8.1-no-jdk-linux-x86_64.tar.gz --strip-components=1 && \
    rm -rf elasticsearch-7.8.1-no-jdk-linux-x86_64.tar.gz

ADD elasticsearch.yml config/elasticsearch.yml

RUN bin/elasticsearch-keystore create && \
    echo "12345678" | bin/elasticsearch-keystore add --stdin "bootstrap.password"

EXPOSE 9200 9300

ENTRYPOINT ["./bin/elasticsearch"]
