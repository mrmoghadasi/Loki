# Grafana-Loki Project

![Loki version](https://img.shields.io/badge/Loki%20version-2.8.0-blue)

Loki is a horizontally-scalable, highly-available, multi-tenant log aggregation system inspired by Prometheus. It is designed to be very cost effective and easy to operate. It does not index the contents of the logs, but rather a set of labels for each log stream.

## Key concepts

- promtail  = is the agent, responsible for gathering logs and sending them to Loki.
- loki = is the main server, responsible for storing logs and processing queries.
- grafana = for querying and displaying the logs.

## Requirements

- Docker
- Docker Compose

# Deploy

1. Clone the repository
```
git clone https://github.com/mrmoghadasi/Loki.git
```

2. Create Config directory
```
mkdir -p /opt/loki/config/
```


3. Navigate to the project directory:
```
cd Loki
cp promtail-config.yml /opt/loki/config/
cp loki-config.yml /opt/loki/config/
cp defaults-grafana.ini /opt/loki/config/
```

4. Create volume directory
```
mkdir -p /volumes/grafana
mkdir -p /volumes/loki
```

5. Fixing permissions
```
sudo chown 10001:10001 /volumes/loki
sudo chown 472:472 /volumes/grafana
```

