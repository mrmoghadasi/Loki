# Grafana-Loki Project

![Loki version](https://img.shields.io/badge/Loki%20version-2.8.0-blue)

Loki is a horizontally-scalable, highly-available, multi-tenant log aggregation system inspired by Prometheus. It is designed to be very cost effective and easy to operate. It does not index the contents of the logs, but rather a set of labels for each log stream.

## Key concepts
**Services:**

- promtail  = is the agent, responsible for gathering logs and sending them to Loki.
- loki = is the main server, responsible for storing logs and processing queries.
- grafana = for querying and displaying the logs.
- nginx = this service runs a secure Nginx container configured with basic authentication to proxy access to the Loki web interface.

**Volumes:**

`/opt/loki/config/loki-config.yml` mounted to `/etc/loki/loki-config.yml` in the Loki container allows you to customize Loki configuration.
`/volumes/loki` mounted to `/loki` in the Loki container provides persistent storage for logs.
`/opt/loki/config/promtail-config.yml` mounted to `/etc/promtail/promtail-config.yml` in the Promtail container allows customization of log collection rules.
`/var/log/auth.log` mounted to `/var/log/auth.log` in the Promtail container allows collecting system logs (replace with your desired log location).
`/opt/loki/config/grafana-defaults.ini` mounted to `/usr/share/grafana/conf/defaults.ini` in the Grafana container allows configuration overrides for Grafana.
`/volumes/grafana` mounted to `/var/lib/grafana` in the Grafana container provides persistent storage for Grafana data.

**Ports:**

    - Loki: 3100 (container) -> 3100 (host) - Exposes the Loki web interface.
    - Promtail: None (runs in the background)
    - Grafana: 3000 (container) -> 3000 (host) - Exposes the Grafana interface.
    -   Nginx:
        - 3200 (container) -> 3200 (host) - Exposes the Nginx proxy interface.
        - 8090:8090 (optional) - Exposes the Nginx admin interface for configuration (if needed).

**Nginx Authentication:**

Basic authentication is enabled using environment variables:
    - BASIC_AUTH_USERNAME: Username for accessing Loki (default: loki_user)
    - BASIC_AUTH_PASSWORD: Password for accessing Loki (default: loki_password)

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
cp grafana-defaults.ini /opt/loki/config/
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

5. Start deploy whith dockercCompose:
```
docker-compose up -d
```


## License

[MIT](https://choosealicense.com/licenses/mit/) 
This project is licensed under the MIT License.

## Credits

This project was created by My User (mrm.elec@email.com)

[![LinkedIn](https://img.shields.io/badge/-LinkedIn-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/mohamad-reza-moghadasi-5755b959/)](https://www.linkedin.com/in/mohamad-reza-moghadasi-5755b959/) [![Gmail](https://img.shields.io/badge/-Gmail-red?style=flat-square&logo=Gmail&logoColor=white&link=mailto:mrm.elec@gmail.com)](mailto:mrm.elec@gmail.com)



