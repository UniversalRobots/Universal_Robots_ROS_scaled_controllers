# Scaled joint trajectory controller

This package contains a joint trajectory controller leveraging on-the-fly speed scaling to slow down
trajectories using a robot's teach pendant.


## position_controllers/ScaledJointTrajectoryController and velocity_controllers/ScaledJointTrajectoryController
These controllers work similar to the well-known
[`joint_trajectory_controller`](http://wiki.ros.org/joint_trajectory_controller).

However, they are extended to handle the robot's execution speed specifically. Because the default
`joint_trajectory_controller` would interpolate the trajectory with the configured time constraints
(ie: always assume maximum velocity and acceleration supported by the robot), this could lead to
significant path deviation due to multiple reasons:
 - The speed slider on the robot might not be at 100%, so motion commands sent from ROS would
   effectively get scaled down resulting in a slower execution.
 - The robot could scale down motions based on configured safety limits resulting in a slower motion
   than expected and therefore not reaching the desired target in a control cycle.
 - Motions might not be executed at all, e.g. because the robot is E-stopped or in a protective stop
 - Motion commands sent to the robot might not be interpreted, e.g. because there is no interpreter
   for ROS commands, such as the [`external_control`](https://github.com/UniversalRobots/Universal_Robots_ROS_Driver#prepare-the-robot)
   program node for Universal Robots running on the robot controller.
 - The program interpreting motion commands could be paused.

The following plot illustrates the problem:
![Trajectory execution with default trajectory controller](doc/traj_without_speed_scaling.png
"Trajectory execution with default trajectory controller")

The graph shows a trajectory with one joint being moved to a target point and back to its starting
point. As the joint's speed is limited to a very low setting on the teach pendant, speed scaling
(black line) activates and limits the joint speed (green line). As a result, the target
trajectory (light blue) doesn't get executed by the robot, but instead the pink trajectory is executed.
The vertical distance between the light blue line and the pink line is the path error in each
control cycle. We can see that the path deviation gets above 300 degrees at some point and the
target point at -6 radians never gets reached.

All of the cases mentioned above are addressed by the scaled trajectory versions. Trajectory execution
can be transparently scaled down using the speed slider on the teach pendant without leading to
additional path deviations. Pausing the program or hitting the E-stop effectively leads to
`speed_scaling` being 0 meaning the trajectory will not be continued until the program is continued.
This way, trajectory executions can be explicitly paused and continued.

With the scaled version of the trajectory controller the example motion shown in the previous diagram becomes:
![Trajectory execution with scaled_joint_trajectory_controller](doc/traj_with_speed_scaling.png
"Trajectory execution with scaled_joint_trajectory_controller")

The deviation between trajectory interpolation on the ROS side and actual robot execution stays minimal and the
robot reaches the intermediate setpoint instead of returning "too early" as in the example above.

Under the hood this is implemented by proceeding the trajectory not by a full time step but only by
the fraction determined by the current speed scaling. If speed scaling is currently at 50% then
interpolation of the current control cycle will start half a time step after the beginning of the
previous control cycle.

## Acknowledgement
Developed in collaboration between:

[<img height="60" alt="Universal Robots A/S" src="../scaled_controllers/doc/resources/ur_logo.jpg">](https://www.universal-robots.com/) &nbsp; and &nbsp;
[<img height="60" alt="FZI Research Center for Information Technology" src="../scaled_controllers/doc/resources/fzi_logo.png">](https://www.fzi.de).

***
<!-- 
    ROSIN acknowledgement from the ROSIN press kit
    @ https://github.com/rosin-project/press_kit
-->

<a href="http://rosin-project.eu">
  <img src="http://rosin-project.eu/wp-content/uploads/rosin_ack_logo_wide.png" 
       alt="rosin_logo" height="60" >
</a>

Supported by ROSIN - ROS-Industrial Quality-Assured Robot Software Components.  
More information: <a href="http://rosin-project.eu">rosin-project.eu</a>

<img src="http://rosin-project.eu/wp-content/uploads/rosin_eu_flag.jpg" 
     alt="eu_flag" height="45" align="left" >  

This project has received funding from the European Union’s Horizon 2020  
research and innovation programme under grant agreement no. 732287. 
