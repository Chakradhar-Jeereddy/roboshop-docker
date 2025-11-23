```
***Ethernet network***
ens5: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 10.0.1.178  netmask 255.255.255.0  broadcast 10.0.1.255
        inet6 fe80::a7:76ff:fef9:291f  prefixlen 64  scopeid 0x20<link>
        ether 02:a7:76:f9:29:1f  txqueuelen 1000  (Ethernet)
        RX packets 625970  bytes 905835020 (863.8 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 166914  bytes 36217699 (34.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
````
#### A default interface is created while installing docker engine
#Docker creates its own subnet.
```
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::2017:48ff:fe7a:ad1b  prefixlen 64  scopeid 0x20<link>
        ether 22:17:48:7a:ad:1b  txqueuelen 0  (Ethernet)
        RX packets 13886  bytes 1052418 (1.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15068  bytes 84300007 (80.3 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
***Note*** : Default docker virtual network interface doesn't provide communication between containers

There are two networks
 1) Host network (directly connected to host, no need docker intrface)
 2) Bridge network (created by docker and allocates ips to container)

docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
f01ec7be2469   bridge    bridge    local
a404c6b1189f   host      host      local
138661abc2c3   none      null      local
 
docker run -d --network host nginx (this will directly open the port on host)  -> this is not recommended.

Error
===
2025/11/23 20:32:31 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

## Recommended approach
1) Use bridge network
2) Create your own interface

## command
```
Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks
```

```
docker network create roboshop

docker network ls
NETWORK ID     NAME       DRIVER    SCOPE
f01ec7be2469   bridge     bridge    local
a404c6b1189f   host       host      local
138661abc2c3   none       null      local
f28500911e7c   roboshop   bridge    local
```

## Disconnect containers from default bridge network
docker network disconnect bridge mongodb
docker network disconnect bridge catalogue

# Connect containers to roboshop network
docker network connect   roboshop catalogue