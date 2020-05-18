FROM golang

# Pull the ElasticSearch Beats Source Files and
# ignore error "package github.com/elastic/beats: build constraints exclude all Go files in /go/src/github.com/elastic/beats"
RUN go get github.com/elastic/beats || true
# Build and install filbeat
RUN cd src/github.com/elastic/beats/ && \
    git checkout 7.6 && \
    cd x-pack/filebeat/ && \
    go build && \
    go install

# Add the custom config and other files from https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.2-linux-x86_64.tar.gz
ADD files .

# Enable the modules
RUN rm kibana/7/dashboard/Filebeat-aws-elb-overview.json
RUN rm kibana/7/dashboard/Filebeat-aws-vpcflow-overview.json

# Expose ports for netflow and syslog
EXPOSE 2055 2055/udp 9000 9000/udp

# Start Filebeat
ENTRYPOINT ["filebeat", "-e"]

#docker exec -it filebeat bash -c "filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=[\"elasticsearch:9200\"]'"
#docker exec -it filebeat bash -c "filebeat setup --dashboards"
