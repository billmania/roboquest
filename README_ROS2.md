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
    ROS2 uses shared memory to communicate between nodes on the same host. Both
    containers must execute as the same user, in order to use shared memory.

```
docker run -d --rm \
    --network host \
    --ipc host \
    -v /dev/shm:/dev/shm \
    -v /var/run/dbus:/var/run/dbus \
    --device /dev/gpiomem \
    --device /dev/ttyS0 \
    --device /dev/video0 \
    --device /dev/i2c-1 \
    --name roboquest_core \
    roboquest_core
```
    2. docker-compose
```
docker-compose up -d
```

To manually start the USB camera node:
ros2 run usb_cam usb_cam_node_exe

To view the published frames from the USB camera, use rviz2 with
"default_cam" as the frame and "/image_raw" as the topic.
