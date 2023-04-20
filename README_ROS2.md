# Deploy via docker

1. Start with a Raspberry Pi 4B
```
Hardware    : BCM2835
Revision    : c03112
Model       : Raspberry Pi 4 Model B Rev 1.2
```
2. Install Raspberry Pi OS Bullseye and docker Server 23.0.3
3. cd to roboquest/ros2ws
4. Build the image
```
docker build -t roboquest_core -f Dockerfile.roboquest_core .
```
5. Start the container
```
docker run -it --rm \
    --name roboquest_core \
    roboquest_core \
    /bin/bash

source /opt/ros/humble/setup.bash
source install/setup.bash
