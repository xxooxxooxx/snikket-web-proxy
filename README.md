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
```
The following ports are exposed:

5000: proxy65 port used for file sharing
5222: c2s port (client to server)
5223: c2s legacy ssl port (client to server)
5269: s2s port (server to server)
5347: XMPP component port
5280: BOSH / websocket port
5281: Secure BOSH / websocket port


127.0.0.1:5765 snikket web
127.0.0.1:5280 BOSH / websocket port


tcp        0      0 0.0.0.0:5223            0.0.0.0:*               LISTEN      497375/lua5.2
tcp        0      0 0.0.0.0:5222            0.0.0.0:*               LISTEN      497375/lua5.2
tcp        0      0 0.0.0.0:5269            0.0.0.0:*               LISTEN      497375/lua5.2
tcp        0      0 0.0.0.0:5000            0.0.0.0:*               LISTEN      497375/lua5.2

tcp        0      0 0 0.0.0.0:3478      0.0.0.0:*               LISTEN      11097/turnserver
udp        0      0 0 0.0.0.0:3478      0.0.0.0:*                           11097/turnserver

tcp        0      0 0 0.0.0.0:5349      0.0.0.0:*               LISTEN      11097/turnserver
udp        0      0 0 0.0.0.0:5349      0.0.0.0:*                           11097/turnserver


    upstream web4_1 {
    server 10.10.10.99:5000;
    }
    upstream web4_2 {
    server 10.10.10.99:5222;
    }
    upstream web4_3 {
    server 10.10.10.99:5223;
    }
    upstream web4_4 {
    server 10.10.10.99:5269;
    }

    upstream web4_5 {
    server 10.10.10.99:3478;
    }
    upstream web4_6 {
    server 10.10.10.99:5349;
    }


      server {
      listen 5000;
      proxy_pass web4_1;
      }
      server {
      listen 5222;
      proxy_pass web4_2;
      }
      server {
      listen 5223;
      proxy_pass web4_3;
      }
      server {
      listen 5269;
      proxy_pass web4_4;
      }
      server {
      listen 3478 udp;
      proxy_pass web4_5;
      }
      server {
      listen 3478;
      proxy_pass web4_5;
      }
      server {
      listen 5349 udp;
      proxy_pass web4_6;
      }
      server {
      listen 5349;
      proxy_pass web4_6;
      }

      反代并在运行在隧道内
```
```
Firewall rules settings
The port used by the TURN server needs to be public, so add the following settings to the firewall.

Protocol	PORT
TCP	32355-65535, 3478-3479
UDP	32355-65535, 3478-3479
```
https://github.com/coturn/coturn/wiki/turnserver  
```
# TURN Server public/private address mapping, if the server is behind NAT.
# In that situation, if a -X is used in form "-X <ip>" then that ip will be reported
# as relay IP address of all allocations. This scenario works only in a simple case
# when one single relay address is be used, and no RFC5780 functionality is required.
# That single relay address must be mapped by NAT to the 'external' IP.
# The "external-ip" value, if not empty, is returned in XOR-RELAYED-ADDRESS field.
# For that 'external' IP, NAT must forward ports directly (relayed port 12345
# must be always mapped to the same 'external' port 12345).
#
# In more complex case when more than one IP address is involved,
# that option must be used several times, each entry must
# have form "-X <public-ip/private-ip>", to map all involved addresses.
# RFC5780 NAT discovery STUN functionality will work correctly,
# if the addresses are mapped properly, even when the TURN server itself
# is behind A NAT.
#
# By default, this value is empty, and no address mapping is used.
#
#external-ip=60.70.80.91
#
#OR:
#
#external-ip=60.70.80.91/172.17.19.101
#external-ip=60.70.80.92/172.17.19.102
```
