# Balancing_ROBOT

## Balancing Rotary Inverted Pendulum

### Construction of Robot

The robot is made of three parts - base, arm, pendulum.
Base Link | Arm | Pendulum | Assembled-Setup
------------ | ------------- | ------------- | -------------
<img src="Images/base.png" width="200"/> | <img src="Images/arm.png" width="300"/> | <img src="Images/pendulum.png" width = "60"/> | <img src="Images/assembled_setup.png" width = "150"/>



They were modelled in solidworks, converted to urdf using [sw2urdf](http://wiki.ros.org/sw_urdf_exporter) plugin. The urdf is used by ROS to control robot and by  gazebo to simulate the robot.

### Controllers used in ROS

- Joint State Publisher - To get the current state of robot joints from gazebo. Here joint1 and joint2. It is available in ros.
- Joint Effort Controller - To control the torque applied to the particular joint. Here the torque is used to control joint1. Joint2 is a passive joint. It is available in ros.
- Balancing algorithm - To balance the pendulum in an upright position we have written a python program which commands the Joint Effort Controller how to change by reading joint values from Joint State Publisher.

### Balancing Algorithm

#### Classical Approach
Here we use the Linear Quadratic Regulator(LQR) and poleplacement to achieve stability around the unstable equilibrium point(i.e., upright position). The code for this is included in the package called "\robo". Since this algorithm is valid for a small range of values of angle for pendulum, we implement a pid controller for values outside this range(or for higher values of deviations in pendulum’s upright position). PID controller alone would not be able to stabilize the system, as it is very difficult to tune the pid values. PID results in a drift, which after some time accumulates and makes the system unstable. 

#### Machine Learning Approach 

Here we use Reinforcement Learning to balance the pendullum. The algorithm of reinforcement Learning used here is Deep Q Network. The algorithm is included in the package called "\ai_pen". It also includes algorithms such as qlearn, but Deep Q Netowork is only able to balance the pendulum. The agent learns throught action performed in the environment and resulting feedback. It takes approximately 1.30 to 2.00 hours to train the network.

### Video

This video demostrates the working of the robot when a small disturbance is given to the arm.

####           Using LQR            Using DQN
[<img src="Images/youtube_thumbnail.png" width="200"/>](https://www.youtube.com/watch?v=TlEo0WCmKsQ&feature=youtu.be "LQR Control")
[<img src="Images/youtube_thumbnail.png" width="200"/>](https://youtu.be/wCGOvAL2JPk "DQN Control")

### Note
>Put these files inside src of catkin workspace
