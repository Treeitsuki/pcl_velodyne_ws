# Setup PX4 Env
```bash
docker run -it --rm ubuntu:20.04

apt update
apt install git -y
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
cd PX4-Autopilot
make px4_sitl gazebo-classic
```
[[Bug] Unable to '"make px4_sitl gazebo-classic" #21917
](https://github.com/PX4/PX4-Autopilot/issues/21917)

# Example 
```bash
INFO  [px4] Startup script returned successfully
pxh> INFO  [tone_alarm] home set
INFO  [commander] Ready for takeoff!
pxh> commander takeoff
pxh> INFO  [commander] Armed by internal command
INFO  [tone_alarm] arming warning
INFO  [navigator] Using default takeoff altitude: 2.5 m
INFO  [commander] Takeoff detected
```

# References
[Gazebo Classic Simulation](https://docs.px4.io/main/en/sim_gazebo_classic/)

[ROS with Gazebo Classic Simulation](https://docs.px4.io/main/en/simulation/ros_interface.html)