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
A ROS system is made up of many different programs running simultaneously. Each program is called a _*node*_.  The nodes are communicating with one another with a peer-to-peer manner by passing _*messages*_.  That means messages are not passing through the *roscore* , each node just uses roscore to find each other.

* **Messages** are nothing fancy, but data structures.  Here is an example of a message:

<img src="https://lh3.googleusercontent.com/c8uLbDPLurDIuYd7_xHsp5d1RguPqD1mvvXI5lmwAGgfAAjWFV3-O58LvQjY3buM6R38LJaIFTEGSoRnhB8zsr0cJAlZrMgL-ms93LOPBROTi-YDRX64MuV56VFpBtMqCVfFsEHOicpfIFn6BUwKSo0BAJUdox0Q32t3_DlxDuYJNXpAebdB8cRvpITYfQocP0RYTJFzGmePFOFd4jMTdG7p6GoEJCfn07QF1B8WslS7U01oLH6zY8Rf0PiT025lGjKZPNEkP7QFSR9R6-bGRTNCZPcmFIh6If2_LEE11PqtqR6eJvLohgFDFoYMTlU3Sx90OlKrvh2iLbQl6tyDcC4FZIVW1WmUB3hr-8_2D9f5xRbI7NsCCbUWYQgoV3QHPrybPxk9Ef0hBnqd5IypuXC2-5igMvR15P00QUkV4SElu_kOSAO5Wtv4QVzP2-pF-5DFgEb3C23e8XRub3XHizqV2BFb4Ug5dYtglyeDIl8eJV0v4BX3ykcSYprCqOh9HUuFbBElTBu17vX6vwYDJSWLklenUriIQoft84DYYi9u5V7D6nOvFJ8loRX8TQ3UTQ-iDNJmtr-gPXHYxqsIY5k8PxCBN54Gyj_65bH_s20aXimrNfNqeA=w1304-h1002-no" width="600">

This message is called *Point*. It represents a point in a coordinate system. It has three float values x, y, z. A message is like a *structs* or *class without methods*. You will use a lot of this in the future. Anytime you want to do anything in ROS system, you have to have some kind of message to talk to the system (of course, you can create your own message which will be introduced later).  

* **Topics** are names for streams of some messages with defined types. For example, the [lidar](https://en.wikipedia.org/wiki/Lidar) sensor(the one is spinning on top of the turtlebot) is constantly *publishing* message [LaserScan](http://docs.ros.org/api/sensor_msgs/html/msg/LaserScan.html) on the topic named scan. In ROS, there are countless topics, *nodes* are posting messages on *topics* each time(with various rate). One classic way you want to manipulate the ros system is through **_taking the messages from topics, making use of them and posting some messages on some topics back_**. In ROS, it's called *Publish* and *Subscribe*. Lots of nodes are basically following this model. 

  A natural question to ask is: How do I know what topics are there? It's nice and easy, just use command `rostopic list`.
This will list all the topics that are currently existing in the system. What I mean by that is there are countless topic, but each time in your system there are only few nodes posting messages on some topics. I just need to care about ones that are currently existing.

  ![alt text](https://lh3.googleusercontent.com/adNhU01gzIbw1SkG_S2Lik-SOfWQqnp28LDz7M-N4OIj7OwXPNZLnOo-5TRztrrvDvaARiXKIyyZL91YSMGL2YwCFqOVqWq9GAJvL43ZuhsdRVe2qkxfk5mhXUi-qgKKdQDEp3Ov2MjKKMuZOz80PvQuVdWuqUy3ECVqYh-_UtTSnaKUB-FCxRT7IorxCKQEgJVcW3RSSP3tVvMaEe2Vf_ngPURRgfOJ-k1LB0qrhRTaN_RX68ecMY8u0hF1DslnXAarY_vK5Mw6XEp9SuZdNave3aIAlAPPOadcjNjmE2oSlCzyrhSMjlrL9T5kc9a2eLpYHS1QsKQ8NuFoiaj9vGLEqJQkGW2AgDcexpC3fjr4o3Icxc6_r9f9EJo8PhFGGiv7dZHLzteFHBN0uBteOGSGgg4F9y0VCjrJW0H1NnXj5Qz_W-ww74jQatuNWSookhMDgCx2S9ec_FFC4nT8hBIqC9gQ_p_yt7-Ewqu43FfwEimvEV9ZssjdUkAGvZqpjcKAJkNWp3UweYeyI_wNhto00J6qduxf7cOxEY6HKgvZp97hFpPqUMHCPTsoZvda8ugKX2yGNrgv-NhkxMCMKdtLmPMgylpJSjIm4yu4Pmi0z8LWLaca8PWOMyX0XmPIq5TIbCeQmPk4PwBprmr39MfckIATEq9Ozuo0c0qYwc7Y9oU=w492-h408-no "When you make rostopic list command in terminal")

  ROS gives a very convinient way of working with topics. 

  `rostopic info /odom` to view the odom topic.

  ![alt text](https://lh3.googleusercontent.com/4CH4PVYwG-zIGZUmZwsf2J-M5QoQTcqlWoxJdcbIIlmZoes3LVN1BnBMU1F6WqMjDv6j4XKdk5G4cqbFikEGEjqzfbcPViDKzcxEuZx3wM2WYg5UNqBCBoJsKb4CglAqKG6JL2-Fk5PZqs8kdR5VQg2lqZDEWs7z8vQhw-2-D830WRPBz_XPqOLlniO_xpv73drSpuRoLDdpdJITumuiAa1AfWflX25aK3CSROKisHVz5IwKm4xjsLvoeTJhXdhbvzW7fVFhdWfNlvj5C298LdUxTgx51pF_5CTDfj7-hcTuK7Amvw75d6F0FoPZV-ZvzIALs7hsXN-dp7DMHQVZlQkiuIofkFctiVP2MYaZutehF-Z1T4alR8d-v8OQiqEAyshbuZBOQKzRpGdjGhAWasBgQ9cgZDWNzAAMjDOTcS8x4dJ8igoVlyLrJmqOe6pZnHXcFWgvhkJcjmBTdLBtcGca3LmQ2LMuDi5pbsAfcB8H7cBo9yoSEbEgy3TskbYAZs7ldsTWJHZjRrjIQRmpfI6D5hKwGyT6jUQG8XV-6YWxthLdPJt9yZ-05z8dR2T65jILOUuhrg6VYRkCMBXgFRQxY1WHohfrEyZfdPH_9f-RGeRdZk2Nt7ezzYOqiazZbmZutg0vwETefEasVa7y08RtQB1SAtiJEaRlp0kSweJ1iBg=w492-h261-no "rostopic info /odom")

  /odom is the [odometry](https://en.wikipedia.org/wiki/Odometry) information currently in the system. As shown in the picture, the gazebo simulator is publishing odom and the android/virtual_joystick is subscribing this and the message type is [nav_msgs/Odometry](http://docs.ros.org/api/nav_msgs/html/msg/Odometry.html).

  `rostopic echo /odom` to view the data in real time.

  ![alt text](https://lh3.googleusercontent.com/_biKmwBO1bWtwGB_vTl7STekL0ftmPqocErWEWT83g4Ko8sRBa2vg4TF8v8PlzwzLnCLH7NtGySDb3NQfRflfzG8TfvHyJ2IuCBPwK1gR3esW-ZTrvELe-Dx86QO8Sw7n-mDN2rsa6b_L-iz5jXwPgAyYei2crFno-uUOpPoOZzlznfV9zNMkeLZnvM4iTl4rOU5-4HCA27K3wdUNjKB1idQAZdpIaDQg3OeWqmN6MkjS85i3q_4o30V2bWrrXqvipsYC_Jot2NSD_VWv8QOeSAjTBDG4cnWgFI3ds4qvbybbUKwnheto5i7xHSjKixN0t-zgGCcKu6JeNC-jsXzlo3pVu4b-Ea4sh285K5DxrlnBsqZ_uTK2BtKpc5zEVeX3f0zbbinqURt-ku24yZLApJzphsQFbldiRgaGiQHMhwPKdyHpgKS0U7i75ABT9e3pu2EcMla_JynDjb6teGcngq23q9vlx1aE4RIp5VtDsdP3wbRy9v_T4GLGZlWcZq2HEE5A2P1d9GwEs29d-TgIl1TVwjISmOFA0fXjLinLBeOesaZrNabFB6fQ1GYFjAaTqmPyVm-K33lqlK1y_aUgPyjSUE54BVcLTzCexlYTlie30vjYRYYd073IMGkZ-8tuUS48zLJOCcSrJ-t55-iQSvf3XO-62npb3h2730At_Pwibg=w730-h738-no "/odom data in real time")

  keep in mind these three command, you will use them a lot.


* **Services** are synchronous remote procedure calls. This term has the same meaning here as in elsewhere. For topics, subscribing and publishing are all happening on where the node is running. For services, after setting up the server, when you make a service call, the computation is sent to the server which is another node. A service call would look excactly like a normal function call, except the fact that it will wait for the result from server. 

  ![alt text](https://lh3.googleusercontent.com/CdbKkha9_FBDuQenD8F94Iu5lihtHWi7HY8QGrfd00vN7s2cYcwEBdfd5iLsA_I_wTv34rEY4zgSR7NHQfgsaUxNCmz5cEIY2J2OS3BdvgNBjE8VAIBxLVVLEi6sItNYU5ddZOhbZnWEo3V0hc4RGgYWGdwjaM707Z4xb53TDHQN0tbHogBtpD7U4nRgx-jewt9c2xnSMEoPpyLJtLCOVpzHcK7ank4S8ZeXOf2sKLzmTnJpFX9zAj9lHWXwOHyhwyirzKuc4aE8gm6Ic3DlrfMMpoTruvPgJk-BnzvwiCNJqZYFsPajUGyzpCMoYE3t2D2ID-bDlTpLo10T7jEtJQTqXA6tQhxAci_-5Cy2uMFzS0XXGhvqJZM5czGJ8gbUdwjKLp8z-VY9Q9XNdn42jxEPP1mLThq8KvxhMdlOwKvAdClEAUZieL_GP9mD7BuDECbFeEGEO8PFPpbLpBDIHCc_YQFtZ0627Ur4EMydDZLWsEizoozVAnZG2oz452v9EqMz3ASToWm623PUNbu-Jp2tg684nevtTMX4IfIzG9ilcVopFG3rUDwOGYjw_GDv-MB1zOgObo6jbmgqTWYTn0OVHwMzflp-Qly-TrIIPvJN9_caWaThpg=w1570-h202-no "Example of service call")

  The add_two_ints() is the local proxy function. It's obtained by asking from rospy(underlying ROS system). `'add_two_ints'` is the name of the service, which has been advertised before. The second parameter is the type of the service, which has to be defined before in a similar way as defining *messages*. The the call `add_two_ints(1, 2)`, is actually sent to other node to be computed. [Read more](http://wiki.ros.org/rospy/Overview/Services).

  The ROS system takes care of all the communication behind the scene. It's a good way to distribute the computation workload. Service calls are well suited to things that you only need to do **_occasionally_** and *that take a bounded time to complete*. For example, letting the robot navigate to a destination is not a well suited task for the service model, since you have no idea about when it can be done or if it can be done and you don't want to wait at the service call forever.   

* **Actions** are designed to solve this problem. ROS actions are the best way to implement interfaces to time-extended, goal-oriented behaviors like navigation. This will be introduced more throughfully in the future talk - Navigation in ROS. An action is defined with three part: goal, result and feedback. Each of them is some kind of data structure. Usually, actions, services and topics uses the same set of data structure for a easy communication. For actions, it's like service model, you have to have a server which is another node. The server will take a goal, react accordingly and send back a result. Also, you can set up a feedback which will be sent back to the client. (remember: feedbacks, results, and goals are all just messages, don't be confused.)

## Talk keynote 2: ROS Development — Workspace, Packages, Rosrun
Coding in ROS is actually straightforward, but the non-coding part can sometimes be frustrating. First of all, you have to know the idea of **workspace** and **packages**.

* **Workspace** is in where all your ROS code lives. It's nothing but a directory(a folder, to make it even clearer). Besides the code in underlying ROS system, all code in you want to use should be in the workspace. You can have multiple workspaces, but each time there can be only one in effect. 
  
  How does the system know which one and where it is? 
  * Everytime you want to start working on your code, you have to source a setup shell script file in the workspace. So that the system knows this particular workspace and code in your packages are what you are talking about. A lot of times, the reason people run into "package not found" error is because they forgot to source the setup file in the workspace. It's a pain to type in all the commands everytime you open a terminal. To aviod that, put in the source command in the .bashrc file, so that the terminal runs this command automatically. 
    
    `echo "source ~/(YOUR WORK SPACE)/devel/setup.bash" >> ~/.bashrc`
    
    Conventionally, the workspace is named as something like `catkin_ws`. [(What's catkin?)](http://wiki.ros.org/catkin/conceptual_overview)
    
    <img src="https://ak8.picdn.net/shutterstock/videos/15490690/thumb/1.jpg" width="400">

    Quick exmaple of commands for create a workspace(just for saving you some time and headache):
      1. `source /opt/ros/indigo/setup.bash` This sources system-wise ROS setup file, so that the terminal can find the commands in ROS.
      2. `mkdir -p ~/catkin_ws/src` and `cd ~/catkin_ws/src` 
      3. `catkin_init_workspace` This command creates a workspace directory call *catkin_ws*. (If you forgot to source, you will run in to a command-not-found error)
      4. `cd ~/catkin_ws` 
      5. `catkin_make` This command will build the all the code and meta-data into executables that you can run. The underlying ROS takes care of all that. If you use C++, you will have to call this every time you made some changes in your code. Since we are using python. We don't really pay a lot attention to this.
      6. `source /catkin_ws/devel/setup.bash` Source the setup file in your package, so that the system can find it. 

      ROS organizes the softwares into *packages*. All your packages will be in the src folder in your workspace. 

    

* **Packages** store all your code, data and metadat. 

  `cd ~/catkin_ws/src` & `catkin_create_pkg (WHATEVER-NAME-YOU-LIKE) rospy`
  
  Simple as that, you made a ROS package. Congratultions, you can start coding!
* **Programming Languages** 
  
  In theory, you can code for ROS in almost any main stream languages, but most people do it in python and c++. They will be our main focus. Due to the CMake structure, there are lots of annoying details if you are working with c++. This is **complicated**. It's strongly recommanded to watch and follow exactly this video.  
  [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/2Cmdu6mkxD0/0.jpg "ROS tutorial: C++ walkthrough of publisher & subscriber")](https://youtu.be/2Cmdu6mkxD0)
* **Learn Python in ROS** 
  After finishing following the first tutorial, now do the same to this tutorial. After that, you will find out how much your life will be easier with python. 

  [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/DLVyc9hOvk8/0.jpg "ROS tutorial: C++ walkthrough of publisher & subscriber")](https://youtu.be/DLVyc9hOvk8)

* **Your friends**

  Remember these are your friends:

  * `rostopic list`
  * `rostopic info /(The_Topic_You_Want_To_Know_More)`
  * `rostopic echo /(The_Topic_You_Want_To_Know_More_In_Real_Time)`
  * `rosmsg show (The_Message_You_Want_To_Know)`
  * [The AMAZING community](http://answers.ros.org/questions/)
  * GOOGLE!
## Talk keynote 3: Navigation in ROS — SLAM, Localization, Navigation Stack
* **What is SLAM?**

  Simultaneous localization and mapping (SLAM) is the computational problem of constructing or updating a map of an unknown environment while simultaneously keeping track of an agent's location within it ([wikipedia](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping)).
  
  [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/ml_pgbPEIz8/0.jpg "SLAM in action (record on computer screen)")](https://youtu.be/ml_pgbPEIz8)
  
  [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/yCTHY2m6ByE/0.jpg "SLAM in action (record with camera)")](https://youtu.be/yCTHY2m6ByE)
  
  Watch two videos, they are happening the same time.
  
  The map is save as a [pgm](https://en.wikipedia.org/wiki/Netpbm_format) image file and a [yaml](http://www.yaml.org/) configuration file. They are all human-readable and easy to understand. Open them and see what's going on. 
  
  **_Assignment_**: Read chapter 9 and 10. Build and save the map of *turtlebot_world* in simulator. Upload the map file you made, the yaml file and a writeup of what are they. Also List all the commands you used and tell what they do. 

  In ROS, the robot uses amcl package to localize itself in a map. 

* **AMCL** stands for Adaptive Monte Carlo localization ([original paper](http://robots.stanford.edu/papers/fox.aaai99.pdf)). 

  In ROS, the implementation is in a package called [amcl](http://wiki.ros.org/amcl). It basically takes all your sensor data, combines them, and tries to predict where the robot is in the map. The amcl package computes a set of [poses](http://docs.ros.org/api/geometry_msgs/html/msg/Pose.html) associated with possiblity, the one with highest possiblity with be published. 
  
* **Navigation Stack**

  Navigation is usually not an easy task. The one of the reason ROS is so powerful is that the navigation functionality is came in out-of-box. In ROS, you can simply send a goal to the navigation stack(this's an **_action_**). It will plan the path and navigate the robot for you. You can do it use API or Human interface to send this goal. 
  * Navigation with RVIZ 
    [![IMAGE ALT TEXT HERE](https://img.youtube.com/adfaadyCTHY2m6ByE/0.jpg "TODO TODO TODO TODO")](https://youtu.be/)
  * Navigation with API
    * [Sending Goals to the Navigation Stack](http://wiki.ros.org/navigation/Tutorials/SendingSimpleGoals)
    * Sample Code:
      1. [c++](https://github.com/rozoalex/ROS_NavigationControlPanel/blob/master/src/location_monitor.cpp)
      2. [python](https://github.com/rozoalex/ROS_NavigationControlPanel/blob/master/scripts/location_monitor_node.py)
      3. Demo
      
        In gazebo simulator:
      
        [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/qXnU-0Fiyxk/0.jpg "Navigation in Simulator")](https://youtu.be/qXnU-0Fiyxk)
	
	In Real World:
	
	[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/aVKmEijQYho/0.jpg "Navigation in Real World")](https://youtu.be/aVKmEijQYho)
	
	In real world, there are far more problems than in a simulator. Small things could cause failed navigation and localization. 
	
	<img src="https://lh3.googleusercontent.com/TIJ1lCJwJabmz19poIqIJMD1_Xs3xgE74ixO6fpc5-fUD0qXAjJyfamgrgG70V5Z6ep5X-9DK6ZO1CDiaKdgZ9esO5XFtqPy59_cYNVWxoskQAvP9bHuc8qpY7CZgb6JAh2WZXJuVzDs1WYXwNiNaqEkBTkscKjMwYQEehx3GiCxOcgqqxpR9h23IFM3agAvb2nXBfr_lLGKfK0MDa31eRZO0k4VG-A_VrrmasMRDFUpCa59gN-Fo45FU0xGwwT4a-aR3sbAnSM9Yr6AVoSdveycTWpo0IHnZUCwvoh_vulIRF5VEkRnVOk0QXf8NuLJZGr3wi3UKdOsL6yyBIP1qfq3MLVlvt0K2pqTxfU69KvZnKy1mWDLcOSnpWEGZpJhg5WB-HJPpqgrcxX8eYCkMY-1QXzx7V-GquMUfHMfrnAcZVjJNL7QpTtTyDLASI7mDpys9ARYsH5Peq8-tiCFYLu5xz-a-3BVs9QoVjE7D84z_myfJD_cvLBX4_maixZqZOAf5xqEUdMePKlJYV6NXXvLi1UmKSerk85tiS-v2QnPBsIXmhXFhjK1ujurwpDBD4jFJkfn39KYjKf-5OYhFHZRTTxqZHANbe2paac5Y4OL66nlCwblFxwZ7aiByvkRnpnj7FAgOzYR0pxqbXwzMuwQhyj8iR-rNiCXkex_k9Lg61g=w282-h502-no" width="300">
	
	<img src="https://lh3.googleusercontent.com/DaiR8sTn_T6Y2xTVpQ0galE9cYKwASaeKpMd5aKd8dfdR6eiZacNXnwZwDnp8fcqT1lePCvS0F0BtyTB_YsB3-cmayw_xg2G2oKrNGSaxMG61SHq7cGNf-RHmwzWCf60gOVOzAa2NnLZPRfwRvSqC2i3wsQHn1HVjJe4I7njleh_d1wSdBvsMS85UK0ZTM3J3ySYyMlZz_LsHwTRAi5CK8MNh_IP51kUp3Krxmzn6uqEKNVs7fa2sNf0TSlyCvdgNy-zpGJgFsEpUUgPVx0ff8MakP9_D_a98jkRGlMVRsbcfKG_2eYGkP9guIzYb3qLpao1N8oiLYegTAGARENKY-RkYEAlly7Q19xb-Q8Swx7fTj3dM5tK3STN_9i3WL0Vp8U644gwFUgUttaBwSWFyNiB9iAyYr2_-y-H3sP18YOb87aibgEoirO4A7ITt2jlHcI2JAshLKIbw8U2raZjeY_E3rKkvkb0gFM3lLgt7JLex_n2FpFo63HvdBRNYkU1Qfu1XTEMD-7_wkjtszgf_IbvRJPFH-ZIhmQ-byn2pvc9jbNjpc_D_RmgfjWTcbDJnEAU1Gjs136mUDcfZzlPdp_ZjSupcZPEKnN6sllQJ7j0DF-fYeGyDYrfNgPcxgEDQIsBnFhakZ8pI64TxsRNY33vcEeNpPIQl1swWZoqM_Vj-mg=w368-h656-no" width="300">
  




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

