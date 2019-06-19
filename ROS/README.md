Rostful ROS Examples
====================

This directory contains a set of launch files and scripts that you can use to get an understanding of how to use Rostful with ROS.

You will notice that, in the python spirit, there is no compilation/build step required.
Just install your dependencies, and launch the code.

Prerequisites
-------------

We assume here that Ubuntu is the OS used.

We assume that [ROS Melodic release is installed](http://wiki.ros.org/melodic/Installation/Ubuntu).

We assume that running dynamic python scripts (on your system, in a virtualenv, with ROS or otherwise) holds no secret for you.


System (ROS) Setup
------------------

Clone this repository
```
$ git clone https://github.com/asmodehn/rostful-examples
```

Install all ROS dependencies for this package, using ROS packaging system and tools, from a separate terminal to not affect the usual python runtime environment:
```
$ source /opt/ros/kinetic/setup.bash
$ rosdep update
$ rosdep install --from-paths rostful-examples
```

There is currently no launch system for pyros, so you have to each node manually, in separate terminals to not affect the usual python runtime environment.

```
$ source /opt/ros/kinetic/setup.bash
$ roscore
```
```
$ source /opt/ros/kinetic/setup.bash
$ rosrun turtlesim turtlesim_node
```

Python launch
-------------

This is the advised way to launch rostful, as it naturally follows python way of doing things, and rely only on the bare minimum of ROS.

```
$mkvirtualenv --system-site-packages --python=/usr/bin/python2.7 rostful_test
(rostful_test)$ pip install rostful pyros[ros]
(rostful_test)$ python -m rostful run --server flask
```

ROS launcher
------------

This is a special case, that might be useful to integrate rostful with your other ROS launchers.

*TODO* find a way to run a specific python interpreter from a specific venv (might be worth checking pipenv and poetry for that)...


Troubleshooting
---------------

- make sure you are running python2 (python3 not yet supported all the way down the stack - but could be, with a bit of help)
- make sure you are running python and rostful in a terminal not polluted by ROS (your PYTHONPATH should be empty, modifying it is a hack)
- make sure pyros-setup configuration created in your virtualenv uses the ROS distribution installed on your system (known issue).
- make sure rostful configuration created in your virtualenv actually exposes the ROS services and topics desired. The configuration by default is secure and does not expose anything to the outside world.


Web Usage
---------

Then use [Postman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en)/Chrome or [HTTPRequester](https://addons.mozilla.org/en-us/firefox/addon/httprequester/)/Firefox or any other REST client extension for your favorite browser to be able to manually send requests to the exposed ROS topics/services
Use your hostname ( localhost on your local machine where you probably run turtlesim )

The port where the webserver listens by default is 8080 for security reasons (ports < 1024 require administrator rights)
Then we append a /ros/ prefix to form the URL from the ROS name. This allows us to leave URL space for other pages we might want to serve.

So for turtlesim you should be able to get the current position at this URL:
GET http://localhost:8080/ros/turtle1/pose

There is also a simple Debug UI to make things easy, so you can use your browser to access it at http://localhost:8080/

This is still work in progress, so more details will be documented here when this gets finalized.

