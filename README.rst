Getting Started 
=============== 

The radler framework takes its inspiration from the Robot
Operating System (ROS). In the radler framework, the sensors,
controllers, and actuators are constructed from functional
units called nodes. Each node executes independently with a
period determined by a local clock and scheduling constraints.
The radler supports a publish/subscribe architecture where nodes
communicate by publishing on certain topics and subscribing
to other topics.

To install  
----------

First time after cloning::

	git submodule update --init --recursive

To get radler working on a clean version of Ubuntu 14.04::

	sudo apt-get install cmake python3-pip ipython
	sudo pip3 install tarjan

To install ROS:: 

	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
	wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -
	sudo apt-get update
	sudo apt-get install ros-indigo-ros-base
	(echo ; echo "# Setup for ROS" ; echo "source /opt/ros/indigo/setup.bash" ) >> ~/.bashrc
	source ~/.bashrc

To use **Secure\_ROS**, download .deb file from http://radler.csl.sri.com/deb/secure-ros-indigo-ros-comm_1.11.20_amd64.deb. You can also create .deb file by following instructions from https://github.com/SRI-CSL/secure_ros. 
To enable **Secure\_ROS**:    

::

    source /opt/secure_ros/indigo/setup.bash
    export ROS_IP=<IP_ADDR> 

You can switch back to ROS: 

:: 

    source /opt/ros/indigo/setup.bash 


To compile and run  
----------------------------

Compile
^^^^^^^^
Radler generates files from the RADL file into a usual ROS catkin structure, then a call to `catkin_make` will generate the executables as usual.
(e.g. for `examples/pubsub/pubsub.radl`)::
	mkdir -p /tmp/catkin_ws/src
	./radler.sh --ws_dir /tmp/catkin_ws/src compile examples/pubsub/single_machine/pubsub.radl --plant plant --ROS
	cd /tmp/catkin_ws
	catkin_make

Run
^^^^

Since `pubsub` defines a plant, radler has generated a launch file to run the requested nodes.
Simplest way of running it is to source the catkin workspace we just compiled and use `roslaunch`::

    source devel/setup.bash
    roslaunch pubsub pubsud.plant.host_computer.launch

You should see the output of the two nodes explaining that they are communicating. For more details see `pubsub` example documentation. 

You can stop everything by typing Ctrl-C.
