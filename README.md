## Installation 
Make your life easier: http://wiki.ros.org/turtlebot/Tutorials/indigo/Turtlebot%20Installation.
Under the section 1.1.1 on the page linked above, find the ISO with ROS and Turtlebot software installed. 

* install Ubuntu on Mac

	https://youtu.be/IQIaDO9nR6Y
	
* install Ubuntu on a Windows 10 machine

	https://youtu.be/nBD4KqH5CT8 (recommand)
	
	https://youtu.be/bqSlK376gwo

It is highly recommand to find an old and NON-FANCY laptop to run linux on. Something like a fancy gaming laptop or Surface often have custimized motherboards which make installing linux and dual-booting a little harder, but if that's the only option, it's still doable. 

Consult your TA, professor and online community often, don't get stuck. The process can be irritating. 

**WARNING: The Macbook pro 2016 or newer (the one with touchbar) seems not supporting ubuntu for now.**



## Talk keynote 1: ROS Basics — Topics, Service, Actions
A ROS system is made up of many different programs running simultaneously. Each program is called _*node*_.  The nodes are communicating with one another with a peer-to-peer manner by passing _*messages*_.  That means messages are not passing through the *roscore* , each node just uses roscore to find each other.

* **Messages** are nothing fancy, but data structures.  Here is an example of a message:
![alt text](https://lh3.googleusercontent.com/c8uLbDPLurDIuYd7_xHsp5d1RguPqD1mvvXI5lmwAGgfAAjWFV3-O58LvQjY3buM6R38LJaIFTEGSoRnhB8zsr0cJAlZrMgL-ms93LOPBROTi-YDRX64MuV56VFpBtMqCVfFsEHOicpfIFn6BUwKSo0BAJUdox0Q32t3_DlxDuYJNXpAebdB8cRvpITYfQocP0RYTJFzGmePFOFd4jMTdG7p6GoEJCfn07QF1B8WslS7U01oLH6zY8Rf0PiT025lGjKZPNEkP7QFSR9R6-bGRTNCZPcmFIh6If2_LEE11PqtqR6eJvLohgFDFoYMTlU3Sx90OlKrvh2iLbQl6tyDcC4FZIVW1WmUB3hr-8_2D9f5xRbI7NsCCbUWYQgoV3QHPrybPxk9Ef0hBnqd5IypuXC2-5igMvR15P00QUkV4SElu_kOSAO5Wtv4QVzP2-pF-5DFgEb3C23e8XRub3XHizqV2BFb4Ug5dYtglyeDIl8eJV0v4BX3ykcSYprCqOh9HUuFbBElTBu17vX6vwYDJSWLklenUriIQoft84DYYi9u5V7D6nOvFJ8loRX8TQ3UTQ-iDNJmtr-gPXHYxqsIY5k8PxCBN54Gyj_65bH_s20aXimrNfNqeA=w1304-h1002-no "Example of Point message")
⋅⋅⋅This message is called *Point*. It represents a point in a coordinate system. It has three float values x, y, z. A message is like a *structs* or *class without methods*. You will use a lot of this in the future. Anytime you want to do anything in ROS system, you have to have some kind of message to talk to the system (of course, you can create your own message which will be introduced later).  

* **Topics** are names for streams of some messages with defined types. For example, the [lidar](https://en.wikipedia.org/wiki/Lidar) sensor(the one is spinning on top of the turtlebot) is constantly posting message [LaserScan](http://docs.ros.org/api/sensor_msgs/html/msg/LaserScan.html) on the topic named scan. In ROS, there are countless topics, *nodes* are posting messages on *topics* each time(with various rate). One classic way you want to manipulate the ros system is through **_taking the messages from topics, making use of them and posting some messages on some topics back_**. Lots of nodes are basically following this model. 
⋅⋅⋅A natural question to ask is: How do I know what topics are there? It's nice and easy, just use command `rostopic list`.
This will list all the topics that are currently existing in the system. What I mean by that is there are countless topic, but each time in your system there are only few nodes posting messages on some topics. I just need to care about ones that are currently existing.
![alt text](https://lh3.googleusercontent.com/oZTWcyFukzc7X9a_hPp6O59zJXRkVnHoVroAehjlJo9ViYXsV7dpBbW5f9iz3-TxvXO2oCEM33tRQUozr0wAFgqycjibeE4-5siQJOILbMnzJm9oK8T0p1jglg37gFS7p8toVbQ4D0HSYuVbuSCb1doy1wtCw1276alStMCG4zYysmNWT5MwB7nv0QaqNEvwnxhrqHnN8kLIsaZ8FhqyXJB9QgcsrNtQ0iCbpFVt_9M4fBEpgG4tOIpYDol00AhF1hFQqEDgmpE7Ju5T-CD-oEISju6X_1hrIyS2M-BTEP-cos6fZKbUhBCKmUGP13ePZP-DydczRsFUu0ZeuXEH-AJKMRoxy8_yeWvhGMqbdRB9fV-iE_o1PuNib8Vv2HQmgODof3zHPPLihr47PpMxOm0Kjdk6OVKegIraD5r1GT52DW7UXuPnjIJ-tOKRQU_iUs06bhgBLFPhCYKLEcXUWx5p4nKv9l3Seywutbqy52d4qJpO8XIxXus68J9VjMzcZmV7KFCle60X3UBdXdalPopxr1LOftMxpTvFjeK6RJ7As1tcYj3FvE8SqWl3hoauKrvoN_u6MUJtU_hYzU4F6WkEnkXnITvHKqqqMge4PEBqv9JaJoqAjGCUs97ID1jOI40PM5P4eIccnLenviEobIRhtVFuEdo2iXeNaIdurQpp5mw=w2082-h1364-no "When you make rostopic list command in terminal")










## Setup your workspace and packages

* `echo "source /opt/ros/(YOUR VERSION OF ROS, e.g. indigo)/setup.bash" >> ~/.bashrc` and `echo "source ~/(YOUR WORK SPACE)/devel/setup.bash" >> ~/.bashrc` in your terminal, otherwise you have to source your setup file every time you open a new terminal. [See Discussions here.](http://answers.ros.org/question/117801/how-to-get-the-line-source-develsetupbash-to-run-after-every-time-you-catkin_make/)

## Join the community 
* Sign up an account and start asking question on [ROS answers](http://answers.ros.org/questions/). The community, instead of any perticular person, always knows the answer. You will find it super useful. 

## Drive your simulated turtlebot around...

## The very Basic: custom messages, publish & subscribe messages

## Mapping in Turtlebot 
* Step by Step commands:
  1. `source /opt/ros/indigo/setup.bash`
  2. `roslaunch turtlebot_gazebo turtlebot_world.launch` Open the simulator.  
  3. `roslaunch turtlebot_teleop keyboard_teleop.launch` Open the controller for turtlebot.  
  4. `roslaunch turtlebot_rviz_launchers view_navigation.launch` 
  5. `roslaunch turtlebot_gazebo gmapping_demo.launch` 
  6. `roslaunch turtlebot_gazebo amcl_demo.launch` Enable automatic navigation.
  7. `rosrun map_server map_saver` Save the map. map.pgm and map.yaml will be saved to disk. map.pgm can be viewed by a standard image viewer. 
     
     `rosrun map_server map_server map.yaml` to reuse a safed map.
     
-----
## Robotics Keyword Dictionary 

* Arduino
* Raspberry pi
* Mbot
-----
* ROS

  It stands for Robot Operating System. http://www.ros.org/
* Turtlebot
* LIDAR
* SLAMA* search algorithm
* amcl
  AMCL stands for Adaptive Monte Carlo Localization. `amcl` is a probabilistic Dijkstralocalization system for a robot moving in 2D. It implements the adaptive (or KLD-sampling) Monte Carlo localization approach (as described by Dieter Fox), which uses a particle filter to track the pose of a robot against a known map. 
  - amcl package document: http://wiki.ros.org/amcl
  - What is it AMCL: https://youtu.be/htE5cClSy4Y   https://en.wikipedia.org/wiki/Monte_Carlo_localization
* Message - msg
* Topic 
* Publish
* Subscribe
* roscore
* roslaunch

-----
## Resource
* Map & Nav
  * Pathfinding algorithm: [A* search algorithm](https://en.wikipedia.org/wiki/A*_search_algorithm)
    
    [Dijkstra's algorithm](https://youtu.be/WN3Rb9wVYDY), 
    [Source Code](https://github.com/ros-planning/navigation/blob/kinetic-devel/navfn/src/navfn.cpp), 
    [Discussion](http://answers.ros.org/question/28366/why-navfn-is-using-dijkstra/), 
    https://youtu.be/KNXfSOx4eEE
  * Sending Goals to the Navigation Stack

    http://wiki.ros.org/navigation/Tutorials/SendingSimpleGoals
  * Simulating the ROS Navigation Stack (part 3)

    http://moorerobots.com/blog/post/3

