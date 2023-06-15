# Project requirements and schedule

## First deliverable

** Delivery date: 14 July 2023 **

** Last update: 5 June 2023 **

Enough functionality to:

1. duplicate bootable 32 GB RaspPi microSDs which have a unique hostname
2. have a running Docker daemon in that image
3. have a private registry for docker images
4. connect the RaspPi to either the school's VCS WiFi network or
   a wired Ethernet network with DHCP
5. act as a WiFi Access Point
5. automatically start the RoboQuest application
6. choose one of those network connections using the HAT UI and
   see the IP address
7. via the browser Robot Console UI
    1. display the telemetry from the HAT
    2. wiggle the drive motors
    3. wiggle the servoes
    4. view the stream of video frames from the robot's camera
8. via ssh to the RaspPi, pull updated versions of the RoboQuest
   docker images
