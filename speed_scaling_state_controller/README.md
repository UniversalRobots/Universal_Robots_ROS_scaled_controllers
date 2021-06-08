# Speed scaling state controller
This controller publishes the current actual execution speed as reported by the robot. Values are
floating points between 0 and 1.

## scaled_controllers/SpeedScalingStateController

In the [`ur_robot_driver`](http://wiki.ros.org/ur_robot_driver) this is calculated by multiplying the two [RTDE](https://www.universal-robots.com/articles/ur/real-time-data-exchange-rtde-guide/) data
fields `speed_scaling` (which should be equal to the value shown by the speed slider position on the
teach pendant) and `target_speed_fraction` (Which is the fraction to which execution gets slowed
down by the controller).

Filling this with the appropriate date is part of the robot hardware interface implementation.

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
