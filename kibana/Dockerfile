FROM node:10.21.0-stretch

# Drop everything here
WORKDIR /opt

# Add dependencies
RUN apt update && \
    apt install -y curl tar gzip

# Add Kibana
RUN curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-7.8.1-linux-x86_64.tar.gz && \
    tar zxvf kibana-7.8.1-linux-x86_64.tar.gz --strip-components=1 && \
    rm -rf kibana-7.8.1-linux-x86_64.tar.gz

# Sort out Node for Kibana
RUN rm -rf /opt/node && \
    mkdir -p /opt/node/bin && \
    ln -s /usr/local/bin/node /opt/node/bin/node

# Default Kibana setup
ADD kibana.yml /opt/config/kibana.yml 

# Default Kibana WEB interface port    
EXPOSE 5601

# Run Kibana at start
ENTRYPOINT ["./bin/kibana", "--allow-root"]
