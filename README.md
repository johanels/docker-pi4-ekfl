# docker-pi4-ekfl
Docker -> pi4 -> ElasticSearch + Kibana + Filebeat + Metricbeat

Wanted to get a small ElasticSearch going for home LAB with basic monitoring and testing. This runs on a Raspberry Pi4 4Gb RAM with a 64Gb Class10 MicroSD.
I have my boundary router sending 1Gbps ISP NETFLOW directly into Filebeat.

Running Ubuntu 64bit on the Pi4.

'''bash
sudo sysctl -w vm.max_map_count=262144
'''

References:

https://www.elastic.co/guide/en/elasticsearch/reference/7.6/security-settings.html#api-key-service-settings

After bringing it up, make sure you update the Kibana password using the below:

bash```
curl -H 'Content-Type:application/json' -XPUT http://elastic:12345678@10.1.1.7:9200/_xpack/security/user/kibana/_password -d "{\"password\": \"12345678\"}"
```

Please note:

- Licenses where due
- Home LAB only, many default password
- No SSL encryption
- Use at own risk
- NETFLOW data can contain private information, so respect the users on the network