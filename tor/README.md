# tor

The smallest (**15 MB**) docker image with Tor and Privoxy on Alpine Linux.
Forked from [rdsubhas/tor-privoxy-alpine](https://github.com/rdsubhas/docker-tor-privoxy-alpine) with minor changes for the ability to mount the config files. To use it on a mac, make sure VirtualBox port forwards port 8118 to localhost. Then System Preferences -> Network -> Advanced (from the active connection). On the Proxies tab turn on both "Web Proxy" and "Secure Web Proxy" and add server "127.0.0.1" and port "8118".

### Use

```
# build image
docker build --force-rm -t gpavlidi/tor .

# default settings
docker run -d -p 8118:8118 --name tor gpavlidi/tor

# override settings
docker run -d -p 8118:8118 --name tor -v ~/Code/tools/tor/configs:/root/configs:ro gpavlidi/tor

# try it
curl --proxy localhost:8118 https://check.torproject.org/api/ip
curl --proxy http://$TOR_PORT_8118_TCP_ADDR:$TOR_PORT_8118_TCP_PORT https://check.torproject.org/api/ip
http_proxy=localhost:8118 wget -O - -Y on http://ip-api.com/json

# when editing the config files, just kill the process in the bottom level
# runit will launch it again
```
