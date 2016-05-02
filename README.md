tum_simulator on Kinetic Kame + gazebo-7.0.0
=============

I've updated the tum_simulator package to work with ROS Kinetic Kame and gazebo 7.0.0 from the newly released ubuntu 16.0.4. 
Make sure you have the ardrone_autonomy,joy and joystick_drivers ROS packages installed.

These packages are used to simulate the flying robot Ardrone in ROS environment using gazebo simulator. Totally they are 4 packages. Their functions are descript as below:

1. cvg_sim_gazebo: contains object models, sensor models, quadrocopter models, flying environment information and individual launch files for each objects and pure environment without any other objects.

2. cvg_sim_gazebo_plugins: contains gazebo plugins for the quadrocopter model. quadrotor_simple_controller is used to control the robot motion and deliver navigation information, such as: /ardrone/navdata. Others are plugins for sensors in the quadrocopter, such as: IMU sensor, sonar sensor, GPS sensor.

3. message_to_tf: is a package used to create a ros node, which transfers the ros topic /ground_truth/state to a /tf topic.

4. cvg_sim_msgs: contains message forms for the simulator.

Some packages are based on the tu-darmstadt-ros-pkg by Stefan Kohlbrecher, TU Darmstadt.

How to install the simulator:

1. Create a workspace for the simulator

    ```
    mkdir -p ~/ardrone_ws/src
    cd  ~/ardrone_ws/src
    catkin_init_workspace
    ```
2. Download dependencies

    ```
    git clone https://github.com/acpopescu/ardrone_joystick.git	# The AR.Drone joystick Driver
    git clone https://github.com/acpopescu/tum_simulator.git
    cd ..
    rosdep install --from-paths src --ignore-src --rosdistro kinetic -y
    ```
3. Build the simulator

    ```
    catkin_make
    ```
4. Source the environment

    ```
    source devel/setup.bash
    ```
How to run a simulation:

1. Run a simulation by executing a launch file in cvg_sim_gazebo package:

    ```
    roslaunch cvg_sim_gazebo ardrone_testworld.launch
    ```

2. Run the joystick control node

   ```
   roslaunch ardrone_joystick teleop.launch
   ```