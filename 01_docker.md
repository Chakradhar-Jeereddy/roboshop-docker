## Dokcer objects
- Volumes/Storage
- Networking
- Containers
- Images(Local/remote)

- When you run docker run command, it checks wether image is locally 
  available, if not, it will pull it from hub. Creates a container and sends
  response to client.

***Architechture:***
1) Client - : Command utility
2) Docker Daemon: dockerd
3) Container: run time of the image
4) runC: low-level container runtime

***Docker Objects:***
