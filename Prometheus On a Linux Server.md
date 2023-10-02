# Steps to Install and Configure Prometheus On a Linux Server:

https://devopscube.com/install-configure-prometheus-linux/

- Login as root using **sudo su -** command.

### Setup Prometheus Binaries:
```shell
yum update -y
wget https://github.com/prometheus/prometheus/releases/download/v2.47.0/prometheus-2.47.0.linux-amd64.tar.gz
tar -xvzf prometheus-2.47.0.linux-amd64.tar.gz
mv prometheus-2.22.0.linux-amd64 prometheus-files
```

### Create a Prometheus user, and required directories, and make Prometheus user as the owner of those directories:

```shell
useradd --no-create-home --shell /bin/false prometheus
mkdir /etc/prometheus/ /var/lib/prometheus/
chown prometheus:prometheus /etc/prometheus /var/lib/prometheus
```

### Copy prometheus and promtool binary from prometheus-files folder to /usr/local/bin and change the ownership to prometheus user:

```shell
cp prometheus-files/prometheus /usr/local/bin/
cp prometheus-files/promtool /usr/local/bin/
chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool

cp -r prometheus-files/consoles /etc/prometheus
cp -r prometheus-files/console_libraries /etc/prometheus
chown -R prometheus:prometheus /etc/prometheus/consoles /etc/prometheus/console_libraries
```
---
### Setup Prometheus Configuration

```shell
vi /etc/prometheus/prometheus.yml

global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']

chown prometheus:prometheus /etc/prometheus/prometheus.yml
```

```shell
vi /etc/systemd/system/prometheus.service

[Unit]
Description=Prometheus Server
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```
```shell
systemctl daemon-reload
systemctl enable prometheus
systemctl start prometheus

systemctl status prometheus
```

- Use server's public ip to access the Prometheus

http://[prometheus-ip]:9090/graph

---

# Installing Grafana on an Amazon Linux server:

https://grafana.com/grafana/download?edition=oss

```shell
dnf update -y
dnf install -y https://dl.grafana.com/oss/release/grafana-10.1.4-1.x86_64.rpm
```

**To start the grafana server**

```shell
systemctl daemon-reload
systemctl enable grafana-server
systemctl start grafana-server

systemctl status grafana-server
```
