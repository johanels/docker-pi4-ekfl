# docker-pi4-ekfm
Docker -> pi4 -> ElasticSearch + Kibana + Filebeat + Metricbeat

Wanted to get a small ElasticSearch going for home LAB with basic monitoring and testing. This runs on a Raspberry Pi4 4Gb RAM with a 64Gb Class10 MicroSD.
I have my boundary router sending 1Gbps ISP NETFLOW directly into Filebeat. Packet sniffing also works... For a little while... Be warned...

Running Ubuntu 64bit on the Pi4.

```
sudo sysctl -w vm.max_map_count=262144
```

Open http://server:5601 and login using elastic and 12345678.

Please note:

- Licenses where due
- Home LAB only, many default password
- No SSL encryption
- Use at own risk
- NETFLOW data can contain private information, so respect the users on the network