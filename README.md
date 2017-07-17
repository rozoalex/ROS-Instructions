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

** WARNING: The Macbook pro 2016 or newer (the one with touchbar) seems not supporting ubuntu for now.**

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
* SLAM
* amcl
  AMCL stands for Adaptive Monte Carlo Localization. `amcl` is a probabilistic localization system for a robot moving in 2D. It implements the adaptive (or KLD-sampling) Monte Carlo localization approach (as described by Dieter Fox), which uses a particle filter to track the pose of a robot against a known map. 
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
  * Publishing to /move_base_simple/goal

  http://answers.ros.org/question/47973/publishing-to-move_base_simplegoal/
  * Simulating the ROS Navigation Stack (part 3)

  http://moorerobots.com/blog/post/3

