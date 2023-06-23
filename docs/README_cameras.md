# RoboQuest cameras

Managing cameras included in the RoboQuest system is suffciently
complex to warrant its own document.

## Software components and data flow

## Configuration

### Static configuration

To list the parameters which can be changed:
```
ros2 service call \
    /rq_camera_node/list_parameters rcl_interfaces/srv/ListParameters
```
The popular parameters are:

* brightness
* contrast
* saturation
* framerate

The parameters could be changed using either the rqt GUI or the
ros2 CLI, but the param CLI method hangs and the service CLI
method complains about undefined parameters. This may be caused
by the camera_node not defining any dynamic parameters.

https://answers.ros.org/question/355508/ros2-using-dynamic-parameters-in-python/


```
ros2 param get /rq_camera_node brightness
ros2 param set /rq_camera_node brightness 150

ros2 service call \
    /rq_camera_node/set_parameters rcl_interfaces/srv/SetParameters \
    "parameters: [ {name: \'rq_camera_node/brightness\', value: {type: 4, double_value: 150}}]"

```
