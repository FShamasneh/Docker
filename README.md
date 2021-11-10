# Docker

## Images

### Commands
- `docker image pull`: is the command to download images. We pull images from repositories inside of remote registries. By default, images will be pulled from repositories on Docker Hub. This command will pull the image tagged as latest from the alpine repository on Docker Hub: `docker image pull alpine:latest`.
- `docker image ls`: lists all of the images stored in your Docker host’s local image cache. To see the SHA256 digests of images add the --digests flag.
- `docker image inspect`: is a thing of beauty! It gives you all of the glorious details of an image — layer data and metadata.
- `docker manifest inspect`: allows you to inspect the manifest list of any image stored on Docker Hub. This will show the manifest list for the redis image: `docker manifest inspect redis`.
- `docker buildx`: is a Docker CLI plugin that extends the Docker CLI to support multi-arch builds.
- `docker image rm`: is the command to delete images. This command shows how to delete the `alpine:latest` image — `docker image rm alpine:latest`. You cannot delete an image that is associated with a container in the running (Up) or stopped (Exited) states.

## Containers

### Commands
- `docker container run`: is the command used to start new containers. In its simplest form, it accepts an image and a command as arguments. The image is used to create the container and the command is the application the container will run when it starts. This example will start an Ubuntu container in the foreground, and tell it to run the Bash shell: `docker container run -it ubuntu /bin/bash`.
- `Ctrl-PQ` will detach your shell from the terminal of a container and leave the container running (UP) in the background.
- `docker container ls`: lists all containers in the running (UP) state. If you add the -a flag you will also see containers in the stopped (Exited) state.
- `docker container exec`: runs a new process inside of a running container. It’s useful for attaching the shell of your Docker host to a terminal inside of a running container. This command will start a new Bash shell inside of a running container and connect to it: `docker container exec -it <container-name or container-id> bash`. For this to work, the image used to create the container must include the Bash shell.
- `docker container stop`: will stop a running container and put it in the Exited (0) state. It does this by issuing a `SIGTERM` to the process with `PID 1` inside of the container. If the process has not cleaned up and stopped within 10 seconds, a `SIGKILL` will be issued to forcibly stop the container. docker container stop accepts container IDs and container names as arguments.
- `docker container start`: will restart a stopped (Exited) container. You can give docker container start the name or ID of a container.
- `docker container rm`: will delete a stopped container. You can specify containers by name or ID. It is recommended that you stop a container with the docker container stop command before deleting it with `docker container rm`.
- `docker container inspect`: will show you detailed configuration and runtime information about a container. It accepts container names and container IDs as its main argument.

### Notes
- Killing the main process in the container will kill the container.
- Press `Ctrl-PQ` to exit the container without terminating its main process.
- Containers are designed to be immutable objects and it’s not a good practice to write data to them.
- Stopping containers gracefully. docker container stop sends a `SIGTERM` signal to the main application process inside the container (PID 1). As we said, this gives the process a chance to clean things up and gracefully shut itself down. If it doesn’t exit within 10 seconds, it will receive a `SIGKILL`. This is effectively the bullet to the head. But hey, it got 10 seconds to sort itself out first.

## Dockerfile
~~Big means slow. Big means hard to work with. And big means more potential vulnerabilities and possibly a bigger attack surface!~~
### Commands
- `docker image build` is the command that reads a Dockerfile and containerizes an application. The `-t` flag tags the image, and the `-f` flag lets you specify the name and location of the Dockerfile. With the -f flag, it is possible to use a Dockerfile with an arbitrary name and in an arbitrary location. The build context is where your application files exist, and this can be a directory on your local Docker host or a remote Git repo.
- The `FROM` instruction in a Dockerfile specifies the base image for the new image you will build. It is usually the first instruction in a Dockerfile and a best-practice is to use images from official repos on this line. The `RUN` instruction in a Dockerfile allows you to run commands inside the image. Each `RUN` instruction creates a single new layer.
- The `COPY` instruction in a Dockerfile adds files into the image as a new layer. It is common to use the `COPY`
instruction to copy your application code into an image.
- The `EXPOSE` instruction in a Dockerfile documents the network port that the application uses.
- The `ENTRYPOINT` instruction in a Dockerfile sets the default application to run when the image is started
as a container.
- Other Dockerfile instructions include `LABEL , ENV , ONBUILD , HEALTHCHECK , CMD` and more…

### Notes
- The process of taking an application and configuring it to run as a container is called **containerizing**
- Containers are all about making apps simple to **build, ship, and run**.
- The process of containerizing an app looks like this:
1. Start with your application code and dependencies
2. Create a *Dockerfile* that describes your app, its dependencies, and how to run it
3. Feed the *Dockerfile* into the `docker image build` command
4. Run container from the image
- A *Dockerfile* is the starting point for creating a container image — it describes an application and tells Docker how to build it into an image.
- All *Dockerfiles* start with the **FROM** instruction. This will be the **base layer** of the image, and the rest of the app will be added on top as additional layers. 
- The `docker image build` command parses the *Dockerfile* one-line-at-a-time starting from the top.
- All non-comment lines are Instructions and take the format `INSTRUCTION argument`. Instruction names are not
case sensitive, but it’s normal practice to write them in UPPERCASE. Some instructions create new layers, whereas others just add metadata to the image config file.
- Examples of instructions that create new layers are `FROM , RUN , and COPY`.
- Examples that create metadata include `EXPOSE , WORKDIR , ENV , and ENTRYPOINT`.
- The basic premise is this — if an instruction is adding **content** such as files and programs to the image, it will create a new layer. If it is adding **instructions** on how to build the image and run the application, it will create metadata.


