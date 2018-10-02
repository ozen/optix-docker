This repository consists of a Dockerfile to build OptiX-added versions of NVIDIA's CUDA images.

As of this writing, OptiX is free to use within any application, including commercial and educational applications. But to download, you must be a member of NVIDIA Developer Program (which is free), and confirm that you have read and agree to be bound by the SDK license agreement. In order to build an image, you must download OptiX from NVIDIA's [web site] and make sure the extracted directory is inside the context of the build. Please check out Docker Docs if you don't know what that means.

The Dockerfile defines 2 arguments:

	1. CUDA_IMAGE_TAG e.g. `10.0-runtime-ubuntu18.04`, `9.2-devel-ubuntu16.04`, check [CUDA Docker Repository].
	2. OPTIX_VERSION e.g. `5.1.0`, `4.1.1`.

Example build command:

	cp -R /path/to/NVIDIA-OptiX-SDK-5.1.0-linux64 .
	docker build -t optix --build-arg CUDA_IMAGE_TAG=10.0-runtime-ubuntu18.04 build-arg OPTIX_VERSION=5.1.0 .

It is recommended to use [nvidia-docker] to run GPU-enabled containers.

Example run command:

	docker run --runtime=nvidia -it --rm optix /bin/bash

If you want the programs in the container access host machine's X11 server to display something, you can use the following command to share host machine's X11 socket. A search on the internet would reveal other methods to achieve this.

	docker run --runtime=nvidia -it --rm \
    --volume=/etc/group:/etc/group:ro \
    --volume=/etc/passwd:/etc/passwd:ro \
    --volume=/etc/shadow:/etc/shadow:ro \
    --volume=/etc/sudoers:/etc/sudoers:ro \
    --volume=/etc/sudoers.d:/etc/sudoers.d:ro \
    --volume=/tmp/.X11-unix:/tmp/.X11-unix:rw \
    --user=$(id -u) \
    --env="DISPLAY" \
    optix /bin/bash


[CUDA Docker Repository]:https://hub.docker.com/r/nvidia/cuda/
[web site]: https://developer.nvidia.com/designworks/optix/download
[nvidia-docker]: https://github.com/NVIDIA/nvidia-docker
