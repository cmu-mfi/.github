## V1 - The RR Demo
> 10.30.2023

The demo involves two Yaskawa robots doing staircase LEGO assembly in a loop, the red light curtain projecting dynamic curtains on the Yaskawa robots, and two Neobotix AMRs navigating to four corners of the testbed in a loop.

### A. LEGO Assembly
> ROS1, mfi-twin, yk-architect, yk-destroyer

1. Start YK-Architect and YK-Destroyer
2. Once they boot up, ensure the following before running any commands
  - Ensure the LEGO assembly tool is on the robot
  _{insert images here}_
  - Ensure the tool is not touching any lego brick on the table, and has clearance above all LEGO bricks
    - If that's not the case, put the robot in "TEACH" mode, and jog +Z
    - Put it in the "REMOTE" mode when done
  - Ensure they are in "Remote" mode, by turning the key on the smart pendant
  - Ensure LEGO bricks are laid out in the following layout \
  _{insert images here}_
3. Run the following commands on the mfi-twin workstation
```shell
mfi@mfi-twin$ source repos/ros1_ws/devel/setup.bash
mfi@mfi-twin$ roslaunch testbed_utils RR_Demo.launch
```
- Robots should now be assembling and disassembling the LEGO bricks in a loop

### B. Light Curtain Safety
> ROS1, lc-rpi-red, mfi-twin, yk-architect, yk-destroyer

1. Start YK-Architect, YK-Destroyer, Red LC device
2. Once they boot up, ensure the following:
  - There is a ROS1 node connected with the YK robots (architect and destroyer)
  - If you have followed the [LEGO Assembly](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#a-lego-assembly), then continue to next step
  - Otherwise, follow the steps in [Appendix 1](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix---start-ros1-node-for-yk) for both `yk_architect` and `yk_destroyer`
3. Run the following commands on mfi-twin workstation
```shell
mfi@mfi-twin$ source repos/ros1_ws/devel/setup.bash
mfi@mfi-twin$ roslaunch lc_utils setup_demo.launch
```
- - Starts node to publish joint positions of all robots needed for designing the light curtains. 
  - Publishes transforms between cameras, robots, and lasers.
  - Starts the demo rviz for the light curtain visualizations. 

4. After RViz launches with robot models, run the following commands on `lc-rpi-red`
```shell
ilim@lc-rpi-red$ roslaunch plc_robot yaskawa_hull_1_2.launch`
```
-  - Starts nodes for sending out safety curtains and monitoring them for intrusions.
   - Starts node for visualizing safety curtains on helper camera images.
 
### C. Autonomous Robots
> ROS2, mfi-twin, nb-1, nb-2
1. Launching nav stack on both the robots. Connect via VNC (Reminna or TightVNC, refer [Appendix 2](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix-2---ip-addresses-and-usernames-of-testbed-devices) and [Appendix 3](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix-3---vnc-connect)
    - in a new terminal run `launch_robot_nav` (it's an alias to the ros2 launch command and can be found in the bashrc)

    - in a new terminal run `launch_rviz`

Ensure robots are connected to Netgear5G (stuff only works with 5G for some reason.)

Do the above steps on each robot.

2. Make sure the robots are positioned on the markers on the floor! 
    CMU1 on with its back wheels (dummy wheels) on the marker labeld 1 (direction specified on marker)
    CMU2 on with its back wheels (dummy wheels) on the marker labeld 2 (direction specified on marker) 

3. Launching the waypoint commander from the server (digital twin pc)

    - ssh into the docker 
        `sudo docker exec -it ddg-humble-container bash`
    - export rmw (without this stuff will not run properly or run at all)
        `export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp`
    - source the workspace - 
        `source ../mrsd_teamh/mfi_multiagent_sim/ws/install/setup.bash`
    - run the multi-commander node! 
        `ros2 run multi_navigator multi_commander`


Expected output - the bots will keep on going in circles moving between the 4 corners of the testbed.

## Appendix   
### Appendix 1 - Start ROS1 node for YK

* `lego_moveit_yk.launch`:  Connect with a robot. Also starts moveit interface and yk_tasks ros service interface. More info on yk_tasks available [here](https://github.com/cmu-mfi/motoman_ros1/blob/master/yk_tasks/README.md)
```
roslaunch testbed_utils lego_moveit_yk namespace:=yk_architect
```

### Appendix 2 - IP addresses and usernames of testbed devices
### Appendix 3 - VNC Connect
