FROM golang

# Pull the ElasticSearch Beats Source Files and
# ignore error "package github.com/elastic/beats: build constraints exclude all Go files in /go/src/github.com/elastic/beats"
RUN go get github.com/elastic/beats || true
# Build and install filbeat
RUN cd src/github.com/elastic/beats/ && \
    git checkout 7.8 && \
    cd x-pack/filebeat/ && \
    go build && \
    go install

# Add the custom config and other files from https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.8.1-linux-x86_64.tar.gz
RUN wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.8.1-linux-x86_64.tar.gz && \
    tar zxvf filebeat-7.8.1-linux-x86_64.tar.gz && \
    mv filebeat-7.8.1-linux-x86_64/* ./ && \
    rm -rf filebeat-7.8.1-linux-x86_64 && \
    rm -rf filebeat-7.8.1-linux-x86_64.tar.gz

ADD files .

# Expose ports for netflow and syslog
EXPOSE 2055 2055/udp 9000 9000/udp

# Start Filebeat
ENTRYPOINT ["filebeat", "-e"]
