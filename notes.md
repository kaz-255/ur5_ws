#ROS workspace environemnt

Notes by **KA**
info based on Youtube video
` Programming for Robotics (ROS) Course 1 
https://www.youtube.com/watch?v=0BxVPCInS3M`



##Set up

    source /opt/ros/indigo/setup/bash


Load workspace
use `cd ~/{filePath}/catkin` to load workspace
   
    source devel/setup.bash

    echo $ROS_PACKAGE_PATH

##ROS MASTER
a ROS Master manages communcation between nodes

Start Master with 
    
    roscore

##Nodes
Node registers at start-up with the master
Single-purpose executable program
Compile individuall

Run node with
    
    rosrun package_name node_name

example:
    
    rosrun example example.py

View active nodes with 
```bash
rosnode list
```

Info of a node 
```bash 
rosnode info node_name
```

More commands
```bash
rosnode is a command-line tool for printing information about ROS Nodes.

Commands:
	rosnode ping	test connectivity to node
	rosnode list	list active nodes
	rosnode info	print information about node
	rosnode machine	list nodes running on a particular machine or list machines
	rosnode kill	kill a running node
	rosnode cleanup	purge registration information of unreachable nodes
```

##Topics
Ros Wiki
wiki.ros.org/ROS/Tutorials/UnderstandingTopics

**Node** communicates over **Topics**
Think of topics as names for stream of messages
Nodes can ***publish*** topics that can be ***subscribed*** by other nodes
List active topics
`rostopic list`'
Subscribe topics 
`rostopic echo /topic`
Show info
`rostopic info /topic`

More Commands 
```bash
rostopic is a command-line tool for printing information about ROS Topics.

Commands:
	rostopic bw	    display bandwidth used by topic
	rostopic delay	display delay of topic from timestamp in header
	rostopic echo	print messages to screen
	rostopic find	find topics by type
	rostopic hz	        display publishing rate of topic    
	rostopic info	print information about active topic
	rostopic list	list active topics
	rostopic pub	publish data to topic
	rostopic type	print topic or field type
```

##  Messages
`*msg` files
Data structure type of a topic 

See type of a topic
`rostopic type /topic`

Publish message to a topic
`rostopic pub /topic type args`

### Example of a message
Pose stamped messages
Geometry_msgs/Point.msg
```bash
float64 x
float64 y
float64 z
```
Essentitally a description of a point in cartesian space.
###example
sensor_msgs/image.msg

    std_msgs/Header header
    uint32 seq 
    time stamp
    string frame_id
    uint32 height
    unit32 width
    string encoding
    uint8
    ...

A message may be composed of other messages 


### Constraints
Each constant definition is like a field description, except that it also assigns a value. This value assignment is indicated by use of an equal '=' sign, e.g. 

#  Catkin build system 
What's **catkin**
Catkin is the ROS build system to generate **executables, libraries and interfaces**

## tools

    catkin_make
Build package with
    
    catkin build package_name

***Note*** 
Every new package requires refreshing the environment
    
    source devel/setup.bash

**Warning**
***DO NOT TOUCH content of `/build` or `devel`, only work in `src`*** 


    catkin clean 


#   ROS Launch file
Wiki
http://wiki.ros.org/roslaunch
##  What's Launch
Launch is a tool to **launch multiple nodes.** 
This file speciies 
- which node to execute
- **parameters** of the nodes 
- what **other** launch files to include

The launch files are XML files in extension `.launch`

##  Example
Start a laucnch file with
   
    roslaunch filename.launch

Within a package, use the following to laucnh a file 
   
    roslaunch package_name filename.launch

##  ROS XML format
[Link to ROS Wiki page on Ros XML](http://wiki.ros.org/roslaunch/XML)
Example of launch file

    <launch>
        <node pkg="turtlesim" type="turtlesim_node" name="turtle1"/>
        <node pkg="turtlesim" type="turtle_teleop_key" name="key_ctrl"/>
    </launch>

### Argument example
The <arg> tag allows you to create more re-usable and configurable launch files by specifying values that are passed via the command-line, passing in via an <include>, or declared for higher-level files. Args are not global. An arg declaration is specific to a single launch file, much like a local parameter in a method. You must explicitly pass arg values to an included file, much like you would in a method call. 

    <include file="included.launch">
    <!-- all vars that included.launch requires must be set -->
    <arg name="hoge" value="fuga" />
    </include>

___
#Gazebo Simulator
Physics, collusion, noise with ROS interface

Run Gazebo with

    rosrun gazebo_ros gazebo


___

#   Ros Packages

##  Definition
A ros software (rospackage) contains the source code, launch files configuration message defintiion data and documenation

Dependies are other packages  
## creating new packages
To create new package, use

    catkin create_package package_name {dependencies}

file structure
    
    package name 
    |-  config
    |-  include/package name
    |-  launch
    |-  src
    |-  test
    CMAKELists.txt
    package.xml



#  Pubulisher and Subscribers
## What are these
Publisher is a node that ***publishes*** topics
Subscriber ***listens*** to topics using the method `subsribe()` of the node handle.

a ROS Publisher…

- is a ROS node (program).
- creates a particular type of ROS message. In this case, it’s std_msgs/String, as can be seen on lines 4,7-8 of the code.
- sends (publishes) a message over a channel called “topic”, as can be seen on lines 10 then 12 of the code.




#   ROS Parameter Server