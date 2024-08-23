# turtlebot3_manipulation

## Summary

This package is a modified version of the original ROBOTIS [*turtlebot3_manipulation*](https://github.com/ROBOTIS-GIT/turtlebot3_manipulation) package. It is built to accomodate launching bringup and navigation scripts on multiple TurtleBots.

## [Physical Robot] Instructions for Executing Multi-Robot Trajectories

### Step 0: Initial setup

1. __Compatibility check__: These scripts are intended for use with [ROS Noetic Ninjemys](http://wiki.ros.org/noetic "Noetic Documentation") and Ubuntu 20.04.

2. __Communication setup__: Make sure all TurtleBots can communicate with your PC on one network. Additionally, timesync each TurtleBot to your PC (for this, we used [chrony](https://chrony-project.org/ "Chrony Homepage")).

3. __LDS driver__: Since this package uses namespaces to differentiate between TurtleBots, you must hard-code a field for the namespace into the TurtleBot's LDS driver file. If you intend to use the scripts in this package, be sure to first edit each TurtleBot's *ld08_driver.cpp* file according to the suggestions by “dominik-polic” on [this](https://github.com/ROBOTIS-GIT/ld08_driver/issues/1) GitHub issue thread.

### Step 1: Run roscore

On __your PC__, run roscore.

   ```roscore```

### Step 2: Launch Bringup on TurtleBots

On each __TurtleBot's SBC__, launch its bringup launch file with the namespace specified.

   ```ROS_NAMESPACE={NAME_OF_YOUR_NAMESPACE} roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="{NAME_OF_YOUR_NAMESPACE}" set_lidar_frame_id:="{NAME_OF_YOUR_NAMESPACE}/base_scan"```

### Step 3: Launch manipulation Bringup

On __your PC__, launch the manipulation launch file to bring up the manipulation nodes for all of the TurtleBots' arms.

   ```roslaunch turtlebot3_manipulation_bringup multi_turtlebot3_manipulation_bringup.launch```

### Step 4: Launch the navigation launch file

On __your PC__, run this script to launch the *robot_state_publisher* node, laser filtering, AMCL, and RViz.

   ```roslaunch turtlebot3_manipulation_navigation multi_turtlebot_navigation.launch```

### Step 5: Run the action server/client scripts

The final step involves launching the action client/server scripts in the __[mutli_mobile_manipulation_control](https://github.com/JBVAkshaya/multi_mobile_manipulation_control/)__ package. Click the link and follow the instructions in the README to send trajectories to your TurtleBots.

### Notes

By default, the scripts listed in the instructions above assume you are using *two* TurtleBots. The scripts can be easily modified to accomodate different numbers of robots, but for simplicity, below are the scripts you should run if you are testing on *one* or *three* TurtleBots.

__If using one TurtleBot__:

* In __Step 3__, replace `multi_turtlebot3_manipulation_bringup.launch` with `single_ns_turtlebot3_manipulation_bringup.launch`

* In __Step 4__, replace `multi_turtlebot_navigation.launch` with `single_ns_turtlebot_navigation.launch`.

__If using three TurtleBots__:

* In __Step 3__, replace `multi_turtlebot3_manipulation_bringup.launch` with `three_turtlebot3_manipulation_bringup.launch`.

* In __Step 4__, replace `multi_turtlebot_navigation.launch` with `three_turtlebot_navigation.launch`.

## [Simulation] Instructions for Executing Multi-Robot Trajectories

[Coming soon...]



__*Old text (remove?)*__ This repository contains packages for multi mobile manipulation tasks using team of turtlebots with open manipulators. The repository is developed on top of the ROBOTIS repository: https://github.com/ROBOTIS-GIT/turtlebot3_manipulation