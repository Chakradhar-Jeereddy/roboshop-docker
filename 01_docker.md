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
2) Docker Daemon: CLI -> dockerd -> containerd -> runc(only starts/stops/manages) containers. 
   - runc - low level engine doesn't pull, build image, manage network and volumes.
3) Container: run time of the image
4) runC: low-level container runtime

runc
==
- Low-level tool
- Actually creates and runs the container
- Talks directly to the Linux kernel
- Starts/stops container processes
- Think: engine starter

containerd
==
- Higher-level service
- Manages container lifecycle
- Handles:
  - Image pull
  - Storage
  - Networking hooks
  - Think: container manager

How they work together
==
1️. Kubernetes / Docker says:
  - “Run this container”
2. containerd:
  - “Okay, I’ll manage it”
3. containerd calls runc:
  - “Create and start the container”
4. runc:
  - “Done"

Real-world analogy
==
| Role           | Real life         |
|---------------|-------------------|
| Kubernetes    | Company           |
| containerd    | Project manager   |
| runc          | Machine operator  |
| Linux kernel  | Factory           |
