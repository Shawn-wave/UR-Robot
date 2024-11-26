
# Universal Robots Control with ROS2 

## Requirements
- **Ubuntu**: 22.04
- **ROS2**: Humble


>- If you use an anaconda virtual environment, you might experience an error in the build.
>- But I've written down what to do in this case!


## ROS2 Setting

### 1. Starting the Robot
1. On the **teach pendant** screen, press the red button (power off) at the left bottom.
2. Press **Start** to power up the robot.

---

### 2. Installing `ros_humble_ur` Driver
```bash
sudo apt-get install ros-humble-ur
```
---
### 3. ROS2 Build Tools Installation
```bash
sudo apt install python3-colcon-common-extensions python3-vcstool
```
---
### 4. Create ROS2 Workspace
```bash
export COLCON_WS=~/ur_workspace/ros_ur_driver
mkdir -p $COLCON_WS/src
```
---
### 5. Cloning the Repository
```bash
cd $COLCON_WS
git clone -b humble https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver.git src/Universal_Robots_ROS2_Driver
```
---
### 6. Installing ROS Package Dependencies
```bash
vcs import src --skip-existing --input src/Universal_Robots_ROS2_Driver/Universal_Robots_ROS2_Driver-not-released.humble.repos
rosdep update
rosdep install --ignore-src --from-paths src -y
```
---
### 7. Building ROS2 Package
```bash
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```

>- If you used an anaconda virtual environment, you would have encountered an error in this code.
>- In this case, please run the following code first, before running the build code written above again!
```bash
pip install catkin_pkg empy==3.3.4 rosidl_adapter rosidl_parser rosidl_cmake numpy lark colcon-common-extensions
```


### ※ Build Complete Message ###
```bash
Summary: 7 packages finished [57.4s]
4 packages had stderr output: ur_calibration ur_controllers ur_dashboard_msgs ur_robot_driver
```


---

### 8. Setting Up Built Packages Environment
```bash
source install/setup.bash
```

---

### 9. Configuring IP Settings

1. **Robot IP**:

   Navigate to **Setup > Robot > Network** on the teach pendant.
   - IP address: `192.168.1.X`
   - Subnet mask: `255.255.255.0`
   - Default gateway: `192.168.1.1`
   - Preferred DNS server: `192.168.1.1`
   - Alternative DNS server: `0.0.0.0`

2. **PC (Host) IP**:
   
   IPv4 configuration set to Manual.
   - Address: `192.168.1.Y`
   - Netmask: `255.255.255.0`
   - Gateway: `192.168.1.1`

3. **Connection Test**:
   - Run the following command to confirm connection:
     ```bash
     ping 192.168.1.#
     ```

> **Important Notes:**
> - Replace `X` with a unique number for the robot (e.g., `192.168.1.100`)
> - Replace `Y` with a different unique number for the PC (e.g., `192.168.1.101`)
> - Ensure Robot and PC IPs are in the same subnet but different numbers

---

### 10. Setting up URCaps

1. Copy `externalcontrol-1.0.5.urcap` from `/ur_workspace/ros_ur_driver/src/Universal_Robots_ROS2_Driver/ur_robot_driver/resources` to a USB.
2. Plug the USB into the teach pendant, navigate to **System > URCaps**, open the file, and restart.
3. Go to **Installation > URCaps > External Control** on the pendant.
4. Write the **PC IP address** to Host IP.

Refer to the [URCap installation documentation](https://docs.universal-robots.com/Universal_Robots_ROS2_Documentation/doc/ur_robot_driver/ur_robot_driver/doc/installation/install_urcap_e_series.html) for more information.

---
## Robot control With MoveIt

1. Move the **ur_workspace/ros_ur_driver** directory and Start the ROS2 driver :

   ```bash
   ros2 launch ur_robot_driver ur_control.launch.py ur_type:=ur3e robot_ip:=192.168.1.# launch_rviz:=False
   ```

2. On the teach pendant, press the **Play** button at the bottom right.

3. Open a **new terminal** and Move the **ur_workspace/ros_ur_driver** directory and start the **.py**:
   ```bash
   ros2 launch ur_moveit_config ur_moveit.launch.py ur_type:=ur5e launch_rviz:=true
   ```


---

## Robot control Without MoveIt

1. Move the **ur_workspace/ros_ur_driver** directory and Start the ROS2 driver :

   ```bash
   ros2 launch ur_robot_driver ur_control.launch.py ur_type:=ur3e robot_ip:=192.168.1.#
   ```

2. On the teach pendant, press the **Play** button at the bottom right.

3. Open a **new terminal** and Move the **ur_workspace/ros_ur_driver** directory and start the **.py**:
   ```bash
   ros2 launch ur_robot_driver test_scaled_joint_trajectory_controller.launch.py
   ```

   - This code call `test_goal_publishers_config.yaml` from the `ur_workspace/ros_ur_driver/src/Universal_Robots_ROS2_Driver/ur_robot_driver/config` directory.

   - And call `publisher_scaled_joint_trajectory_controller` in yaml.

--- 

## Additional Resources
- For more detailed documentation, refer to the [Universal Robots ROS2 Documentation](https://docs.universal-robots.com/Universal_Robots_ROS2_Documentation/doc/ur_robot_driver/ur_robot_driver/doc/installation/installation.html).

- For more detailed documentation, refer to the [Universal Robots ROS2 Driver Git](https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver/tree/humble).

---


## Authored By
UR Study in **MARS** (Koreatech)
- Lee SeungHo (Team Lead)
- KI IROO
- Park SeeWoo
- Kim SeongMin
- Lee MinSeok

