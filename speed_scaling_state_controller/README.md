# Speed scaling state controller
This controller publishes the current actual execution speed as reported by the robot. Values are
floating points between 0 and 1.

## scaled_controllers/SpeedScalingStateController

In the [`ur_robot_driver`](http://wiki.ros.org/ur_robot_driver) this is calculated by multiplying the two [RTDE](https://www.universal-robots.com/articles/ur/real-time-data-exchange-rtde-guide/) data
fields `speed_scaling` (which should be equal to the value shown by the speed slider position on the
teach pendant) and `target_speed_fraction` (Which is the fraction to which execution gets slowed
down by the controller).

Filling this with the appropriate date is part of the robot hardware interface implementation.
