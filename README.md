# frp-docker
[FRP](https://github.com/fatedier/frp) is a fast reverse proxy to help you expose a local server behind a NAT or firewall to the Internet. This is the docker file 
for the frp application.

## Why need FRP
I was running home assistant on raspbery pi on my local network. 
I had no option for port-forward so that I can access raspbery pi from the outside of the home network, I mean from internet.
I was looking for a solution solution to expose my local server to the world.  

## FRP Server
I am running frp server on ec2 and that is why server is based on linux-386. Distro and FRP version can be changed from the  Dockerfile. 

### Use docker to run server
```
docker run --rm \
 -v ${PWD}/frps.ini:/etc/frp/frpcsini:ro \
 --network=host \
maruf571/frp-linux-386-server
```

### Use docker-compose to run the server
```
version: '3'
services:
  frp_server:
    image: maruf571/frp-linux-386-server
    restart: always
    volumes:
      - ./frps.ini:/etc/frp/frps.ini:ro
    network_mode: host
```


## FRP Client
I am running frp client on raspberry pi and that is why client is based on linux-arm. Distro and FRP version can be changed from the  Dockerfile. 

### Use docker to run client 
```
docker run --rm \
 -v ${PWD}/frpc.ini:/etc/frp/frpc.ini:ro \
 --network=host \
maruf571/frp-linux-arm-client
```

### Use docker-compose to run client 
```
version: '3'
services:
  frp_client:
    image: maruf571/frp-linux-arm-client
    restart: always
    volumes:
      - ./frpc.ini:/etc/frp/frpc.ini:ro
    network_mode: host
```



 
