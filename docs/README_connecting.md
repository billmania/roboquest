# Connecting to the robot

Out of the box, there are two ways to connect to the robot. They
both require an ssh client.

The first way is using the Access Point (AP) provided by the robot.
The SSID for the AP has the pattern "roboAP_hhhh" where hhhh is
replaced by the last four hex digits of the robot's Ethernet
interface's MAC address. An example SSID is "roboAP_23eb".

The IP address for the robot, when using the AP, is 10.42.0.1/24.

The second way requires connecting the robot's wired Ethernet
interface to a local network. This method may require
administrative access to the local network's DHCP server, in
order to determine the IP address which was assigned to the
robot. In cases where the RoboQuest application software is
installed and running, it's possible to find the robot's IP
address on screen 2 of the robot's hardware User Interface.

The second way is preferred due to better stability and
throughput.

There are two usernames defined: roboquest and ubuntu. roboquest
is preferred, ubuntu is legacy.

Once ssh access is established with the robot, it's possible to
connect the robot to a new WiFi network using the nmcli and nmtui
utilities.
