
#### Table of Contents

* V2 - The TE Demo
  * A. Command Server
  * B. LEGO Assembly
  * C. Light Curtain Safety
  * D. Autonomous Robots
  * E. Miscellaneous
* V1 - The RR Demo
* Appendix
  * 

## V2 - The TE Demo
> 11.09.2023

The demo involves 
a. two Yaskawa robots (yk_architect and yk_destroyer) assembling chair and pyramid lego models,
b. one Yaskawa robot (yk_builder) working with AMR to assemble from LEGO kit
c. schedule and task visualization of (b)
d. light curtain safety for yk_architect and yk_destroyer
e. live simulation models for robot arms, AMRs, and light curtains

### A. Command Server
> Flask based server hosted on mfi-twin

```shell
mfi@mfi-twin$ ~/repos/mfi_commander/command_server.py
```
**Do not close the terminal**

This starts a web server where the states of tasks are published. 
- Check tasks by running in another terminal `$ curl http://localhost:5000/command`
- Post a task by using following syntax 
[USE ONLY FOR DEBUGGING. AVOID RUNNING THIS DURING ACTUAL DEMO] \
`curl -d '{"name":"yk_task", "status":"START"}' -H "Content-Type: application/json" -X POST http://localhost:5000/command`

> RUN ALL THE OTHER SECTIONS BEFORE RUNNING THE STEP BELOW

`curl -d '{"name":"amr_task1", "status":"START"}' -H "Content-Type: application/json" -X POST http://localhost:5000/command`

### B. LEGO Assembly
> ROS1, mfi-twin, yk_architect, yk_destroyer, yk_builder

1. Start YK-Architect, YK-Destroyer, YK-Builder
2. Once they boot up, ensure the following before running any commands
  - Ensure the LEGO assembly tool is on the YK-Architect and YK-Destroyer
  - Ensure the Hook tool is on the YK-Builder 
  - Ensure the tool is not touching any lego brick on the table, and has clearance above all LEGO bricks
    - If that's not the case, put the robot in "TEACH" mode, and jog +Z
    - Put it in the "REMOTE" mode when done
  - Ensure they are in "Remote" mode, by turning the key on the smart pendant
  - Ensure LEGO bricks are laid out in the following layout(s) \

[TBD by Ruixuan]

3. Run the following commands on the mfi-twin workstation
```shell
mfi@mfi-twin$ source repos/ros1_ws/devel/setup.bash
mfi@mfi-twin$ roslaunch testbed_utils TE_Demo.launch
```
- YK-Architect and YK-Destroyer should now be assembling and disassembling the LEGO bricks in a loop.
- YK-Builder will wait for commands from the web server.

4. Run Azure Kinect to enable AMR docking calibration

open terminal window
```shell
ssh mfi@yk-god
mfi@yk-god$ start_dummy_screen
```
this allows azure kinect to start via SSH, a pre-reqquisite for command below.

another terminal window. password = `lego`
```shell
ssh -X mfi@yk-god
mfi@yk-god$ export DISPLAY=:0
mfi@yk-god$ roslaunch azure_kinect_ros_driver kinect_rgbd.launch
```


### C. Light Curtain Safety
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

4. After RViz launches with robot models, run the following commands on red light curtain. password=`ilimlab`
```shell
ssh ilim@192.168.1.4
ilim@lc-rpi$ roslaunch plc_robot yaskawa_hull_1_2.launch
```
-  - Starts nodes for sending out safety curtains and monitoring them for intrusions.
   - Starts node for visualizing safety curtains on helper camera images.
 
### D. Autonomous Robots
> ROS2, mfi-twin, nb-1, nb-2

(TBD)

<hr>

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
ilim@lc-rpi-red$ roslaunch plc_robot yaskawa_hull_1_2.launch
```
-  - Starts nodes for sending out safety curtains and monitoring them for intrusions.
   - Starts node for visualizing safety curtains on helper camera images.
 
### C. Autonomous Robots
> ROS2, mfi-twin, nb-1, nb-2

1. Make sure the robots are positioned on the markers on the floor! 
    CMU1 on with its back wheels (dummy wheels) on the marker labeld 1 (direction specified on marker)
    CMU2 on with its back wheels (dummy wheels) on the marker labeld 2 (direction specified on marker)

2. Launching nav stack on both the robots.
    - Connect via VNC (Reminna or TightVNC, refer [Appendix 2](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix-2---ip-addresses-and-usernames-of-testbed-devices) and [Appendix 3](https://github.com/cmu-mfi/.github/edit/main/DEMO.md#appendix-3---vnc-connect)
    > steps below under (2) not needed if you see RVIZ in VNC window. Move to step 3.
    - in a new terminal run `launch_robot_nav` (it's an alias to the ros2 launch command and can be found in the bashrc)

    - in a new terminal run `launch_rviz`

Ensure robots are connected to Netgear5G (stuff only works with 5G for some reason.)

Do the above steps on each robot.

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

<hr>

## Appendix   
### Appendix 1 - Start ROS1 node for YK

* `lego_moveit_yk.launch`:  Connect with a robot. Also starts moveit interface and yk_tasks ros service interface. More info on yk_tasks available [here](https://github.com/cmu-mfi/motoman_ros1/blob/master/yk_tasks/README.md)
```
roslaunch testbed_utils lego_moveit_yk namespace:=yk_architect
```

### Appendix 2 - IP addresses, usernames, and passwords of testbed devices

| Device                 | Hostname               | IP Address             | Username           | Password           |
| ---------------------- | ---------------------- | ---------------------- | ------------------ | ------------------ |
| Main Workstation       | mfi-twin               | 192.168.1.2            | mfi                | lego               |
| PC - Robot Arms        | yk-god                 | 192.168.1.70           | mfi                | lego               |
| Yaskawa Robot A        | yk_architect           | 192.168.1.71           | NA                 | NA                 |
| Yaskawa Robot B        | yk_builder             | 192.168.1.72           | NA                 | NA                 |
| Yaskawa Robot C        | yk_creator             | 192.168.1.73           | NA                 | NA                 |
| Yaskawa Robot D        | yk_destroyer           | 192.168.1.74           | NA                 | NA                 |
| Light Curtain Red (Wired)| lc-rpi                 | 192.168.1.4             | ilim               | ilimlab            |
| Light Curtain Red (WiFi) | lc-rpi                 | 192.168.1.6             | ilim               | ilimlab            |
| Light Curtain Blue (Wired)| lc-rpi                 | 192.168.1.5             | ilim               | ilimlab            |
| Light Curtain Blue (WiFi) | lc-rpi                 | 192.168.1.3             | ilim               | ilimlab            |
| Neobotix 1 or nb-1        |                     | 192.168.1.100          | mfi                | neobotix           |
| Neobotix 2 or nb-2        |                     | 192.168.1.101          | mfi                | neobotix           |


### Appendix 3 - VNC Connect
