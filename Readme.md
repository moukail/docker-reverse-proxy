### Add local domain names in hosts file
In linux
```
sudo nano /etc/hosts
```

In Windows go to C:/system32/drivers/hosts and open it with notepad++

Then add your local domains
````
127.0.0.1   localhost
127.0.0.1   teesing-frontend.dev
127.0.0.1   teesing-backend.dev
````

### Add your local domain in Caddyfile

```
<your-local-domain>:80 {
  reverse_proxy <container-name>:<container-port>
}
```
### Start de reverse proxy
```
docker compose up
```

### In Your Project
in your docker-compose file use expose instead of port in nginx service

````
  nginx:
    container_name: teesing-nginx
    build:
      context: .docker/nginx
    expose:
      - "3000"
      - "3001"
      - "3002"
````

You have to use the same network as the reverse proxy

````
networks:
  default:
    name: logitrade
    external: true
````

start your project

```
docker compose up --build
```

Now you don't have to use a port in your browser just your local domain