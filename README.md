# Docker
## Images
### Commands:
- `docker image pull`: is the command to download images. We pull images from repositories inside of remote registries. By default, images will be pulled from repositories on Docker Hub. This command will pull the image tagged as latest from the alpine repository on Docker Hub: `docker image pull alpine:latest`.
- `docker image ls`: lists all of the images stored in your Docker host’s local image cache. To see the SHA256 digests of images add the --digests flag.
- `docker image inspect`: is a thing of beauty! It gives you all of the glorious details of an image — layer data and metadata.
- `docker manifest inspect`: allows you to inspect the manifest list of any image stored on Docker Hub. This will show the manifest list for the redis image: `docker manifest inspect redis`.
- `docker buildx`: is a Docker CLI plugin that extends the Docker CLI to support multi-arch builds.
- `docker image rm`: is the command to delete images. This command shows how to delete the `alpine:latest` image — `docker image rm alpine:latest`. You cannot delete an image that is associated with a container in the running (Up) or stopped (Exited) states.

## Containers
### Commands:
- `docker container run`: is the command used to start new containers. In its simplest form, it accepts an image and a command as arguments. The image is used to create the container and the command is the application the container will run when it starts. This example will start an Ubuntu container in the foreground, and tell it to run the Bash shell: `docker container run -it ubuntu /bin/bash`.
- Ctrl-PQ will detach your shell from the terminal of a container and leave the container running (UP) in the background.
- `docker container ls`: lists all containers in the running (UP) state. If you add the -a flag you will also see containers in the stopped (Exited) state.
- `docker container exec`: runs a new process inside of a running container. It’s useful for attaching the shell of your Docker host to a terminal inside of a running container. This command will start a new Bash shell inside of a running container and connect to it: `docker container exec -it <container-name or container-id> bash`. For this to work, the image used to create the container must include the Bash shell.
- `docker container stop`: will stop a running container and put it in the Exited (0) state. It does this by issuing a `SIGTERM` to the process with `PID 1` inside of the container. If the process has not cleaned up and stopped within 10 seconds, a `SIGKILL` will be issued to forcibly stop the container. docker container stop accepts container IDs and container names as arguments.
`docker container start`: will restart a stopped (Exited) container. You can give docker container start the name or ID of a container.
`docker container rm`: will delete a stopped container. You can specify containers by name or ID. It is recommended that you stop a container with the docker container stop command before deleting it with `docker container rm`.
`docker container inspect` will show you detailed configuration and runtime information about a container. It accepts container names and container IDs as its main argument.
### Notes:
- Killing the main process in the container will kill the container.
- Press `Ctrl-PQ` to exit the container without terminating its main process.
- Containers are designed to be immutable objects and it’s not a good practice to write data to them.
- Stopping containers gracefully. docker container stop sends a `SIGTERM` signal to the main application process inside the container (PID 1). As we said, this gives the process a chance to clean things up and gracefully shut itself down. If it doesn’t exit within 10 seconds, it will receive a `SIGKILL`. This is effectively the bullet to the head. But hey, it got 10 seconds to sort itself out first.
- 
