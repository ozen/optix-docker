FROM nvidia/cuda:10.0-devel-ubuntu18.04
MAINTAINER Yigit Ozen
ADD NVIDIA-OptiX-SDK-5.1.0-linux64 /usr/local/optix
ENV LD_LIBRARY_PATH /usr/local/optix/lib64:${LD_LIBRARY_PATH}
