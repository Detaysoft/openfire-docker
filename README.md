# Openfire Docker

## Using Docker-Compose

```
services:
  openfire1:
    restart: always
    image: abdurrahmanekr/openfire:<openfire version>-apm
    pid: "host"
    ports:
      - "7070:7070"
      - "9090:9090"
    volumes:
      - 'openfire-data:/var/lib/openfire'
      - 'openfire-plugins:/usr/share/openfire/plugins'
      - 'openfire-lib:/usr/share/openfire-custom-libs'
    environment:
      APM_HOST: 'beat'
    networks:
      - apm

volumes:
  openfire-data:
  openfire-plugins:
  openfire-lib:
  openfire-mysql:
  openfire-mysql-log:

networks:
  apm:
    driver: bridge
```

### Compiling

```
docker build -t abdurrahmanekr/openfire:<openfire version> .
```