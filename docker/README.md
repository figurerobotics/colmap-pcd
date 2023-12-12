# How to build COLMAP-PCD using Docker

## Requirements
- A linux based host machine with at least one NVIDIA GPU<sup>[1](#f1)</sup>.

## Quick Start:

1. Check that Docker >=19.03<sup>[2](#f2)</sup> installed on your host machine:

`docker --version`

2. Check that you have an NVIDIA driver installed on your host machine<sup>[5](#f5)</sup>:

`nvidia-smi`

3. If GUI interface is perferred, run 

`make run-gui`

4. If command line is fine, run

`make run-term`


## Notes

Running COLMAP binaries can use a lot of memory (depending on the size of your
data set / imagery). Docker has a relatively small default memory setting
(2Gb on Mac). You will probably want to increase this before you run any larger
workflows. From Docker desktop on Mac for example, just open the Docker GUI, go
to the *Advanced* tab and increase via the slider:

![](docker-memory-settings.png?raw=true)

<a name="f1">1</a>: COLMAP needs NVIDA GPU compute hardware for dense reconstruction (as of 12/10/2019), and is optional for feature extraction and matching.

<a name="f2">2</a>: This is because Docker 19.03+ natively supports NVIDIA GPUs.

<a name="f3">3</a>: You should get a similar output to what you get when you ran step 2 on your host, since the docker container is detecting the same GPU(s). If you have trouble, you may want to read the [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) webpage, as the scripts `./setup-ubuntu.sh` and `./setup-centos.sh` are based on instructions posted there and may change over time.

<a name="f4">4</a>: Right now this workflow is designed to build the latest release of COLMAP. To build a specific release, open up the Dockerfile and append '--branch *RELEASE_TAG*' as indicated in the Dockerfile, with *RELEASE_TAG* being the specific release you want to build.

<a name="f5">5</a>: If it is not yet installed, install an NVIDIA driver and NVIDIA container runtime:

```
sudo apt install ubuntu-drivers-common
sudo ubuntu-drivers autoinstall
```

If you failed to install the above, check the appropriate NVIDIA driver by yourself and install it:

```
ubuntu-drivers devices
e.g.
sudo apt install nvidia-driver-455
```

ref: “https://collabnix.com/introducing-new-docker-cli-api-support-for-nvidia-gpus-under-docker-engine-19-03-0-beta-release/”
