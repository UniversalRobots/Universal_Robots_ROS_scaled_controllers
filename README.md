# Scaled controllers

This repository contains controllers and hardware interface for `ros_control` that are leveraging an
on-the-fly speed scaling mechanism. For example, they are used by the
[`ur_robot_driver`](http://wiki.ros.org/ur_robot_driver).

For this, the following subpackages exist:

  * A **speed_scaling_interface** to read the value of the current speed scaling into controllers.
  * A **speed_scaling_state_controller** that publishes the current execution speed as reported by
  the robot to a topic interface. Values are floating points between 0 and 1.
  * A **scaled_joint_trajectory_controller** that is similar to the *joint_trajectory_controller*,
  but it uses the speed scaling reported by the robot to reduce execution speed of the trajectory.


## Acknowledgement
Developed in collaboration between:

[<img height="60" alt="Universal Robots A/S" src="scaled_controllers/doc/resources/ur_logo.jpg">](https://www.universal-robots.com/) &nbsp; and &nbsp;
[<img height="60" alt="FZI Research Center for Information Technology" src="scaled_controllers/doc/resources/fzi_logo.png">](https://www.fzi.de).

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
