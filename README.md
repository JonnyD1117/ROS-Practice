# ROS-Practice

This is my repo on setting up and using ROS. This readme is intended to function as a cheat sheet for ROS since my usage of ROS is inconsistent and I find myself constantly looking back at previous work or tutorials to makeup the ground which I have lost during my periods of non-consistent usage of ROS.

## ROS Version:

* Noetic
* Ubuntu 20.04 LTS
* Windows WSL2

## Installation and Setup:

Navigate to http://wiki.ros.org/noetic/Installation to setup a brand new installation of ROS Noetic.

### Create ROS Workspace (aka: Catkin_ws folder)

```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make

```
