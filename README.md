Openpose dockerized flask microservice

Dockerized openpose web microservice based on flask with thin cpu implementation of pose estimation. Suitable for systems, when you need isolated pose estimation service. Microservice based on https://github.com/facebookresearch/DensePose/

Postman documentation https://www.getpostman.com/collections/a108214eff536f4bbcd5


```
Run
sudo docker build -t densepose:c2-cuda9-cudnn7 .
sudo nvidia-docker run --rm -p 5000:5000 -t -d densepose:c2-cuda9-cudnn7

For debug
sudo nvidia-docker run --rm -p 5000:5000 -it densepose:c2-cuda9-cudnn7 bash
```



ML GPU docker environment installation for ubuntu 18.04 server 
```

1 install cuda
https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=debnetwork

2 check installation
nvidia-smi
You will see you GPU

3 docker installation
https://docs.docker.com/install/linux/docker-ce/ubuntu/

4 install Nvidia docker
https://github.com/NVIDIA/nvidia-docker
```

