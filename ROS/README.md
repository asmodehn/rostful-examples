Rostful ROS Examples
====================

This directory contains a set of launch files and script that you can use to get an understanding of how to use Rostful.

Prerequisites
-------------

First, install [ROS Kinetic release](http://wiki.ros.org/kinetic/Installation/Ubuntu).



The Python way
--------------

Clone this repository
```
$ git clone https://github.com/asmodehn/rostful-examples
```

Install all ROS dependencies for this package, using ROS packaging system and tools:
```
$ rosdep update
$ rosdep install --from-paths rostful-examples
```

There is currently no launch system for pyros, so you have to each node manually.

```
$ source /opt/ros/kinetic/setup.bash
$ roscore
```
```
$ source /opt/ros/kinetic/setup.bash
$ rosrun turtlesim turtlesim_node
```

This is the advised way to launch rostful, as it works well both from source or install,
integrate with python workflow, and only relies on the bare minimum of ROS.

```
$mkvirtualenv --system-site-packages --python=/usr/bin/python2.7 rostful_test
(rostful_test)$ pip install rostful pyros[ros]
(rostful_test)$ python -m rostful run
```

Troubleshooting:
- make sure you are running python2 (python3 not yet supported all the way - but could be...)
- make sure you are running python and rostful in a terminal not polluted by ROS (your PYTHONPATH should be empty, modifying it is a hack)
- make sure pyros-setup configuration created in your virtualenv uses the ROS distribution installed on your system


The ROS way
--------------


Clone this repository:

```
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws
$ wstool init src https://raw.githubusercontent.com/asmodehn/rostful/kinetic/rosinstall/kinetic.rosinstall
```

Install all dependencies:
```
$ rosdep update
$ rosdep install --from-paths src --ignore-src -y
```

Then, build everything:
```
$ catkin_make
$ source devel/setup.bash
```

This example has a simple ROS launcher

```
roslaunch launch/turtlesim.launch
```

Note: using rostful from source in a ROS workflow  (catkin environment), although possible for porting rostful to ROS, is not recommended.
Use the more flexible Python way instead, leveraging the pyros\[ros\] interface.

Usage
-----

Then use [Postman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en)/Chrome or [HTTPRequester](https://addons.mozilla.org/en-us/firefox/addon/httprequester/)/Firefox or any other REST client extension for your favorite browser to be able to manually send requests to the exposed ROS topics/services
Use your hostname ( localhost on your local machine where you probably run turtlesim )

The port where the webserver listens by default is 8080 for security reasons (ports < 1024 require administrator rights)
Then we append a /ros/ prefix to form the URL from the ROS name. This allows us to leave URL space for other pages we might want to serve.

So for turtlesim you should be able to get the current position at this URL:
GET http://localhost:8080/ros/turtle1/pose

There is also a simple Debug UI to make things easy, so you can use your browser to access it at http://localhost:8080/

This is still work in progress, so more details will be documented here when this gets finalized.

