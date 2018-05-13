# Control of a 3D Quadrotor #

## The Goal of this Project ##

In the real world the flight controller is usually implemented in C or C++. So in this project we will implement your controller in C++. The code you write here can eventually be transferred to a real drone!

<p align="center">
<img src="images/controls.png" width="500"/>
</p>

You may find it helpful to consult the [Python controller code](https://github.com/udacity/FCND-Controls/blob/solution/controller.py) as a reference when you build out this controller in C++.

## Writeup ##
- [README](./README.md) 

## Implemented Controller ##
- [QuadControlParams.txt](config/QuadControlParams.txt): This file contains the configuration for the controller. While the simulator is running, you can modify this file, and the simulator will "refresh" those parameters on the next loop execution.
- [QuadControl.cpp](src/QuadControl.cpp): This is where all the fun is, but I should not say this because this file contains the implementation of the controller only. Most of the time needed to pass the scenarios is spend on the parameter tuning.

### Implemented body rate control in C++. ###
#### The controller should be a proportional controller on body rates to commanded moments. The controller should take into account the moments of inertia of the drone when calculating the commanded moments. ####

- changes are reflected in [BodyRateControl](src/QuadControl.cpp#L113)
```
- Body rate controller collects the commanded roll, pitch and yaw.
- These are translated into desired rotational acceleration along the axis in the body frame(momentCmd).
- Calculation:  momentCmd = I * kpPQR * (pqrCmd - pqr);
- V3F structure is used to store moments of inertia in every asis (I)
- kpPQR is a V3F used to store proportional gains on angular velocity on all axes
- Simple proportional controller with error (pqrCmd - pqr) 
- error indicates desired body rates [rad/s](pqrCmd) – current or estimated body rates [rad/s](pqr)
```    

### Implement roll pitch control in C++. ###
#### The controller should use the acceleration and thrust commands, in addition to the vehicle attitude to output a body rate command. The controller should account for the non-linear transformation from local accelerations to body rates. Note that the drone's mass should be accounted for when calculating the target angles. ####

- changes are reflected in RollPitchControl(src/QuadControl.cpp#L141-L161)
```
- Purpose is to calculate a desired pitch and roll rates 
- Based on a desired global lateral acceleration, the current attitude, and desired collective thrust
- First we obtain current tilt from the rotation matrix R.
- Then we compute the desired tilt by normalizing the desired acceleration by the thrust. 
- Prevent drone flipping using max-min constrain
- Determines the desired roll and pitch rate in the world frame
- Finally, in order to output the desired roll and pitch rate in the body frame
- Tuning kpBank and kpPQR(again until the drone flies more or less stable upward)
```

### Implement altitude controller in C++. ###
#### The controller should use both the down position and the down velocity to command thrust. Ensure that the output value is indeed thrust (the drone's mass needs to be accounted for) and that the thrust includes the non-linear effects from non-zero roll/pitch angles.Additionally, the C++ altitude controller should contain an integrator to handle the weight non-idealities presented in scenario 4. ####

TBD

### Implement lateral position control in C++. ###
#### The controller should use the local NE position and velocity to generate a commanded local acceleration. ####

TBD

### Implement yaw control in C++. ###
#### The controller can be a linear/proportional heading controller to yaw rate commands (non-linear transformation not required). ####

TBD

### Implement calculating the motor commands given commanded thrust and moments in C++. ###
#### The thrust and moments should be converted to the appropriate 4 different desired thrust forces for the moments. Ensure that the dimensions of the drone are properly accounted for when calculating thrust from moments. ####

TBD

## Flight Evaluation ##
#### Your C++ controller is successfully able to fly the provided test trajectory and visually passes inspection of the scenarios leading up to the test trajectory. #####
Ensure that in each scenario the drone looks stable and performs the required task. Specifically check that the student's controller is able to handle the non-linearities of scenario 4 (all three drones in the scenario should be able to perform the required task with the same control gains used). 

TBD
