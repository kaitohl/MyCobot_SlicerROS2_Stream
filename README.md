# MyCobot_SlicerROS2_Stream

## Setup

**Step 1:** Ensure you have installed the pymycobot Python API

```bash
$ pip install pymycobot --user
```

For more details, see the Python API

**Step 2:** Create a ROS2 workspace folder, and a src folder in the workspace. We will use `ros2_mycobot` as our example workspace.

```bash
$ mkdir ~/ros2_mycobot/src
```

**Step 3:** Clone the MyCobot ROS2 repository in the src folder.

```bash
$ cd ~/ros2_mycobot/src
$ git clone https://github.com/elephantrobotics/mycobot_ros2.git
```

Ensure you are cloning the proper branch depending on your Ubuntu version. For more details, see the MyCobot ROS2 Repo

**Step 4:** Build your workspace.

```bash
$ cd ~/ros2_mycobot
$ colcon build
```

**Step 5:** Open `listen_real.py` from the path below:

```bash
$ /home/ros2_mycobot/src/mycobot_ros2/mycobot_280/mycobot_280/mycobot_280/listen_real.py
```

and change line 25 from

```python
self.declare_parameter('port','/dev/ttyUSB0')
```

to

```python
self.declare_parameter('port','/dev/ttyACM0')
```

**Step 6:** Rerun colcon build to update the changes in the workspace

```bash
$ cd ~/ros2_mycobot
$ colcon build
```

**Step 7:** Navigate to the robot's URDF folder from the path below

```bash
$ cd ~/ros2_mycobot/install/mycobot_description/share/mycobot_description/urdf/mycobot_280_m5
```

This folder is where the MyCobot 280 m5's URDF is located along with the .dae files that define 3D models of each joint.

**Step 8:** Replace the `mycobot_280_m5` folder with the one provided in this repository. The new folder contains .stl files of all the joints and an updated URDF file.

## Running

**Step 1:** Ensure the robot is connected to your device and in transponder mode. Run the following command to enable permissions for the connect port:

```bash
$ sudo chmod 777 /dev/ttyACM0
```

**Step 2:** Source the workspace. Note: Every new terminal you open, ensure to source the workspace

```bash
$ cd ~/ros2_mycobot
$ source install/setup.bash
```

**Step 3:** Run the following command:

```bash
$ ros2 run mycobot_280 listen_real
```

**Step 4:** Open another terminal and run the following command:

```bash
$ ros2 launch mycobot_280 slider_control.launch.py
```

**Step 5:** Open another terminal and run SlicerROS2. Using the default paramters in the module should work.
