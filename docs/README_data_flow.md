# RQ Data Flow

How data flows from the robot, to the browser UI, and back to the robot.

## Configuration

Most of the data which flows between the robot and the UI is
configurable using a single configuration file. Configuration
consists basically of specifying a data source and its
destination. Sources of data can be either

1. a published ROS topic
2. a browser UI component

while destinations for data can be either

1. a subscribed ROS topic
2. a called ROS service

The backend server publishes to topics, subscribes from topics,
and provides services. It does not call services. The frontend UI
subscribes from topics, publishes to topics, and calls services.
For data published onto a topic by the backend and used by the
frontend, the topic name and message type must be already defined
in the backend code. This generally limits new topics to ROS
standard message definitions.

In order for a ROS topic to be used by the frontend UI, the
configuration file public/config/configuration.json must specify
the following 5 items:

1. a widget to which the data is associated, with the "type" and "id"
   attributes defined
2. the name of the topic in the widget's "topic" attribute
3. if the frontend subscribes then the widget's "topicDirection"
   attribute is set to "subscribe", otherwise to "publish"
4. the widget's "msgType" attribute set to the full string name of the
   message
5. the widget's "msgAttribute" attribute set to the full name of the
   data item(s) in the message

For a service called by the frontend, the widget configuration will
have:

1. a widget to which the data is associated, with the "type" and "id"
   attributes defined
2. the name of the service in the widget's "service" attribute
3. the widget's "msgType" attribute set to the full string name of the
   service message
4. the widget's "msgAttribute" attribute set to the full name of the
   data item(s) in the service message

## Implementation

The NodeJS application reads the configuration file and extracts
those widgets with a non-empty string for the "topic" attribute.
If the "topicDirection" attribute is "subscribe" then a ROS
subscriber is created, using the topic name and the message type.
The callback function is created at run time too. All of the
topic callback functions immediately call the send_to_client_cb()
method. The topic name is used as the socket event name and the
entire message from the topic is sent as the payload.

The message payload is sent as a JSON string. This costs two
unnecessary conversions of the message payload, from object to
JSON string and then from JSON string back to object. The payload
should instead be transmitted via the socket as an object.

On the browser client side, the same configuration file is read
and the same subset of widgets are extracted. The browser
interprets "topic" as a socket event name and "msgAttribute" as
the attribute of interest from the JSON string payload with the
event.

