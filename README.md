# Grafana Agent on-premises!

Ever wondered if you can use the easy peasy Grafana Agent without Grafana Cloud?

For example, along with your **ON-PREMISES deployments of  Prometheus, Loki and Tempo?** 
Answer is **YES, OF COURSE**.


This repo just shows the basics and it's a one-shot working config to build on.

# Remote write

The harder bits to set up are the **remote_write** configs for Prometheus, Loki, etc.
For example, for Prometheus:
```yml
metrics:
  global:
    remote_write:
      - url: http://prometheus:9090/api/v1/write
```


and for Loki
```yml
logs:
  configs:
    ..
    clients:
      - url: http://loki:3100/loki/api/v1/push
```

You can even configure different scrapes to send metrics to distinct remote write endpoints, but I won't be going into that for now.

Please have a look at

    ./conf/grafana-agent/agent-linux.yaml

The rest is basically boilerplate config.

# How to test it yourself

Clone the repo


    docker-compose up -d

In your browser, go to localhost:3000 and log into Grafana with admin/admin.
Click explore, select one of the provisioned Prometheus or Loki datasources and begin querying your scraped metrics and logs!

## NEVER, EVER use this in production
This **repo lacks any kind of security, scalability that you DEFINITELY NEED for anything close to a production workload**.
