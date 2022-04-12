# Optitrack_MC

# ROS Bag 
A Rosbag or bag is a file format in ROS for storing ROS message data. These bags are often created by
subscribing to one or more ROS topics and storing the received message data in an efficient file structure. 

*All terminals MUST be sourced -> $source /opt/ros/noetic/setup.bash * 

# Creating ROS Bag Directory 

Open a new terminal  
$roscore  

Open a new terminal  
$ mkdir ~/bagfiles 
$ cd ~/bagfiles 

# Recording Data from motion capture system  

Open a new terminal  
$ roslaunch mocap_optitrack mocap.launch 

$rosbag record -a 

$rosbag info (rosbag name).bag 

$rosbag play (rosbag name).bag 

# Graphing Rosbag Data  
PyQtGraph (2D) 
or 
Matlab (3D) 

# PyQtGraph  
Open a new terminal  

$ roscore 

Open a new terminal  

$ cd ~/bagfiles 

$rosbag play (rosbag name). Bag 

Open a new terminal  

$ rqt_bag 

-> insert bag files  

-> left click on bar-> view -> plot 

-> adjust axes 

# MATLAB  

Open a new terminal to convert bag files to csv file 

$ rostopic echo -b (bag name).bag -p /mocap_node/bebop_1/pose>(name for csv file).csv 

Open MATLAB  

-> upload file into MATLAB 

-> type: t=readtable(‘name_of_file.csv’) 

-> type: plot3 (t, 5,6,7)  * establishes x,y,z axis *

