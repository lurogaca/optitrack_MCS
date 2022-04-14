## Table of contents
* [Calibrating Optitrack](#calibrating-optitrack)
* [Reading Data](#reading-data)
* [Rosbag](#rosbag)
* [Graphing](#graphing)

*All terminals MUST be sourced -> $source /opt/ros/noetic/setup.bash * 
## Calibrating Optitrack
1.Start System  

2.Launch Software Motive  

3.Wanding – Calibrates Cameras with respect to the room 

-> Under Camera Calibration click on ‘Start Wanding’ 

-> Thoroughly wave the wanding device all around the room in all x,y, and z positions where your drone/object is expected to fly 

-> Continue to wave the wand until the monitor shows that it is very sufficient  

-> Click ‘calculate’ 

-> Click ‘Apply’ 

4.Ground plane – Calibrates Cameras with respect to the ground  

-> Place ground calibration device on the desired origin of the room  

-> Select ‘Ground Plane’ icon 

-> Click on ‘Ground Plane’ 

-> Click Export 

5.Create Objects 

-> Place object on floor on the origin previously defined facing the desired orientation 

-> In the perspective view window, select the object using the mouse 

-> Click ‘Builder plane’ 

-> Name the object  

-> Click ‘create’ 

* In the properties window, use the given channel in streaming ID when connecting to the Optitrack system to read data from 
the created object 
	
## Reading Data

Install Mocap_Optitrack Package:

Open a new terminal  

```
$ roscore
```
Open a new terminal 
```
$ sudo apt-get install ros-noetic-mocap-optitrack 
```
Edit mocap.yaml file: 
```
$cd /opt/ros/noetic 

$cd share  

$cd mocap_optitrack 

$cd config  

$ sudo gedit mocap.yaml 
```
Edit the following: 

- delete robot_2 paragraph  

- multicast interface: 239.255.42.99 

- command port:1510 

- data port: 1511 

- change “robot_1” -> “object_name” * name used when calibrating*  

- rigid bodies: “7” * streaming ID*  



Connect to Motion Capture System:


Open a new terminal 
```
$ roslaunch mocap_optitrack mocap.launch 
```
Open a new terminal 
```
$ rostopic list 

$ rostopic echo /mocap_node/bebop_1/pose 
```

## Rosbag
A Rosbag or bag is a file format in ROS for storing ROS message data. These bags are often created by
subscribing to one or more ROS topics and storing the received message data in an efficient file structure. 

Create Rosbag Directory: 

Open a new terminal 

```
$ roscore
```
Open a new terminal 

```
$ mkdir ~/bagfiles 
$ cd ~/bagfiles 
```
Record Data from motion capture system:  

Open a new terminal 
```
$ roslaunch mocap_optitrack mocap.launch 

$ rosbag record -a 

$ rosbag info (rosbag name).bag 

$ rosbag play (rosbag name).bag 
```

## Graphing

You can graph your using PyQtGraph (2D) or Matlab (3D) 


PyQtGraph: 

Open a new terminal  
```
$ roscore
```
Open a new terminal  
```
$ cd ~/bagfiles 
$ $rosbag play (rosbag name).bag
```
Open a new terminal  
```
$ rqt_bag
```

 -> insert bag files  

-> left click on bar
-> view 
-> plot 
-> adjust axes 

![square](https://user-images.githubusercontent.com/103215218/163457093-c041b722-3332-4cdb-a59d-a45d8d035109.png)



MATLAB:

Open a new terminal to convert bag files to csv file 
```
$ rostopic echo -b (bag name).bag -p /mocap_node/bebop_1/pose>(name for csv file).csv 
```
Open MatLab:

-> upload file into MATLAB 

type:
```
t=readtable(‘name_of_file.csv’) 
```
type :
```
plot3 (t, 5,6,7)) 
```
* establishes x,y,z axis 

![Screenshot from 2022-04-14 12-51-51](https://user-images.githubusercontent.com/103215218/163457482-dc991859-a14b-4ac1-8628-44d4ff070eb7.png)

