```
version: '3.8'

services:
  influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - "8086:8086"
    environment:
      - INFLUXDB_DB=telegraf
      - INFLUXDB_ADMIN_USER=admin
      - INFLUXDB_ADMIN_PASSWORD=your_admin_password
      - INFLUXDB_USER=telegraf
      - INFLUXDB_USER_PASSWORD=your_telegraf_password
    volumes:
      - influxdb_data:/var/lib/influxdb
    networks:
      - grafana_network

  telegraf:
    image: telegraf:latest
    container_name: telegraf
    volumes:
      - telegraf_config:/etc/telegraf
    depends_on:
      - influxdb
    networks:
      - grafana_network

networks:
  grafana_network:

volumes:
  influxdb_data:
  telegraf_config:
```
