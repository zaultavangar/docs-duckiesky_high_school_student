# Intro to ROS {#sac2-ros-intro status=ready}


## Motivation

When writing software for a robot, it is easier to break down the software into smaller, more manageable chunks than to write one big program that does everything. While we could have a really long Python program that interfaced with each sensor, used the sensor data to estimate the state of the drone such as it's height an how fast it's moving, and then use this information to change the speeds of the motors, this has several disadvantages. First, if there is a bug in the code (a mistake in the software), it would be very hard to find in a large file where all of the code is together. Second, if someone wanted to improve just one part of the code, such as a better estimate of the IR sensor, they would need to read through a bunch of code that isn't relevant to make their change; additionally, it would be hard to undo those changes if they didn't work well. Instead, software engineers prefer to write _modular_ code, where each program only performs one small job that contributes to a larger job. For example, one program can handle talking to the IR sensor, another program can interface with the camera, another can combine the data, and another can use the combined data to control the motors. Using this software design, it is easy to design and test smaller pieces of code before they go into the bigger picture. If the IR program isn't working right, it won't stop the camera from working, and it will be easy to find the problem.

When we break down the software into smaller programs, we then face the problem of making the programs talk to each other. The data collected in one program might be needed by another program. Let's consider an example of this situation on the drone.

### Example

In the last lesson, you wrote a Python program that could read the ADC, and convert the value to a distance measurement. These steps were essential to obtain the height of the drone in meters. The problem we face now is sharing that value with other programs running on the drone. When the drone is flying, we want the _controller_ to know how high the drone is, so that it can speed up or slow down the motors accordingly. We will go into details on controllers in a later section. For now, we will set up a simpler problem to solve that will demonstrate the process of using a sensor to control an actuator.

**Goal:** The goal is to adjust the brightness of the LED on your drone based on the distance measured by the IR sensor. If the distance is small, the LED should be bright. As the distance measurement increases, the LED should dim. This will simulate speeding up and slowing down the motors based on how high the drone is. The information in this lesson will provide the background needed to accomplish this goal in the following two lessons.

## Software Architecture on the DuckieDrone

Take a look at [this diagram](https://docs.duckietown.org/daffy/opmanual_sky/out/software_architecture_intro.html) that illustrates the software that runs on the drone. Refer back to this diagram as you read through the following points.

### Hardware

Each rectangle with sharp corners in the diagram represents a piece of physical hardware. The IR sensor and the camera are two sensors on the drone.

### Software

Each rectangle with rounded corners represents an individual Python program. Notice that there are specific programs that read the data from each sensor. Inside of that program, the data is read, converted into a useful measurement, and then shared with other programs. If student A's IR sensor code worked better than student B's, then student A could share just their IR code with student B, and student B would be able to use just this code with the rest of the code being their own. This is one advantage of modular software design: small parts of code can be interchanged easily.

### Middleware

In order to share data between programs, such as the IR sensor reading, we use _middleware_. Middleware runs "between" the hardware and software on the drone. In the diagram, the middleware is represented by the arrows that connect the software.

**ROS**

The middleware used on the drone is called the Robot Operating System, or ROS (pronounced like "moss" but with an "r"). This is industry standard software and is used in many profession robotics companies. You can watch a few cool examples of robots that use ROS [here](https://www.youtube.com/watch?v=Z70_3wMFO24).

**ROS on the drone**

For the purposes of the drone, ROS is a communication tool that allows one Python program to talk to another. For example, ROS will allow the `ir.py` program to share the distance measurement from the IR sensor with another program that can adjust how fast the motors are spinning to hold the drone at a specific height.

## ROS jargon

The communication system in ROS comes with its own vocabulary. The following terms are essential for understanding ROS.

### Node

A ROS node is simply a program that contains publishers or subscribers. On the drone, a node is just one of the Python programs that is used to make the drone fly.

For more info: [ROS wiki link](http://wiki.ros.org/Nodes)

### Publishers

A publisher is a ROS entity that sends messages to a topic. In python, a publisher is just an object with a "publish()" method that sends the message.

For more info: [ROS wiki link](http://wiki.ros.org/rospy/Overview/Publishers%20and%20Subscribers)

### Messages

A message is a structured format for data. Messages standardize how the publisher is supposed to format the data, so that the receiver knows how to read it. For example, there is a Boolean message type where the data can only be `True` or `False`. There is also a String message type, where the data can be any text such as `this is my message!`. We can also make custom message types that combine two or more existing message types. For example, we could create a message type that contains two Booleans and one String.

```
bool
bool
string
```

We would want to label the Booleans and the String so that the sender and receiver would know which data was which. If the first Boolean determined whether I wanted ice cream, and the second Boolean determined whether I wanted to pay for it, I would not want those mixed up! Here is what a custom message type could look like:

```
bool      do_i_want_icecream
bool      do_i_want_to_pay_for_it
string    flavor
```

The first column shows the type of the data, also known as the **fieldtype**. The second column shows the label for the data, also known as the **fieldname**. Together, the fieldtype and fieldname make one **field** in a ROS message.

The way that we would use this message in Python is to create a blank message, and then to edit the fields. For example:

```
my_icecream_order = OrderMessage()  # create a blank message

OrderMessage.do_i_want_icecream = True
OrderMessage.do_i_want_to_pay_for_it = False
OrderMessage.flavor = "Strawberry"
```

Now I can publish my_icecream_order and my ice cream robot will go and buy me strawberry ice cream!

For more info: [ROS wiki link](http://wiki.ros.org/msg)

### Topic

A ROS topic is a named bus that messages get published to and subscribed to. In Python, a ROS topic is just a String that identifies where a publisher should send messages, and where a subscriber should look to receive those messages. Only one message type can be sent along a topic, and this is set when the topic is created by a publisher. For example, we might want to create a topic called `order` that has the message type `OrderMessage`. We can create a publisher that publishes our ice cream orders to the `order` topic.

For more info: [ROS wiki link](http://wiki.ros.org/Topics)

### Subscriber

A ROS subscriber "subscribes" to a topic and listens for messages. When the subscriber is created, it is told what topic to listen to. As soon as a subscriber receives a message, it passes along the message to a **callback** function.

For more info: [ROS wiki link](http://wiki.ros.org/rospy/Overview/Publishers%20and%20Subscribers)

### Callback

A callback is a function that takes as input a ROS message, and then performs some action based on that message. In some cases, the action might just be storing the message data. In other cases, the action might involve the physical world. In the ice cream example, the callback function would hopefully make our ice cream robot go and buy us ice cream. In the case of the drone, the flight controller node is subscribed to roll, pitch, yaw, and throttle commands on the `/pidrone/fly_commands` topic. When new commands are published to this topic, the callback in the flight controller subscriber sends these commands to change the speeds of the drone motors.

### Master

In order for ROS nodes to communicate with messages over topics, each node must register with the ROS Master. The ROS master facilitates communication between nodes by keeping track of all of the nodes, topics, publishers, and subscribers. This information is used to help nodes find each other so that they can communicate.

For more info: [ROS wiki link](http://wiki.ros.org/Master)

### Summary

ROS allows a _node_ to _publish_ a _message_ to a _topic_ and then another node can _subscribe_ to the topic to receive messages. Once a message is received, the subscriber passes the message to a _callback_ function that does something with the data. This communication is facilitated by a _ROS Master_, which allows nodes to find each other to communicate.

## ROS commands

There are a number of useful ROS commands that you can use in the terminal.

For details on all of the ROS commands: [ROS wiki](http://wiki.ros.org/ROS/CommandLineTools)

### roscd

`roscd` is the ROS version of `cd`; it lets you navigate directly to ROS packages. For example, if you are in the home directory on the drone, instead of typing: `cd ~/ws/src/pidrone_pkg`, you can just type `roscd pidrone_pkg`.

### roscore

`roscore` is the command used to start a ROS master. No arguments are needed to run this command

### rostopic list

`rostopic list` will list all of the ROS topics that are currently being published and subscribed to

### rostopic info

`rostopic info (topic_name)` will list the publishers, subscribers, and message type of whatever topic you replace `(topic_name)` with  

### rosbag
rosbag allows you to record all of the messages sent to topics. you can specify just one topic to record using `rosbag record (topic_name)`, or you can record all of the topics using `rosbag record -a`. Recording data is useful for testing and debugging. You can also use `rosbag play (file.bag)` to play back the recorded data.

For more info: [ROS wiki](http://wiki.ros.org/rosbag/Commandline)

## Environment Variables

Environment variables modify key attributes of a program. For our applications in ROS, the most important environment variable is `ROS_MASTER_URI`. To change an environment variable, you can either type `export (VARIABLE) = (value)` with the correct variable and values into the terminal. These changes will only be temporary and you'll need to export the values every time. Alternatively, you can create a shell script to export the values for you, as we have done in the [pidrone_pkg](https://github.com/h2r/pidrone_pkg). Take a look at the `setup_for_managed_mode.sh` and `setup_for_master_mode.sh` scripts.

### ROS MASTER URI

The `ROS_MASTER_URI` environment variable sets the IP address and port of the ROS master. All of the ROS nodes will look to this address to register themselves. If there are two computers both connected on the same internet network and both running ROS, one computer can start up a ROS Master using `roscore`, and the other computer can set it's `ROS_MASTER_URI` to be the same as the first computer's. Then, the ROS nodes on the two separate computers can talk to each other! This is a very useful feature because it allows the computation load to be distributed across devices. For example, some of the programs that are run on the drone can instead be run offboard on another computer running ROS. This is necessary for some of the features on the drone. However, nearly all of the DuckieDrone's programs can be run onboard.

## Catkin workspace

There is one more essential ROS element that is worth mentioning if you are interested in creating your own workspace. In programming, a workspace is used to keep track of all of the programming files, dependencies, and executable code. For ROS, the workspace setup is called catkin. The main thing to note is that ROS packages (a set of programs that run together), go in the `src` directory. This is why the path to the `pidrone_pkg` is `~/ws/src/pidrone_pkg`. For instructions on creating your own workspace, refer to the [ROS wiki](http://wiki.ros.org/catkin/Tutorials/create_a_workspace).
