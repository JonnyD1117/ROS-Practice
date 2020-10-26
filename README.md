# ROS-Practice

This is my repo on setting up and using ROS. This readme is intended to function as a cheat sheet for ROS since my usage of ROS is inconsistent and I find myself constantly looking back at previous work or tutorials to makeup the ground which I have lost during my periods of non-consistent usage of ROS.

## ROS Version:

* Noetic
* Ubuntu 20.04 LTS
* Windows WSL2

## Installation and Setup:

Navigate to http://wiki.ros.org/noetic/Installation to setup a brand new installation of ROS Noetic.

### Create ROS Workspace (Catkin_ws folder)
To create a new ROS workspace folder run the following code in the directory or choice. This will create the catkin_ws and src folders which will store the rest of the ROS package files.

```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
```

Once these folders are created source the devel directory as follows...

```
$ source devel/setup.bash
```

This will setup the bash file needed to run ROS correctly. Running the following command will ensure that your ROS environment variables are set correctly.
 ```
 $ echo $ROS_PACKAGE_PATH
 /home/youruser/catkin_ws/src:/opt/ros/kinetic/share
 ```

 ROS has file system commands which are intended to make the navigating the ROS filesystem more manageable. The two most useful commands are 'rospack find...' and 'roscd', used as shown below.

 ```
$ rospack find [package_name]
 ```
 &
 ```
$ roscd [locationname[/subdir]]
 ```

## Creating a ROS Package

http://wiki.ros.org/ROS/Tutorials/CreatingPackage

For a package to be compatible with CATKIN package, it must meet the following requirements.

* package.xml file
* CMakeLists.txt
* Each package must reside in its OWN folder


 1. **package.xml**: The 'package.xml' file  is a XML file which complies with catkin, and includes information about the package such as ...
    * package name
    * version numbers
    * authors
    * maintainers
    * Package specific build dependencies

    For more info on package.xml see the ROS wiki at: http://wiki.ros.org/catkin/package.xml

2. **CMakeLists.txt**: The XMakeLists.txt file is the input to the Cmake system for building the software packages. The CMakeLists file is a 'vanilla' Cmake file which includes a few addition constraints.

For more info on CMakeLists.txt file see the ROS wiki at: http://wiki.ros.org/catkin/CMakeLists.txt

3. **Individual Folder per Package**: This requirements dictates that each package must have its own folder. This requirement imposes the following restrictions.

   * No nested packages
   * Multiple packages cannot share a single directory

### Creating catkin Package:

To create a package, change into the "catkin_ws" directory as follows.

```
# You should have created this in the Creating a Workspace Tutorial
$ cd ~/catkin_ws/src
```

Then use the command *catkin_create_pkg*, as documented below.

http://wiki.ros.org/catkin/commands/catkin_create_pkg

```
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

An example of using this command is shown below.

```
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```

Once the package has been created, the user must "catkin_make" the workspace again to generate the appropriate setup files. Following this operation the setup environment needs to be sourced.

**Update Workspace**
```
$ cd ~/catkin_ws
$ catkin_make
```

**Source New 'setup.bash'**
```
$ . ~/catkin_ws/devel/setup.bash
```

Should it be required, the dependencies of the newly created package can be view by running...
```
$ rospack depends1 beginner_tutorials
    roscpp
    rospy
    std_msgs
```


### Customizing 'package.xml':
Once the package has been generated and sourced, the package.xml file should match the package specifics to ensure the package runs correctly.

1. **Description Tag**: denotes the name of the ROS package being created

```
<description>The beginner_tutorials package</description>
```

2. **Maintainer Tags**: denotes the maintainers of the package and their contact information

```
<maintainer email="user@todo.todo">user</maintainer>
```
3. **License Tags**: denotes the type of license applied to the package for legal usage

```
<license>BSD</license>
```
4. **Dependencies Tags**: denotes the "build system" being used (catkin) as well as the ROS packages which the new project references. The layout for this tag is shown below.  

```
<buildtool_depend>catkin</buildtool_depend>
  <build_depend>roscpp</build_depend>
  <build_depend>rospy</build_depend>
  <build_depend>std_msgs</build_depend>
```

Once every tag has been correctly set the 'package.xml' should look as follows...

```
1 <?xml version="1.0"?>
2 <package format="2">
3   <name>beginner_tutorials</name>
4   <version>0.1.0</version>
5   <description>The beginner_tutorials package</description>
6
7   <maintainer email="you@yourdomain.tld">Your Name</maintainer>
8   <license>BSD</license>
9   <url type="website">http://wiki.ros.org/beginner_tutorials</url>
10   <author email="you@yourdomain.tld">Jane Doe</author>
11
12   <buildtool_depend>catkin</buildtool_depend>
13
14   <build_depend>roscpp</build_depend>
15   <build_depend>rospy</build_depend>
16   <build_depend>std_msgs</build_depend>
17
18   <exec_depend>roscpp</exec_depend>
19   <exec_depend>rospy</exec_depend>
20   <exec_depend>std_msgs</exec_depend>
21
22 </package>
```

### Building ROS Package:

With all of the new package specific dependencies installed, we can build the new package. Before we can build we must setup the environment by sourcing the set.bash files, shown below.

```
# source /opt/ros/%YOUR_ROS_DISTRO%/setup.bash
$ source /opt/ros/kinetic/setup.bash             # For Kinetic for instance
```

Once this has been done the system can be build using "catkin_make" tool from within the "workspace" directory.

```
$ catkin_make
```


## Understanding ROS Nodes:
