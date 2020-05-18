# Alphine version for Node v10.19
FROM alpine:3.10

# Drop everything here
WORKDIR /opt

# Add dependencies
RUN apk add --no-cache --update curl tar gzip

# Add Kibana
RUN curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-7.6.2-linux-x86_64.tar.gz && \
    tar zxvf kibana-7.6.2-linux-x86_64.tar.gz --strip-components=1 && \
    rm -rf kibana-7.6.2-linux-x86_64.tar.gz

# Sort out Node v10.19 for Kibana 7.6.2
RUN apk add --no-cache --update nodejs
RUN rm -rf /opt/node
RUN mkdir -p /opt/node/bin
RUN ln -s /usr/bin/node /opt/node/bin/node

# Default Kibana setup
ADD kibana.yml /opt/config/kibana.yml

# Default Kibana WEB interface port    
EXPOSE 5601

# Run Kibana at start
ENTRYPOINT ["./bin/kibana", "--allow-root"]

