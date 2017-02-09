This repository includes Dockerfiles to build OptiX-added versions of NVIDIA's CUDA images. As of this writing, OptiX 4 is free to use within any application, including commercial and educational applications. But to download, you must be a member of NVIDIA DesignWorks (which is free) and confirm that you have read and agree to be bound by the SDK license agreement. In order to build an image, you must download OptiX from NVIDIA's [web site] and make sure the extracted directory is inside the context of the build. Please check out Docker Docs if you don't know what that means.

It is recommended to use [nvidia-docker] to run GPU-enabled containers.

Example build command:

	cp -R /path/to/NVIDIA-OptiX-SDK-4.0.2-linux64 .
	docker build -t optix:4.0.2 -f ubuntu-14.04/cuda-7.5/optix-4.0.2/Dockerfile

Example run command:

	nvidia-docker run -it --rm pyoptix:4.0.2 /bin/bash

If you want the programs in the container access host machine's X11 server to display something, you can use the following command to share host machine's X11 socket. A search on the internet would reveal other methods to achieve this.

	nvidia-docker run -it --rm \
    --volume="/home/$USER:/home/$USER" \
    --volume=/etc/group:/etc/group:ro \
    --volume=/etc/passwd:/etc/passwd:ro \
    --volume=/etc/shadow:/etc/shadow:ro \
    --volume=/etc/sudoers:/etc/sudoers:ro \
    --volume=/etc/sudoers.d:/etc/sudoers.d:ro \
    --volume=/tmp/.X11-unix:/tmp/.X11-unix:rw \
    --user=$(id -u) \
    --env="DISPLAY" \
    --workdir="/home/$USER" \
    pyoptix:4.0.2 /bin/bash


[web site]: https://developer.nvidia.com/designworks/optix/download
[nvidia-docker]: https://github.com/NVIDIA/nvidia-docker
