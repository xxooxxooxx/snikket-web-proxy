# Snikket web proxy

This component proxies HTTP/HTTPS requests to the right place.
```
cd snikket-web-proxy
docker build -t snikket-web-proxy:my .
docker build --no-cache -t snikket-web-proxy:my .

vi /etc/nginx/nginx.conf

%s/example.com/your.com/g

curl -o docker-compose.yml https://snikket.org/service/resources/docker-compose.beta.yml

docker exec snikket create-invite --admin --group default
```

https://github.com/SaraSmiseth/prosody/blob/dev/readme.md
