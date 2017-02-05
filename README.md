As of this writing, OptiX 4 is free to use within any application, including commercial and educational applications. But to download, you must be a member of NVIDIA DesignWorks (which is free) and confirm that you have read and agree to be bound by the SDK license agreement.

This repository includes Dockerfiles to build OptiX-added versions of NVIDIA's CUDA images. In order to build an image, you must download OptiX from NVIDIA's [web site] and make sure the extracted directory is inside the context of the build. Please check out Docker Docs if you don't know what that means.

It is recommended to use [nvidia-docker] to run GPU-enabled containers.

Example build command:

	docker build -t optix:4.0.2 -f ubuntu-14.04/cuda-7.5/optix-4.0.2/Dockerfile

[web site]: https://developer.nvidia.com/designworks/optix/download
[nvidia-docker]: https://github.com/NVIDIA/nvidia-docker
