## V1 - The RR Demo
> 10.30.2023

The demo involves two Yaskawa robots doing staircase LEGO assembly in a loop, the red light curtain projecting dynamic curtains on the Yaskawa robots, and two Neobotix AMRs navigating to four corners of the testbed in a loop.

### A. LEGO Assembly
> ROS1, mfi-twin, yk-architect, yk-destroyer

- Start YK-Architect and YK-Destroyer
- Once they boot up, ensure the following before running any commands
  - Ensure the LEGO assembly tool is on the robot
  _{insert images here}_
  - Ensure the tool is not touching any lego brick on the table, and has clearance above all LEGO bricks
    - If that's not the case, put the robot in "TEACH" mode, and jog +Z
    - Put it in the "REMOTE" mode when done
  - Ensure they are in "Remote" mode, by turning the key on the smart pendant
  - Ensure LEGO bricks are laid out in the following layout \
  _{insert images here}_
- Run the following commands on the mfi-twin workstation
```shell
mfi@mfi-twin$ source repos/ros1_ws/devel/setup.bash
mfi@mfi-twin$ roslaunch testbed_utils RR_Demo.launch
```
- Robots should now be assembling and disassembling the LEGO bricks in a loop

### B. Light Curtain Safety
> ROS1, lc-rpi-red, mfi-twin, yk-architect, yk-destroyer

- Start YK-Architect, YK-Destroyer, Red LC device
- Once they boot up, ensure the following:
  - There is a ROS1 node connected with the YK robots (architect and destroyer)
  - If you have followed the [LEGO Assembly](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#a-lego-assembly), then continue to next step
  - Otherwise, follow the steps in [Appendix 1](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix---start-ros1-node-for-yk) for both `yk_architect` and `yk_destroyer`
- Run the following commands on mfi-twin workstation
```shell
mfi@mfi-twin$ source repos/ros1_ws/devel/setup.bash
mfi@mfi-twin$ roslaunch lc_utils setup_demo.launch
```
- - Starts node to publish joint positions of all robots needed for designing the light curtains. 
  - Publishes transforms between cameras, robots, and lasers.
  - Starts the demo rviz for the light curtain visualizations. 

- After RViz launches with robot models, run the following commands on `lc-rpi-red`
```shell
ilim@lc-rpi-red$ roslaunch plc_robot yaskawa_hull_1_2.launch`
```
-  - Starts nodes for sending out safety curtains and monitoring them for intrusions.
   - Starts node for visualizing safety curtains on helper camera images.
 
### C. Autonomous Robots

## Appendix   
### Appendix 1 - Start ROS1 node for YK

* `lego_moveit_yk.launch`:  Connect with a robot. Also starts moveit interface and yk_tasks ros service interface. More info on yk_tasks available [here](https://github.com/cmu-mfi/motoman_ros1/blob/master/yk_tasks/README.md)
```
roslaunch testbed_utils lego_moveit_yk namespace:=yk_architect
```

### Appendix 2 - IP addresses and usernames of testbed devices
### Appendix 3 - VNC Connect
