# Docker
## Images - The commands:
- `docker image pull`: is the command to download images. We pull images from repositories inside of remote registries. By default, images will be pulled from repositories on Docker Hub. This command will pull the image tagged as latest from the alpine repository on Docker Hub: `docker image pull alpine:latest`.
- `docker image ls`: lists all of the images stored in your Docker host’s local image cache. To see the SHA256 digests of images add the --digests flag.
- `docker image inspect`: is a thing of beauty! It gives you all of the glorious details of an image — layer data and metadata.
- `docker manifest inspect`: allows you to inspect the manifest list of any image stored on Docker Hub. This will show the manifest list for the redis image: `docker manifest inspect redis`.
- `docker buildx`: is a Docker CLI plugin that extends the Docker CLI to support multi-arch builds.
- `docker image rm`: is the command to delete images. This command shows how to delete the `alpine:latest` image — `docker image rm alpine:latest`. You cannot delete an image that is associated with a container in the running (Up) or stopped (Exited) states.