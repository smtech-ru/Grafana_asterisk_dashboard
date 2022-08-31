# Grafana asterisk dashboard
## Asterisk Configuration
To collect metrics, you need to enable the embedded prometheus_exporter for asterisk.


Сreate configuration files on asterisk server `prometheus.conf` и `http.conf`

Example config `prometheus.conf`
```
[general]
enabled = yes
core_metrics_enabled = yes
uri = metrics
```

Example config `http.conf`
```
[general]
enabled=yes
enablestatic=yes
bindaddr=0.0.0.0
bindport=8088
prefix=
sessionlimit=100
session_inactivity=30000
session_keep_alive=15000
```

## Prometheus Configuration
Example config:
```
  - job_name: "asterisk_exporter"
    scrape_interval: 10s
    static_configs:
      - targets: ["localhost:8088"]        #IP-address Asterisk Server
        labels:
          id: "Asterisk"
```

## View Metrics
You can view the resulting metrics using the following command: 

`curl http://localhost:8088/metrics`

## Metrics
* asterisk_channels_count
* asterisk_calls_sum
* asterisk_calls_count
* asterisk_channels_state
* asterisk_channels_duration_seconds
* asterisk_endpoints_count
* asterisk_endpoints_state
* asterisk_endpoints_channels_count
* asterisk_bridges_count
* asterisk_bridges_channels_count
* asterisk_core_properties
* asterisk_core_uptime_seconds
* asterisk_core_last_reload_seconds
* asterisk_core_scrape_time_ms

## General rows
General information about the asterisk server

![image alt](/images/general_rows.png)

## States rows
Information about the status of channels state, endpoint state and channels duration seconds

![image alt](/images/States_rows.png)

## Statistics rows
Graph

![image alt](/images/Statistics_rows.png)

#### The project was completed by [SN](https://github.com/StanislavVN) working after [SPbEC-Mining Ltd](https://github.com/smtech-ru).
