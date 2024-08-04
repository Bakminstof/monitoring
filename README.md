Мониторинг ресурсов для

Для получения метрик с Node-exporter в конфигурации Prometheus 
(grafana-prometheus/volumes/prometheus/prometheus.yml) нужно добавить хост Node-exporter
```
- job_name: "node-exporter"

static_configs:
  - targets: ["NODE_EXPORTER_HOST:9100"]
```

Запуск Node-exporter
```shell
cd node-exporter

docker-compose up --build -d
```

Запуск Grafana и Prometheus
```shell
cd grafana-prometheus

docker-compose up --build -d
```
В настройках Grafana в конфигурациях базы данных указать Prometheus с адресом http://prometheus:9090
Дашборды для Grafana [тут](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)

[Prometheus](http://localhost:9090)
[Grafana](http://localhost:3000)  

