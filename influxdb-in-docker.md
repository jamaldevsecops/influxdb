```
version: '3.8'

services:
  influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - "8086:8086"
    environment:
      - INFLUXDB_ADMIN_USER=admin
      - INFLUXDB_ADMIN_PASSWORD=your_admin_pass
    volumes:
      - influxdb_data:/var/lib/influxdb
    networks:
      - grafana_network
    restart: always

  telegraf:
    image: telegraf:latest
    container_name: telegraf
    volumes:
      - telegraf_config:/etc/telegraf
    depends_on:
      - influxdb
    networks:
      - grafana_network
    restart: always

networks:
  grafana_network:
          
volumes:
  influxdb_data:
  telegraf_config:

```
```
docker-compose up -d
```
```
ufw allow 8086/tcp
```

```
http://your_ip_address:8086
```
