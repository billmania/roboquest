# Theory of Operations

## Summary

The purpose of this application is to control a small, mobile
robot from a browser. The robot has a limited collection of
sensors, the ability to move in the horizontal plane, and the
ability to control some servoes. Information from the sensors is
displayed on the browser. The robot's actuators, both drive
motors and servoes, can be controlled from the browser.

## Logging

Operating system log files are in /var/log. ROS log files are on
the host OS in /var/lib/docker/volumes/ros_logs/_data. They're
made available to the Docker containers as a docker volume named
"ros_logs".

Both the OS log files and the ROS log files are rotated aggressively,
the former via logrotate and the latter via a few lines at the end of
/etc/rc.local.

## Basic data flow

The robot automatically and continuously publishes measurements
from its sensors. These include voltage and amperage measurements
from the power system. Video frames from USB cameras are sent to
the browser. Lastly, there are five ADC channels whose
measurements are also sent to the browser.

In the other direction, the browser can control the state of the
battery charger for the power system. It can set the velocity of
each of two drive motors. Finally, it can set the position of
sixteen servoes.

Measurement and status information from the robot is sent to
the browser in a continuous stream. The browser extracts individual
values and uses them to update widgets on the page. The video
frames are displayed as the background of the browser page.

The browser has control widgets for the charger, drive motors,
and servoes' OFF and ON state. It also has velocity and position
controls for the combined drive motors and individual servoes,
respectively.

There is functionality at the browser to also manage the
application, in terms of its configuration and run state.

## Implementation

### Versions

The operating system is Raspberry Pi OS Debian 11 bullseye
aarch64 running on a Raspberry Pi 4B Rev 1.5. The RoboQuest HAT
hardware is running firmware version 5.1. The container system is
Docker version 23.0.5.

The robotics framework is ROS2 Humble running in several Docker
containers. The programming languages are Python 3.9 and
ECMAScript 5 (I think) with Google V8 version 10. The server side
JavaScript is executed by NodeJS Hydrogen (18.17.1) and uses rclnodejs
version 0.22.1.

Communications with the browser use ExpressJS version 4.18.2 and
socket.io version 4.6.1.

### Responsibilities

Python is used for communication with the hardware and the OS.
JavaScript is used for communication with and management of the
browser-based UI. Communication between Python applications
and between Python and JavaScript applications is handled by
ROS2 Humble.

The JavaScript applications access the ROS2 graph via rclnodejs.
They use ExpressJS to serve static files and JavaScript to the
browser. Two-way asynchronous communication with the browser uses
socket.io.

## Future considerations

### [ros2control](https://control.ros.org/master/index.html)

### [Node composition](https://docs.ros.org/en/humble/Concepts/About-Composition.html)

