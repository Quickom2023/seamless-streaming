## Requirements
### Linux
- Driver NVIDIA
``` sh
# Display current status of all NVIDIA GPUs
nvidia-smi
```
- NVIDIA Container Toolkit
``` sh
# Add the package repositories
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit

sudo systemctl restart docker
```

## Installation
1. Clone the repository:
``` sh
git clone https://github.com/tyanfarm/seamless-streaming
```

2. Open folder: 
``` sh
cd seamless-streaming
```

3. Check if container can use GPU
``` sh
docker run -it --rm --gpus all ubuntu nvidia-smi -L
```

4. Build docker image
``` sh
DOCKER_BUILDKIT=1 docker build -t seamless-app:latest .
```

5. Build docker container
``` sh
docker run --gpus all -p 7860:7860 --name seamless-container seamless-app:latest
```

5. Check logs
``` sh
docker logs -f seamless-container
```

The server will listen on port 7680 by default. 