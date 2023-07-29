# Snikket web proxy

This component proxies HTTP/HTTPS requests to the right place.
```
cd snikket-web-proxy
docker build -t snikket-web-proxy:my .
docker build --no-cache -t snikket-web-proxy:my .

vi /etc/nginx/nginx.conf

%s/example.com/your.com/g
```

https://github.com/SaraSmiseth/prosody/blob/dev/readme.md
