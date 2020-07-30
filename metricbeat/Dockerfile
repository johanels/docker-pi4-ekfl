FROM golang

# Pull the ElasticSearch Beats Source Files and
# ignore error "package github.com/elastic/beats: build constraints exclude all Go files in /go/src/github.com/elastic/beats"
RUN go get github.com/elastic/beats || true

# Build and install metricbeat
RUN cd src/github.com/elastic/beats/ && \
    git checkout 7.8 && \
    cd x-pack/metricbeat/ && \
    go build && \
    go install

# https://www.elastic.co/downloads/beats/metricbeat
RUN curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.8.1-linux-x86_64.tar.gz && \
    tar xzvf metricbeat-7.8.1-linux-x86_64.tar.gz && \
    mv /go/metricbeat-7.8.1-linux-x86_64/kibana /go/

# Add config file
ADD metricbeat.yml metricbeat.yml
RUN chmod go-w metricbeat.yml

# Start Filebeat
ENTRYPOINT ["metricbeat", "-e"]

