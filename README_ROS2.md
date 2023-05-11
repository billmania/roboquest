# Deploy via docker

1. Start with a Raspberry Pi 4B
```
Hardware    : BCM2835
Revision    : c03112
Model       : Raspberry Pi 4 Model B Rev 1.2
```
2. Install Raspberry Pi OS Bullseye and docker Server 23.0.3
3. cd to roboquest/ros2ws
4. Build the images
    1. docker
```
docker build -t roboquest_core -f Dockerfile.roboquest_core .
```
    2. docker-compose
```
docker-compose build
```
5. Start the containers
    1. docker
```
docker run -it --rm \
    --network host \
    --device /dev/gpiomem \
    --device /dev/ttyS0 \
    --name roboquest_core \
    roboquest_core
```
    2. docker-compose
```
docker-compose up -d
```

